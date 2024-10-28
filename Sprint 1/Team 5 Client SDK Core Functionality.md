Here are the specifications for **Team 5: Client SDK Core Functionality**, written in the same LeetCode-style format. These APIs allow client applications to interact with the Osiris platform for function invocation and response handling.

---

### API 1: Call Function Command

**Problem:**
Implement the `callFunction` API in the client SDK, which allows a client to invoke a function deployed on the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def callFunction(function_name: str, *args: list) -> any:
    pass
```

**Description:**
- The `callFunction` API is used to invoke a function on the Osiris platform.
- It takes the function name and a list of arguments as input and returns the result of the function execution.

**Input:**
- `function_name`: The name of the function to invoke. (string)
- `args`: A list of arguments to pass to the function. (list of any)

**Output:**
- The result of the function execution (any).

**Sample Input:**
```python
response = callFunction("addNumbers", 3, 5)
```

**Sample Output:**
```python
response = 8
```

---

### API 2: Async Function Call Command

**Problem:**
Implement the `callFunctionAsync` API in the client SDK, which allows a client to invoke a function asynchronously on the Osiris platform.

**Type:** Function

**Function Signature:**
```python
async def callFunctionAsync(function_name: str, *args: list) -> any:
    pass
```

**Description:**
- The `callFunctionAsync` API allows the client to invoke a function asynchronously, which is useful for non-blocking operations.
- It returns a result or an error upon completion of the function execution.

**Input:**
- `function_name`: The name of the function to invoke asynchronously. (string)
- `args`: A list of arguments to pass to the function. (list of any)

**Output:**
- The result of the asynchronous function execution.

**Sample Input:**
```python
result = await callFunctionAsync("addNumbers", 2, 7)
```

**Sample Output:**
```python
result = 9
```

---

### API 3: Get Function Result Command

**Problem:**
Implement the `getFunctionResult` API in the client SDK, which retrieves the result of a previously invoked function.

**Type:** Function

**Function Signature:**
```python
def getFunctionResult(request_id: str) -> any:
    pass
```

**Description:**
- The `getFunctionResult` API retrieves the result of a function using its `request_id`.
- This is useful in cases where the function was invoked asynchronously, and the result is needed later.

**Input:**
- `request_id`: The unique ID of the request whose result is to be retrieved. (string)

**Output:**
- The result of the function execution.

**Sample Input:**
```python
result = getFunctionResult("request-123")
```

**Sample Output:**
```python
result = 15
```

---

### API 4: Serialize Function Arguments Command

**Problem:**
Implement the `serializeArgs` API in the client SDK, which serializes function arguments into a format suitable for transmission to the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def serializeArgs(*args: list) -> str:
    pass
```

**Description:**
- The `serializeArgs` API serializes the provided function arguments into a JSON string for transmission to the Osiris platform.
- It handles different data types, ensuring the arguments are correctly formatted.

**Input:**
- `args`: A list of arguments to serialize. (list of any)

**Output:**
- A JSON string representing the serialized arguments.

**Sample Input:**
```python
serialized = serializeArgs(1, "hello", {"key": "value"})
```

**Sample Output:**
```python
serialized = '[1, "hello", {"key": "value"}]'
```

---

### API 5: Deserialize Function Response Command

**Problem:**
Implement the `deserializeResponse` API in the client SDK, which deserializes the function response received from the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def deserializeResponse(response: str) -> any:
    pass
```

**Description:**
- The `deserializeResponse` API deserializes the JSON response received from the Osiris platform back into the appropriate Python objects.
- It ensures that the data is correctly interpreted based on its type.

**Input:**
- `response`: The JSON string received from the function execution. (string)

**Output:**
- The deserialized response in its original type.

**Sample Input:**
```python
deserialized = deserializeResponse('{"result": 8}')
```

**Sample Output:**
```python
deserialized = {"result": 8}
```

---

### API 6: Set Request Timeout Command

**Problem:**
Implement the `setTimeout` API in the client SDK, which sets a timeout for function requests to the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def setTimeout(timeout: int) -> None:
    pass
```

**Description:**
- The `setTimeout` API allows clients to define a timeout (in milliseconds) for requests made to the Osiris platform.
- If the function call does not return a response within the specified timeout, an error is triggered.

**Input:**
- `timeout`: The time (in milliseconds) before the request times out. (integer)

**Output:**
- None

**Sample Input:**
```python
setTimeout(3000)  # 3 seconds timeout
```

**Sample Output:**
```python
# No output, timeout set to 3000 milliseconds.
```

---

### API 7: Handle Function Errors Command

**Problem:**
Implement the `handleFunctionError` API in the client SDK, which processes errors returned by the Osiris platform after a function call.

**Type:** Function

**Function Signature:**
```python
def handleFunctionError(error_code: int, error_message: str) -> None:
    pass
```

**Description:**
- The `handleFunctionError` API processes error codes and error messages returned by the Osiris platform.
- It can be extended to log the error, retry the function call, or take other appropriate actions.

**Input:**
- `error_code`: The error code returned by the Osiris platform. (integer)
- `error_message`: The detailed error message explaining what went wrong. (string)

**Output:**
- None

**Sample Input:**
```python
handleFunctionError(404, "Function not found")
```

**Sample Output:**
```python
Error 404: Function not found.
```

---

### API 8: Track Request Status Command

**Problem:**
Implement the `trackRequestStatus` API in the client SDK, which allows the client to track the status of a function call.

**Type:** Function

**Function Signature:**
```python
def trackRequestStatus(request_id: str) -> str:
    pass
```

**Description:**
- The `trackRequestStatus` API provides real-time updates about the status of a function call (e.g., pending, running, completed).
- The client can use this API to monitor long-running operations or track requests invoked asynchronously.

**Input:**
- `request_id`: The unique ID of the function request to track. (string)

**Output:**
- The current status of the request (e.g., `"pending"`, `"running"`, `"completed"`).

**Sample Input:**
```python
status = trackRequestStatus("request-456")
```

**Sample Output:**
```python
status = "completed"
```

---

### API 9: Cancel Request Command

**Problem:**
Implement the `cancelRequest` API in the client SDK, which allows the client to cancel a pending or running function call.

**Type:** Function

**Function Signature:**
```python
def cancelRequest(request_id: str) -> bool:
    pass
```

**Description:**
- The `cancelRequest` API allows a client to cancel a function invocation that is either pending or running.
- It takes the request ID and attempts to cancel the function call.

**Input:**
- `request_id`: The unique ID of the function request to cancel. (string)

**Output:**
- `True` if the request was successfully canceled, `False` otherwise.

**Sample Input:**
```python
canceled = cancelRequest("request-789")
```

**Sample Output:**
```python
canceled = True
```

---

These specifications provide the core functionality for the Client SDK, allowing client applications to invoke functions, serialize and deserialize data, handle errors, and monitor function executions. Each API is designed to make interaction with the Osiris platform seamless and efficient.

# Team 5: Client SDK Core Functionality
## SPRINT 1
### Trello link:
https://trello.com/invite/b/671e9313531e58561197c45f/ATTI3d945370511e4bb15adf9e00b8dcb3b7037D5AF5/team-5-outsiders
### Technology:
---
- Language: Python
- **_Asyncio_**: For asynchronous programming in Python. APIs like callFunctionAsync and trackRequestStatus will benefit from asyncio to handle non-blocking operations.
- **_JSON_**: For serialization and deserialization tasks, the built-in json library will be essential. serializeArgs and deserializeResponse will use json.dumps() and json.loads() for converting data to and from JSON.
- **_Unittest_**: Python’s unittest library can be used for writing test cases for each API function.
- **_Requests or Aiohttp_**: If your SDK communicates with the Osiris platform over HTTP, the requests library (synchronous) or aiohttp (asynchronous) will be needed. These libraries provide methods to send HTTP requests and handle responses, which may be useful in functions like callFunction, callFunctionAsync, trackRequestStatus, and cancelRequest.

| API    | Function                | Description                                                                                           | Input Parameters                                                                                | Output                                  | Story Points |
|--------|--------------------------|-------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|-----------------------------------------|--------------|
| **1**  | `callFunction`           | Invokes a function deployed on the Osiris platform synchronously.                                     | `function_name`: str, `args`: list                                                               | Result of function execution (any)      | 3 points     |
| **2**  | `callFunctionAsync`      | Invokes a function asynchronously, useful for non-blocking operations.                                | `function_name`: str, `args`: list                                                               | Result of function execution (any)      | 8 points     |
| **3**  | `getFunctionResult`      | Retrieves the result of a previously invoked function using its request ID.                           | `request_id`: str                                                                               | Result of function execution (any)      | 5 points     |
| **4**  | `serializeArgs`          | Serializes function arguments into JSON format for transmission.                                      | `args`: list                                                                                     | Serialized JSON string (str)            | 5 points     |
| **5**  | `deserializeResponse`    | Deserializes JSON response from the Osiris platform back to Python objects.                           | `response`: str                                                                                  | Deserialized response (any)             | 5 points     |
| **6**  | `setTimeout`             | Sets a timeout (in milliseconds) for requests to the Osiris platform.                                 | `timeout`: int                                                                                   | None                                    | 2 points     |
| **7**  | `handleFunctionError`    | Processes errors by handling error codes and messages from the Osiris platform.                       | `error_code`: int, `error_message`: str                                                          | None                                    | 8 points     |
| **8**  | `trackRequestStatus`     | Provides real-time updates on the status of a function call.                                         | `request_id`: str                                                                               | Current status (str)                    | 8 points     |
| **9**  | `cancelRequest`          | Allows the client to cancel a pending or running function invocation.                                 | `request_id`: str                                                                               | True if successfully canceled (bool)    | 3 points     |

---

### Team Assignments:
Justin Abraham:<br>
Alexandra Drzewosz:<br>
Valliammai Janakiraman:<br>
Justin Nguyen:<br>
Joshua Rosillo:<br>
Nirbhav Talloju:
