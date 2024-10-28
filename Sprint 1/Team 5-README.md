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
