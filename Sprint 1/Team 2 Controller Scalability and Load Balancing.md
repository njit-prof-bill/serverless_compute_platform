Here are the specifications for **Team 2: Controller Scalability and Load Balancing APIs**, written in the same LeetCode-style format. These APIs focus on scaling decisions, load management, and container instance monitoring.

---

### API 1: Get Current Load API

**Problem:**
Implement the `getCurrentLoad` API, which retrieves the current CPU and memory usage on the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def getCurrentLoad() -> dict:
    pass
```

**Description:**
- The function `getCurrentLoad` retrieves the current CPU and memory usage of the platform.
- The response contains the percentage of CPU and memory utilization.

**Input:**
- None

**Output:**
- A dictionary containing `cpu_usage` and `memory_usage` (as percentages).

**Sample Input:**
```json
{}
```

**Sample Output:**
```json
{
  "cpu_usage": 45.0,
  "memory_usage": 70.5
}
```

---

### API 2: Scale Up Instances API

**Problem:**
Implement the `scaleUpInstances` API to provision additional containers when resource usage exceeds a defined threshold.

**Type:** Function

**Function Signature:**
```python
def scaleUpInstances(instance_count: int) -> bool:
    pass
```

**Description:**
- The function `scaleUpInstances` provisions additional containers to handle increased load.
- It accepts the number of additional instances to be created as input.

**Input:**
- `instance_count`: The number of new instances to spin up. (integer)

**Output:**
- `True` if the scaling operation succeeds, `False` otherwise.

**Sample Input:**
```json
{
  "instance_count": 3
}
```

**Sample Output:**
```json
{
  "result": true
}
```

---

### API 3: Scale Down Instances API

**Problem:**
Implement the `scaleDownInstances` API to decommission containers when resource usage drops below a defined threshold.

**Type:** Function

**Function Signature:**
```python
def scaleDownInstances(instance_count: int) -> bool:
    pass
```

**Description:**
- The function `scaleDownInstances` reduces the number of active instances by decommissioning idle containers.
- It accepts the number of instances to remove as input.

**Input:**
- `instance_count`: The number of instances to terminate. (integer)

**Output:**
- `True` if the scaling down succeeds, `False` otherwise.

**Sample Input:**
```json
{
  "instance_count": 2
}
```

**Sample Output:**
```json
{
  "result": true
}
```

---

### API 4: Get Active Instances API

**Problem:**
Implement the `getActiveInstances` API to retrieve a list of all active containers currently running in the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def getActiveInstances() -> list:
    pass
```

**Description:**
- The function `getActiveInstances` returns a list of all active container instances running on the platform.
- Each instance is represented by its ID and resource usage.

**Input:**
- None

**Output:**
- A list of active instances, where each instance includes its `instance_id`, `cpu_usage`, and `memory_usage`.

**Sample Input:**
```json
{}
```

**Sample Output:**
```json
[
  {
    "instance_id": "i-12345",
    "cpu_usage": 65.0,
    "memory_usage": 75.0
  },
  {
    "instance_id": "i-67890",
    "cpu_usage": 35.0,
    "memory_usage": 45.0
  }
]
```

---

### API 5: Auto-Scaling Status API

**Problem:**
Implement the `getAutoScalingStatus` API to check if the auto-scaling feature is enabled or disabled.

**Type:** Function

**Function Signature:**
```python
def getAutoScalingStatus() -> str:
    pass
```

**Description:**
- The function `getAutoScalingStatus` returns whether the auto-scaling feature is currently enabled or disabled on the platform.

**Input:**
- None

**Output:**
- A string indicating whether auto-scaling is `"enabled"` or `"disabled"`.

**Sample Input:**
```json
{}
```

**Sample Output:**
```json
{
  "auto_scaling": "enabled"
}
```

---

### API 6: Set Auto-Scaling Threshold API

**Problem:**
Implement the `setAutoScalingThreshold` API to define the CPU and memory usage thresholds that trigger automatic scaling.

**Type:** Function

**Function Signature:**
```python
def setAutoScalingThreshold(cpu_threshold: float, memory_threshold: float) -> bool:
    pass
```

**Description:**
- The function `setAutoScalingThreshold` configures the CPU and memory usage percentages at which the platform will trigger auto-scaling.
- It accepts two input parameters: `cpu_threshold` and `memory_threshold`, representing the usage percentages that trigger scaling.

**Input:**
- `cpu_threshold`: The CPU usage percentage that will trigger scaling. (float)
- `memory_threshold`: The memory usage percentage that will trigger scaling. (float)

**Output:**
- `True` if the threshold settings are successfully applied, `False` otherwise.

**Sample Input:**
```json
{
  "cpu_threshold": 80.0,
  "memory_threshold": 75.0
}
```

**Sample Output:**
```json
{
  "result": true
}
```

---

These API specifications provide the necessary scaling and load-balancing capabilities for the Osiris platform, ensuring that it can dynamically adjust to changes in demand by adding or removing containers as necessary. Each API provides mock responses to allow initial testing.