Here are the specifications for **Team 10: Function Library Core Management**, written in the same LeetCode-style format. These APIs manage the lifecycle, organization, and versioning of functions within the Osiris platform's function library.

---

### API 1: Add Function to Library Command

**Problem:**
Implement the `addFunctionToLibrary` API, which adds a new function to the function library on the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def addFunctionToLibrary(function_name: str, code: str, runtime: str, version: str = "1.0") -> bool:
    pass
```

**Description:**
- The `addFunctionToLibrary` API adds a new function to the function library.
- It accepts the function’s name, code, runtime environment, and an optional version number. The default version is `"1.0"`.
- The function returns `True` if the function is successfully added to the library, `False` otherwise.

**Input:**
- `function_name`: The name of the function to be added. (string)
- `code`: The source code of the function. (string)
- `runtime`: The runtime environment for the function (e.g., Python 3.8, Node.js). (string)
- `version`: The version of the function (default is `"1.0"`). (string)

**Output:**
- `True` if the function is successfully added to the library, `False` otherwise.

**Sample Input:**
```python
response = addFunctionToLibrary("addNumbers", "def add(a, b): return a + b", "Python 3.8")
```

**Sample Output:**
```python
response = True
```

---

### API 2: Update Function in Library Command

**Problem:**
Implement the `updateFunctionInLibrary` API, which updates an existing function in the function library.

**Type:** Function

**Function Signature:**
```python
def updateFunctionInLibrary(function_name: str, code: str, version: str) -> bool:
    pass
```

**Description:**
- The `updateFunctionInLibrary` API updates the code and version of an existing function in the library.
- It requires the function name, new code, and a new version number.

**Input:**
- `function_name`: The name of the function to update. (string)
- `code`: The updated source code for the function. (string)
- `version`: The new version of the function (e.g., `"1.1"`). (string)

**Output:**
- `True` if the function is successfully updated, `False` otherwise.

**Sample Input:**
```python
response = updateFunctionInLibrary("addNumbers", "def add(a, b): return a - b", "1.1")
```

**Sample Output:**
```python
response = True
```

---

### API 3: Remove Function from Library Command

**Problem:**
Implement the `removeFunctionFromLibrary` API, which removes a function from the function library.

**Type:** Function

**Function Signature:**
```python
def removeFunctionFromLibrary(function_name: str) -> bool:
    pass
```

**Description:**
- The `removeFunctionFromLibrary` API removes a function from the library based on its name.
- The function returns `True` if the function is successfully removed, `False` otherwise.

**Input:**
- `function_name`: The name of the function to be removed. (string)

**Output:**
- `True` if the function is successfully removed, `False` otherwise.

**Sample Input:**
```python
response = removeFunctionFromLibrary("addNumbers")
```

**Sample Output:**
```python
response = True
```

---

### API 4: List Functions in Library Command

**Problem:**
Implement the `listFunctionsInLibrary` API, which retrieves a list of all functions currently stored in the function library.

**Type:** Function

**Function Signature:**
```python
def listFunctionsInLibrary() -> list:
    pass
```

**Description:**
- The `listFunctionsInLibrary` API returns a list of all functions currently stored in the library.
- Each entry includes the function name, runtime, and the latest version.

**Input:**
- None

**Output:**
- A list of functions in the library, with each entry containing the function name, runtime, and version.

**Sample Input:**
```python
functions = listFunctionsInLibrary()
```

**Sample Output:**
```python
functions = [
    {"function_name": "addNumbers", "runtime": "Python 3.8", "version": "1.1"},
    {"function_name": "multiplyNumbers", "runtime": "Node.js", "version": "1.0"}
]
```

---

### API 5: Get Function Details Command

**Problem:**
Implement the `getFunctionDetails` API, which retrieves detailed information about a specific function in the library.

**Type:** Function

**Function Signature:**
```python
def getFunctionDetails(function_name: str) -> dict:
    pass
```

**Description:**
- The `getFunctionDetails` API retrieves detailed information about a function, including its code, runtime, and version history.

**Input:**
- `function_name`: The name of the function to retrieve details for. (string)

**Output:**
- A dictionary containing the function's details (e.g., `function_name`, `code`, `runtime`, `version`).

**Sample Input:**
```python
details = getFunctionDetails("addNumbers")
```

**Sample Output:**
```python
details = {
    "function_name": "addNumbers",
    "code": "def add(a, b): return a - b",
    "runtime": "Python 3.8",
    "version": "1.1"
}
```

---

### API 6: Rollback Function Version Command

**Problem:**
Implement the `rollbackFunctionVersion` API, which rolls back a function to a previous version in the library.

**Type:** Function

**Function Signature:**
```python
def rollbackFunctionVersion(function_name: str, target_version: str) -> bool:
    pass
```

**Description:**
- The `rollbackFunctionVersion` API reverts a function to a specified earlier version.
- The function accepts the function name and the target version to roll back to.

**Input:**
- `function_name`: The name of the function to roll back. (string)
- `target_version`: The version to roll back to. (string)

**Output:**
- `True` if the rollback is successful, `False` otherwise.

**Sample Input:**
```python
response = rollbackFunctionVersion("addNumbers", "1.0")
```

**Sample Output:**
```python
response = True
```

---

### API 7: Search Function by Runtime Command

**Problem:**
Implement the `searchFunctionByRuntime` API, which allows searching for functions in the library based on their runtime environment.

**Type:** Function

**Function Signature:**
```python
def searchFunctionByRuntime(runtime: str) -> list:
    pass
```

**Description:**
- The `searchFunctionByRuntime` API retrieves a list of functions that use a specified runtime environment (e.g., `Python 3.8`, `Node.js`).

**Input:**
- `runtime`: The runtime environment to search for (e.g., Python, Node.js). (string)

**Output:**
- A list of functions that use the specified runtime.

**Sample Input:**
```python
functions = searchFunctionByRuntime("Python 3.8")
```

**Sample Output:**
```python
functions = [
    {"function_name": "addNumbers", "version": "1.1"},
    {"function_name": "subtractNumbers", "version": "1.0"}
]
```

---

### API 8: Publish Function Command

**Problem:**
Implement the `publishFunction` API, which marks a function as "published" and ready for use on the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def publishFunction(function_name: str) -> bool:
    pass
```

**Description:**
- The `publishFunction` API publishes a function from the library, making it available for use on the platform.
- Once published, the function can be invoked by other developers or systems.

**Input:**
- `function_name`: The name of the function to publish. (string)

**Output:**
- `True` if the function is successfully published, `False` otherwise.

**Sample Input:**
```python
response = publishFunction("addNumbers")
```

**Sample Output:**
```python
response = True
```

---

### API 9: Unpublish Function Command

**Problem:**
Implement the `unpublishFunction` API, which removes a function from the "published" state, making it unavailable for invocation.

**Type:** Function

**Function Signature:**
```python
def unpublishFunction(function_name: str) -> bool:
    pass
```

**Description:**
- The `unpublishFunction` API removes a function from the "published" state, meaning it cannot be invoked by other systems or developers until it is published again.

**Input:**
- `function_name`: The name of the function to unpublish. (string)

**Output:**
- `True` if the function is successfully unpublished, `False` otherwise.

**Sample Input:**
```python
response = unpublishFunction("addNumbers")
```

**Sample Output:**
```python
response = True
```

---

### API 10: Archive Function Command

**

Problem:**
Implement the `archiveFunction` API, which archives a function in the library to remove it from active use but keep it for future reference.

**Type:** Function

**Function Signature:**
```python
def archiveFunction(function_name: str) -> bool:
    pass
```

**Description:**
- The `archiveFunction` API archives a function, which removes it from active usage but retains its information and code in the library for future reference.
- Archived functions can be restored later if needed.

**Input:**
- `function_name`: The name of the function to archive. (string)

**Output:**
- `True` if the function is successfully archived, `False` otherwise.

**Sample Input:**
```python
response = archiveFunction("addNumbers")
```

**Sample Output:**
```python
response = True
```

---

These specifications handle the lifecycle of functions in the Osiris platform's function library, including adding, updating, removing, versioning, and publishing functions. This ensures that functions can be managed effectively and deployed across the platform as needed.