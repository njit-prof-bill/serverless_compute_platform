[Back to home.](./README.md)

Using Terraform can help achieve cloud agnosticism, as Terraform provides a consistent way to define and provision infrastructure across multiple cloud providers. Below is a detailed description of how to use Terraform to manage Docker Swarm infrastructure on AWS, Azure, GCP, and on-premises environments.

### AWS

1. **Setup Terraform Configuration:**
   - Create a Terraform configuration file (`main.tf`) to define your AWS infrastructure.

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "swarm_manager" {
  ami           = "ami-<your-ami-id>"
  instance_type = "t3.medium"

  user_data = <<-EOF
              #!/bin/bash
              docker swarm init
              EOF

  tags = {
    Name = "SwarmManager"
  }
}

resource "aws_instance" "swarm_worker" {
  count         = 3
  ami           = "ami-<your-ami-id>"
  instance_type = "t3.medium"

  user_data = <<-EOF
              #!/bin/bash
              docker swarm join --token <manager-token> <manager-ip>:2377
              EOF

  tags = {
    Name = "SwarmWorker"
  }
}
```

2. **Provision Infrastructure:**
   - Initialize Terraform and apply the configuration:
     ```sh
     terraform init
     terraform apply
     ```

### Azure

1. **Setup Terraform Configuration:**
   - Create a Terraform configuration file (`main.tf`) for Azure infrastructure.

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "West US"
}

resource "azurerm_virtual_network" "example" {
  name                = "example-network"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
}

resource "azurerm_subnet" "internal" {
  name                 = "internal"
  resource_group_name  = azurerm_resource_group.example.name
  virtual_network_name = azurerm_virtual_network.example.name
  address_prefixes     = ["10.0.2.0/24"]
}

resource "azurerm_network_interface" "example" {
  name                = "example-nic"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.internal.id
    private_ip_address_allocation = "Dynamic"
  }
}

resource "azurerm_virtual_machine" "swarm_manager" {
  name                  = "swarm-manager"
  location              = azurerm_resource_group.example.location
  resource_group_name   = azurerm_resource_group.example.name
  network_interface_ids = [azurerm_network_interface.example.id]
  vm_size               = "Standard_DS1_v2"

  delete_os_disk_on_termination = true
  delete_data_disks_on_termination = true

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }

  storage_os_disk {
    name              = "swarmmanagerosdisk"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }

  os_profile {
    computer_name  = "swarmmanager"
    admin_username = "<admin-username>"
    admin_password = "<admin-password>"
    custom_data = <<-EOF
                  #!/bin/bash
                  docker swarm init
                  EOF
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}

resource "azurerm_virtual_machine" "swarm_worker" {
  count                 = 3
  name                  = "swarm-worker-${count.index}"
  location              = azurerm_resource_group.example.location
  resource_group_name   = azurerm_resource_group.example.name
  network_interface_ids = [azurerm_network_interface.example.id]
  vm_size               = "Standard_DS1_v2"

  delete_os_disk_on_termination = true
  delete_data_disks_on_termination = true

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }

  storage_os_disk {
    name              = "swarmworkerosdisk"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }

  os_profile {
    computer_name  = "swarmworker-${count.index}"
    admin_username = "<admin-username>"
    admin_password = "<admin-password>"
    custom_data = <<-EOF
                  #!/bin/bash
                  docker swarm join --token <manager-token> <manager-ip>:2377
                  EOF
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}
```

2. **Provision Infrastructure:**
   - Initialize Terraform and apply the configuration:
     ```sh
     terraform init
     terraform apply
     ```

### GCP

1. **Setup Terraform Configuration:**
   - Create a Terraform configuration file (`main.tf`) for GCP infrastructure.

```hcl
provider "google" {
  project = "<your-project-id>"
  region  = "us-central1"
}

resource "google_compute_instance" "swarm_manager" {
  name         = "swarm-manager"
  machine_type = "n1-standard-1"
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-9"
    }
  }

  network_interface {
    network       = "default"
    access_config = {}
  }

  metadata_startup_script = <<-EOF
                            #!/bin/bash
                            docker swarm init
                            EOF
}

resource "google_compute_instance" "swarm_worker" {
  count        = 3
  name         = "swarm-worker-${count.index}"
  machine_type = "n1-standard-1"
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-9"
    }
  }

  network_interface {
    network       = "default"
    access_config = {}
  }

  metadata_startup_script = <<-EOF
                            #!/bin/bash
                            docker swarm join --token <manager-token> <manager-ip>:2377
                            EOF
}
```

2. **Provision Infrastructure:**
   - Initialize Terraform and apply the configuration:
     ```sh
     terraform init
     terraform apply
     ```

### On-Premises

1. **Setup Terraform Configuration:**
   - Create a Terraform configuration file (`main.tf`) for on-premises infrastructure using tools like Libvirt or Vagrant.

```hcl
provider "libvirt" {
  uri = "qemu:///system"
}

resource "libvirt_domain" "swarm_manager" {
  name   = "swarm-manager"
  memory = "1024"
  vcpu   = 1

  disk {
    volume_id = "${libvirt_volume.manager.id}"
  }

  network_interface {
    network_name = "default"
  }

  cloudinit = "${libvirt_cloudinit_disk.common-init.id}"

  console {
    type        = "pty"
    target_port = "0"
    target_type = "serial"
  }

  user_data = <<-EOF
              #!/bin/bash
              docker swarm init
              EOF
}

resource "libvirt_domain" "swarm_worker" {
  count  = 3
  name   = "swarm-worker-${count.index}"
  memory = "1024"
  vcpu   = 1

  disk {
    volume_id = "${libvirt_volume.worker[count.index].id}"
  }

  network_interface {
    network_name = "default"
  }

  cloudinit = "${libvirt_cloudinit_disk.common-init.id}"

  console {
    type        = "pty"
    target_port = "0"
    target_type = "serial"
  }

  user_data = <<-EOF
              #!/bin/bash
              docker swarm join --token <manager-token> <manager-ip>:2377
              EOF
}

resource "libvirt_cloudinit_disk" "common-init" {
  name           = "common-init.iso"
  user_data      = <<-EOF
                  #cloud-config
                  EOF
  user_data_fallback = <<-EOF
                      #cloud-config
                      EOF
}
```

2. **Provision Infrastructure:**
   - Initialize Terraform and apply the configuration:
     ```sh
     terraform init
     terraform apply
     ```

### Using Terraform to Manage Docker Containers Directly

Using Terraform scripts to start and stop containers directly can simplify our infrastructure management and still allow us to maintain cloud agnosticism. This approach removes the need for a dedicated orchestration tool like Docker Swarm, as Terraform can manage the lifecycle of your containerized applications across multiple cloud providers and on-premises environments. Here’s how you can achieve this:

### AWS Example

1. **Terraform Configuration for AWS:**

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "osiris_container" {
  count         = var.container_count
  ami           = "ami-<your-ami-id>"
  instance_type = "t3.micro"

  user_data = <<-EOF
              #!/bin/bash
              docker run -d --name osiris-container-${count.index} my_osiris_image
              EOF

  tags = {
    Name = "OsirisContainer-${count.index}"
  }
}

variable "container_count" {
  description = "Number of containers to run"
  default     = 1
}
```

2. **Provisioning Containers:**
   - Initialize Terraform and apply the configuration with the desired number of containers:
     ```sh
     terraform init
     terraform apply -var "container_count=3"
     ```

### Azure Example

1. **Terraform Configuration for Azure:**

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_virtual_machine" "osiris_container" {
  count                  = var.container_count
  name                   = "osiris-container-${count.index}"
  location               = azurerm_resource_group.example.location
  resource_group_name    = azurerm_resource_group.example.name
  network_interface_ids  = [azurerm_network_interface.example.id]
  vm_size                = "Standard_DS1_v2"

  delete_os_disk_on_termination = true
  delete_data_disks_on_termination = true

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }

  storage_os_disk {
    name              = "osdisk"
    caching           = "ReadWrite"
    create_option     = "FromImage"
    managed_disk_type = "Standard_LRS"
  }

  os_profile {
    computer_name  = "osiriscontainer-${count.index}"
    admin_username = "<admin-username>"
    admin_password = "<admin-password>"
    custom_data = <<-EOF
                  #!/bin/bash
                  docker run -d --name osiris-container-${count.index} my_osiris_image
                  EOF
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}

variable "container_count" {
  description = "Number of containers to run"
  default     = 1
}
```

2. **Provisioning Containers:**
   - Initialize Terraform and apply the configuration with the desired number of containers:
     ```sh
     terraform init
     terraform apply -var "container_count=3"
     ```

### GCP Example

1. **Terraform Configuration for GCP:**

```hcl
provider "google" {
  project = "<your-project-id>"
  region  = "us-central1"
}

resource "google_compute_instance" "osiris_container" {
  count        = var.container_count
  name         = "osiris-container-${count.index}"
  machine_type = "n1-standard-1"
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-9"
    }
  }

  network_interface {
    network       = "default"
    access_config = {}
  }

  metadata_startup_script = <<-EOF
                            #!/bin/bash
                            docker run -d --name osiris-container-${count.index} my_osiris_image
                            EOF
}

variable "container_count" {
  description = "Number of containers to run"
  default     = 1
}
```

2. **Provisioning Containers:**
   - Initialize Terraform and apply the configuration with the desired number of containers:
     ```sh
     terraform init
     terraform apply -var "container_count=3"
     ```

### On-Premises Example

1. **Terraform Configuration for On-Premises using Libvirt:**

```hcl
provider "libvirt" {
  uri = "qemu:///system"
}

resource "libvirt_domain" "osiris_container" {
  count   = var.container_count
  name    = "osiris-container-${count.index}"
  memory  = "1024"
  vcpu    = 1
  network_interface {
    network_name = "default"
  }

  disk {
    volume_id = "${libvirt_volume.osiris_container_volume[count.index].id}"
  }

  cloudinit = "${libvirt_cloudinit_disk.osiris_container_cloudinit.id}"

  console {
    type        = "pty"
    target_port = "0"
    target_type = "serial"
  }

  user_data = <<-EOF
              #!/bin/bash
              docker run -d --name osiris-container-${count.index} my_osiris_image
              EOF
}

resource "libvirt_volume" "osiris_container_volume" {
  count = var.container_count
  name  = "osiris-container-volume-${count.index}"
  pool  = "default"
  source {
    url = "https://cloud.centos.org/centos/7/images/CentOS-7-x86_64-GenericCloud.qcow2"
  }
  format = "qcow2"
}

resource "libvirt_cloudinit_disk" "osiris_container_cloudinit" {
  count = var.container_count
  name  = "osiris-container-cloudinit-${count.index}.iso"
  user_data = <<-EOF
              #cloud-config
              EOF
}

variable "container_count" {
  description = "Number of containers to run"
  default     = 1
}
```

2. **Provisioning Containers:**
   - Initialize Terraform and apply the configuration with the desired number of containers:
     ```sh
     terraform init
     terraform apply -var "container_count=3"
     ```

[Back to home.](./README.md)
