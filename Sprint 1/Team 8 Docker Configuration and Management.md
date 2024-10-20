Here are the specifications for **Team 8: Docker Configuration and Management**, written in the same LeetCode-style format. These APIs focus on managing Docker containers, images, and related configurations on the Osiris platform.

---

### API 1: Build Docker Image Command

**Problem:**
Implement the `buildDockerImage` API, which builds a Docker image from a specified Dockerfile.

**Type:** Function

**Function Signature:**
```python
def buildDockerImage(dockerfile_path: str, image_name: str, tags: list = None) -> bool:
    pass
```

**Description:**
- The `buildDockerImage` API builds a Docker image from a given Dockerfile and assigns it a name.
- Optionally, a list of tags can be applied to the image for versioning.
- It returns `True` if the image is successfully built, `False` otherwise.

**Input:**
- `dockerfile_path`: The file path to the Dockerfile. (string)
- `image_name`: The name to assign to the built image. (string)
- `tags`: An optional list of tags to apply to the image (e.g., `["latest", "v1.0"]`). (list of strings)

**Output:**
- `True` if the Docker image was successfully built, `False` otherwise.

**Sample Input:**
```python
response = buildDockerImage("./Dockerfile", "my-app-image", ["latest", "v1.0"])
```

**Sample Output:**
```python
response = True
```

---

### API 2: Push Docker Image Command

**Problem:**
Implement the `pushDockerImage` API, which pushes a Docker image to a remote registry.

**Type:** Function

**Function Signature:**
```python
def pushDockerImage(image_name: str, registry_url: str) -> bool:
    pass
```

**Description:**
- The `pushDockerImage` API pushes a locally built Docker image to a specified Docker registry.
- The image must have been built and tagged correctly before being pushed to the registry.

**Input:**
- `image_name`: The name of the Docker image to push, including tags if applicable. (string)
- `registry_url`: The URL of the Docker registry where the image should be pushed. (string)

**Output:**
- `True` if the Docker image was successfully pushed to the registry, `False` otherwise.

**Sample Input:**
```python
response = pushDockerImage("my-app-image:latest", "registry.hub.docker.com")
```

**Sample Output:**
```python
response = True
```

---

### API 3: Pull Docker Image Command

**Problem:**
Implement the `pullDockerImage` API, which pulls a Docker image from a remote registry.

**Type:** Function

**Function Signature:**
```python
def pullDockerImage(image_name: str, registry_url: str) -> bool:
    pass
```

**Description:**
- The `pullDockerImage` API pulls a Docker image from a specified Docker registry.
- The image must exist in the registry, and it is downloaded to the local system for use.

**Input:**
- `image_name`: The name of the Docker image to pull, including tags if applicable. (string)
- `registry_url`: The URL of the Docker registry from which the image should be pulled. (string)

**Output:**
- `True` if the Docker image was successfully pulled, `False` otherwise.

**Sample Input:**
```python
response = pullDockerImage("my-app-image:latest", "registry.hub.docker.com")
```

**Sample Output:**
```python
response = True
```

---

### API 4: Run Docker Container Command

**Problem:**
Implement the `runDockerContainer` API, which starts a new Docker container based on a specified image.

**Type:** Function

**Function Signature:**
```python
def runDockerContainer(image_name: str, container_name: str, ports: dict = None, env_vars: dict = None) -> bool:
    pass
```

**Description:**
- The `runDockerContainer` API starts a Docker container based on the specified image.
- Optionally, it can map ports and set environment variables for the container.

**Input:**
- `image_name`: The name of the Docker image to run. (string)
- `container_name`: The name to assign to the running container. (string)
- `ports`: An optional dictionary for port mapping (e.g., `{"8080": "80"}`). (dict)
- `env_vars`: An optional dictionary for setting environment variables in the container (e.g., `{"ENV": "production"}`). (dict)

**Output:**
- `True` if the Docker container was successfully started, `False` otherwise.

**Sample Input:**
```python
response = runDockerContainer("my-app-image:latest", "my-app-container", {"8080": "80"}, {"ENV": "production"})
```

**Sample Output:**
```python
response = True
```

---

### API 5: Stop Docker Container Command

**Problem:**
Implement the `stopDockerContainer` API, which stops a running Docker container.

**Type:** Function

**Function Signature:**
```python
def stopDockerContainer(container_name: str) -> bool:
    pass
```

**Description:**
- The `stopDockerContainer` API stops a running Docker container by its name.
- The function waits for the container to gracefully shut down before returning a response.

**Input:**
- `container_name`: The name of the Docker container to stop. (string)

**Output:**
- `True` if the Docker container was successfully stopped, `False` otherwise.

**Sample Input:**
```python
response = stopDockerContainer("my-app-container")
```

**Sample Output:**
```python
response = True
```

---

### API 6: Remove Docker Container Command

**Problem:**
Implement the `removeDockerContainer` API, which removes a Docker container from the system.

**Type:** Function

**Function Signature:**
```python
def removeDockerContainer(container_name: str) -> bool:
    pass
```

**Description:**
- The `removeDockerContainer` API removes a stopped Docker container by its name.
- This is useful for cleaning up containers that are no longer needed.

**Input:**
- `container_name`: The name of the Docker container to remove. (string)

**Output:**
- `True` if the Docker container was successfully removed, `False` otherwise.

**Sample Input:**
```python
response = removeDockerContainer("my-app-container")
```

**Sample Output:**
```python
response = True
```

---

### API 7: Inspect Docker Container Command

**Problem:**
Implement the `inspectDockerContainer` API, which retrieves detailed information about a Docker container.

**Type:** Function

**Function Signature:**
```python
def inspectDockerContainer(container_name: str) -> dict:
    pass
```

**Description:**
- The `inspectDockerContainer` API returns detailed information about a Docker container, including its status, resource usage, and environment settings.

**Input:**
- `container_name`: The name of the Docker container to inspect. (string)

**Output:**
- A dictionary containing detailed information about the container (e.g., `status`, `cpu_usage`, `memory_usage`, `ports`).

**Sample Input:**
```python
container_info = inspectDockerContainer("my-app-container")
```

**Sample Output:**
```python
container_info = {
    "status": "running",
    "cpu_usage": "10%",
    "memory_usage": "256MB",
    "ports": {"8080": "80"}
}
```

---

### API 8: List Docker Containers Command

**Problem:**
Implement the `listDockerContainers` API, which lists all Docker containers running on the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def listDockerContainers() -> list:
    pass
```

**Description:**
- The `listDockerContainers` API retrieves a list of all Docker containers running on the platform.
- It returns an array of container information, including the container name, image, and current status.

**Input:**
- None

**Output:**
- A list of running containers, with each entry containing the container name, image, and status.

**Sample Input:**
```python
containers = listDockerContainers()
```

**Sample Output:**
```python
containers = [
    {"name": "my-app-container", "image": "my-app-image:latest", "status": "running"},
    {"name": "another-container", "image": "another-image:latest", "status": "stopped"}
]
```

---

### API 9: Clean Docker System Command

**Problem:**
Implement the `cleanDockerSystem` API, which removes unused Docker images, containers, and volumes to free up disk space.

**Type:** Function

**Function Signature:**
```python
def cleanDockerSystem() -> bool:
    pass
```

**Description:**
- The `cleanDockerSystem` API removes all unused Docker images, stopped containers, and orphaned volumes to free up disk space.
- It performs a system-wide cleanup and ensures that only active resources remain.

**Input:**
- None

**Output:**
- `True` if the system was successfully cleaned, `False` otherwise.

**Sample Input:**
```python
response = cleanDockerSystem()
```

**Sample Output:**
```python
response = True
```

---

### API 10: Docker Logs Command

**Problem:**
Implement the `getDockerLogs` API, which retrieves the logs from a running Docker

 container.

**Type:** Function

**Function Signature:**
```python
def getDockerLogs(container_name: str, tail: int = 100) -> list:
    pass
```

**Description:**
- The `getDockerLogs` API retrieves the logs from a specified Docker container.
- The logs can be limited by the `tail` parameter, which specifies the number of recent log lines to retrieve.

**Input:**
- `container_name`: The name of the container from which to retrieve logs. (string)
- `tail`: The number of most recent log lines to retrieve (default is 100). (integer)

**Output:**
- A list of log entries (each entry is a string representing a log line).

**Sample Input:**
```python
logs = getDockerLogs("my-app-container", tail=50)
```

**Sample Output:**
```python
logs = [
    "2024-10-20 12:00:00 - Container started",
    "2024-10-20 12:00:01 - Service initialized",
    "2024-10-20 12:00:02 - Listening on port 8080"
]
```

---

These specifications provide core functionality for managing Docker containers, images, and configurations on the Osiris platform. Each command is designed to enable smooth deployment, management, and monitoring of Docker-based services.