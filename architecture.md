### Osiris Platform Detailed Technical Requirements

#### Overview
The Osiris platform will be a peer-to-peer style cluster where each container runs an instance of the same controller software. The platform will maintain a distributed ledger, similar to a blockchain, to keep track of all functions running across the cluster. Scaling decisions will be decentralized, with each controller capable of spawning new containers when needed.

#### 1. Architecture

1. **Peer-to-Peer Cluster**:
   - Each container runs an instance of the Osiris Controller.
   - Containers are peers and communicate with each other to maintain cluster state.

2. **Distributed Ledger**:
   - A blockchain-like ledger is maintained by each controller.
   - The ledger holds an index of all functions running on all containers.
   - Controllers synchronize their ledgers to ensure consistency.

3. **Decentralized Scaling**:
   - Each controller monitors resource usage and function backlogs.
   - Controllers can spawn new containers when reaching capacity thresholds.
   - Controllers can decide to run multiple instances of the same function if there is a backlog but the server is not at capacity.

#### 2. Osiris Controller

1. **Core Responsibilities**:
   - Monitor resource usage (CPU, memory, etc.).
   - Maintain a copy of the distributed ledger.
   - Communicate with other controllers to synchronize the ledger.
   - Make scaling decisions based on resource usage and function backlogs.
   - Spawn new containers and assign functions to them.

2. **Components**:
   - **Resource Monitor**:
     - Tracks CPU, memory, and other resource usage.
     - Reports resource usage to the controller.
   - **Ledger Manager**:
     - Maintains the local copy of the distributed ledger.
     - Synchronizes the ledger with other controllers.
     - Adds new functions to the ledger when they start.
     - Removes functions from the ledger when they stop.
   - **Scaling Manager**:
     - Analyzes resource usage and backlog information.
     - Decides when to spawn new containers.
     - Coordinates with other controllers to balance the load.
   - **Function Manager**:
     - Starts, stops, and manages functions on the local container.
     - Reports function status to the ledger manager.

#### 3. Distributed Ledger

1. **Structure**:
   - The ledger is a blockchain-like structure where each block contains:
     - A list of functions running on a specific container.
     - A timestamp.
     - A cryptographic hash of the previous block.
   - Each controller maintains a full copy of the ledger.

2. **Synchronization**:
   - Controllers periodically synchronize their ledgers to ensure consistency.
   - New blocks are broadcast to all controllers in the cluster.
   - Consensus algorithm ensures that all controllers agree on the current state of the ledger.

3. **Operations**:
   - **Add Function**: When a new function starts, the controller adds a new block with the function details.
   - **Remove Function**: When a function stops, the controller adds a new block with the updated state.
   - **Verify Ledger**: Controllers verify the integrity of their ledgers using the cryptographic hashes.

#### 4. Decentralized Scaling

1. **Threshold Monitoring**:
   - Each controller monitors its resource usage and function backlogs.
   - Thresholds for CPU, memory, and other resources are configurable.
   - When a threshold is reached, the controller decides whether to scale.

2. **Scaling Decisions**:
   - Controllers can decide to:
     - Spawn a new container if the local container is at capacity.
     - Run additional instances of a function locally if there is a backlog but sufficient resources.
   - Scaling decisions are based on a combination of resource usage and function demand.

3. **Spawning New Containers**:
   - Controllers use Terraform to provision new containers on the cluster.
   - The new container is assigned functions based on the backlog and resource availability.
   - The new container joins the cluster and starts running the assigned functions.

#### 5. Communication Protocol

1. **Inter-Controller Communication**:
   - Controllers communicate using a peer-to-peer protocol.
   - Messages include ledger updates, scaling requests, and function status updates.
   - Controllers use a gossip protocol to propagate information efficiently.

2. **Security**:
   - Communication between controllers is encrypted.
   - Authentication ensures that only authorized controllers can join the cluster.
   - The ledger is protected by cryptographic hashes to prevent tampering.

### Detailed Components

#### Core Components

1. **Controller**
   - **Description:** The Controller is the master service responsible for managing function deployments, traffic routing, load balancing, and instance scaling.
   - **Responsibilities:**
     - Register and deregister functions.
     - Route incoming requests to the appropriate function instances.
     - Monitor function execution and system load.
     - Scale function instances up or down based on demand.
     - Maintain the in-memory index ledger of all running functions.

2. **CLI (Command Line Interface)**
   - **Description:** The CLI is a client-side tool for developers to manage the Osiris platform, including function deployment, monitoring, and scaling.
   - **Responsibilities:**
     - Deploy new functions to the platform.
     - Update or remove existing functions.
     - Retrieve logs and performance metrics.
     - Manage user roles and permissions.

3. **Client-SDK**
   - **Description:** The Client-SDK is a set of libraries that developers use to call Osiris functions from their applications. It handles serialization of function calls into API requests and deserialization of responses.
   - **Responsibilities:**
     - Look up functions by name.
     - Serialize function arguments into JSON.
     - Make API calls to the Controller.
     - Deserialize API responses into function return values.

4. **Function-SDK**
   - **Description:** The Function-SDK is used on the server side to handle incoming API requests, deserialize them into function calls, and serialize the return values into API responses.
   - **Responsibilities:**
     - Deserialize API requests into function arguments.
     - Invoke the appropriate function with the deserialized arguments.
     - Serialize function return values into JSON responses.

5. **Dockerfile**
   - **Description:** Dockerfiles describe the container images for deploying the Osiris platform and its functions.
   - **Responsibilities:**
     - Define the environment and dependencies for the Controller, function instances, and other components.
     - Ensure consistent and reproducible deployments across different environments.

6. **Terraform**
   - **Description:** Terraform scripts define the infrastructure needed to deploy Osiris on various cloud providers or on-premises environments.
   - **Responsibilities:**
     - Provision the necessary compute, storage, and networking resources.
     - Manage infrastructure as code for versioning and reproducibility.
     - Ensure cloud-agnostic deployment capabilities.

#### Key Data Stores

1. **Function Library**
   - **Description:** The function library is a repository of all functions written for the Osiris platform. These functions are stored as executables.
   - **Responsibilities:**
     - Store function code and metadata.
     - Provide versioning and rollback capabilities.
     - Serve function executables to instances as needed.

2. **Index Ledger**
   - **Description:** The index ledger is an in-memory data store that lists all functions running throughout the system. It is kept in sync across all servers.
   - **Responsibilities:**
     - Track the state and location of all running function instances.
     - Provide quick lookups for the Controller to route requests.
     - Synchronize state changes across all instances to ensure consistency.

### Workflow

1. **Function Deployment**
   - Developer writes a function and uses the CLI to deploy it to Osiris.
   - The function is registered with the Controller and stored in the function library.
   - The function’s metadata is added to the index ledger.

2. **Function Invocation**
   - A client application calls a function using the Client-SDK.
   - The Client-SDK serializes the request and sends it to the Controller.
   - The Controller routes the request to the appropriate function instance.
   - The Function-SDK on the server deserializes the request and invokes the function.
   - The function executes and returns a result.
   - The Function-SDK serializes the result and sends it back to the Controller.
   - The Controller sends the response back to the Client-SDK.
   - The Client-SDK deserializes the response and returns it to the calling application.

3. **Scaling and Load Management**
   - The Controller monitors function load and demand.
   - When demand increases, the Controller starts additional instances of the required functions.
   - When demand decreases, the Controller shuts down idle instances.
   - The index ledger is updated to reflect the current state of all function instances.
