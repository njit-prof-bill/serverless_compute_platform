### Technical Description of Osiris Functions

#### Overview

Osiris is a scalable, serverless compute platform that is cloud-agnostic, designed to simplify backend development and eliminate vendor lock-in. Osiris functions are similar to AWS Lambda or Azure Serverless functions but offer a more flexible and developer-friendly approach. This document outlines how Osiris functions are defined, deployed, and executed within the platform.

#### Function Definition

Osiris functions are defined like regular functions in the developer's chosen programming language. Unlike other serverless platforms that require proprietary function signatures (e.g., AWS Lambda's `lambda_handler`), Osiris functions are written with standard function names and parameters, returning values directly upon completion.

**Example Function Definition (Python):**
```python
def add_numbers(a, b):
    return a + b
```

**Example Function Definition (JavaScript):**
```javascript
function addNumbers(a, b) {
    return a + b;
}
```

#### Function Registration and Deployment

When a function is deployed to Osiris, it is registered with the platform's gateway/controller. This registration process includes:
1. The function's name.
2. Expected parameters.
3. Metadata necessary for routing and execution.

The gateway/controller maintains a registry of all deployed functions and their states.

#### Calling Functions

To invoke an Osiris function, the calling side utilizes the Osiris SDK. Due to the nature of different programming languages, it is not feasible to entirely mimic native function-call syntax. Instead, the SDK requires the function name as the first argument, followed by the parameters.

**Example Function Call (Python with Osiris SDK):**
```python
response = osiris.call_function('add_numbers', 3, 5)
```

**Example Function Call (JavaScript with Osiris SDK):**
```javascript
osiris.callFunction('addNumbers', 3, 5)
  .then(response => console.log(response))
  .catch(error => console.error(error));
```

#### SDK Operations

1. **Function Lookup:** The SDK uses the provided function name to look up the corresponding function in the Osiris registry.
2. **Argument Serialization:** The arguments are serialized into JSON format.
3. **API Call:** The SDK makes a RESTful API call (potentially using GraphQL or gRPC) to the Osiris gateway/controller, passing the serialized arguments.

#### Gateway/Controller Operations

1. **Request Handling:** The gateway/controller receives the API call, deserializes the arguments, and identifies the target function.
2. **Routing:** The gateway/controller routes the request to the appropriate server running the function. If no instance is available, it decides whether to queue the request, start a new instance, or both.
3. **State Monitoring:** The gateway/controller monitors the running state of all functions, managing instances based on demand. It queues requests when necessary and performs cold starts for new instances.
4. **Load Management:** It also shuts down instances that are idle to optimize resource usage.

#### Function Execution on Server

1. **Request Reception:** The server hosting the function has an Osiris client that receives the request from the gateway/controller.
2. **Argument Deserialization:** The Osiris client deserializes the JSON arguments.
3. **Function Invocation:** The function is called with the deserialized arguments.
4. **Response Serialization:** The function’s return value is serialized into JSON format.
5. **Response Delivery:** The Osiris client sends the serialized response back to the gateway/controller.

#### Response Handling

1. **Response Reception:** The gateway/controller receives the response from the server.
2. **Response Serialization:** The response is serialized and sent back to the SDK.
3. **SDK Response Handling:** The SDK deserializes the response and provides it to the calling code.

### Summary

The Osiris platform enables developers to write backend functions in their preferred programming language without conforming to proprietary signatures. The platform uses an SDK on the calling side to handle function invocation, serialization, and API calls. The gateway/controller manages routing, state monitoring, load balancing, and scaling. This approach ensures a seamless, cloud-agnostic serverless experience, abstracting away infrastructure complexities and focusing on developer productivity.