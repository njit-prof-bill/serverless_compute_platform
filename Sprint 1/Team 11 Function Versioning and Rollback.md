Here are the specifications for **Team 11: Function Versioning and Rollback**, written in the same LeetCode-style format. These APIs are focused on version management for functions in the Osiris platform, including creating new versions, listing versions, and rolling back to previous versions.

---

### API 1: Create New Function Version Command

**Problem:**
Implement the `createFunctionVersion` API, which creates a new version of a function in the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def createFunctionVersion(function_name: str, code: str, version: str) -> bool:
    pass
```

**Description:**
- The `createFunctionVersion` API creates a new version of an existing function, storing the new version along with its code in the system.
- The function name and version number must be unique.

**Input:**
- `function_name`: The name of the function to version. (string)
- `code`: The source code for the new version. (string)
- `version`: The version number (e.g., `"2.0"`). (string)

**Output:**
- `True` if the new version is successfully created, `False` otherwise.

**Sample Input:**
```python
response = createFunctionVersion("addNumbers", "def add(a, b): return a + b", "2.0")
```

**Sample Output:**
```python
response = True
```

---

### API 2: Get Function Version Details Command

**Problem:**
Implement the `getFunctionVersionDetails` API, which retrieves detailed information about a specific version of a function.

**Type:** Function

**Function Signature:**
```python
def getFunctionVersionDetails(function_name: str, version: str) -> dict:
    pass
```

**Description:**
- The `getFunctionVersionDetails` API retrieves information about a specific version of a function, including the code and runtime environment.

**Input:**
- `function_name`: The name of the function. (string)
- `version`: The version number of the function. (string)

**Output:**
- A dictionary containing the version details (e.g., `function_name`, `code`, `runtime`, `version`).

**Sample Input:**
```python
details = getFunctionVersionDetails("addNumbers", "1.0")
```

**Sample Output:**
```python
details = {
    "function_name": "addNumbers",
    "code": "def add(a, b): return a + b",
    "runtime": "Python 3.8",
    "version": "1.0"
}
```

---

### API 3: List Function Versions Command

**Problem:**
Implement the `listFunctionVersions` API, which retrieves a list of all versions for a specific function.

**Type:** Function

**Function Signature:**
```python
def listFunctionVersions(function_name: str) -> list:
    pass
```

**Description:**
- The `listFunctionVersions` API retrieves all the available versions for a given function, including version numbers and their creation dates.

**Input:**
- `function_name`: The name of the function. (string)

**Output:**
- A list of versions, with each entry containing the version number and creation date.

**Sample Input:**
```python
versions = listFunctionVersions("addNumbers")
```

**Sample Output:**
```python
versions = [
    {"version": "1.0", "created_at": "2024-10-01"},
    {"version": "2.0", "created_at": "2024-10-20"}
]
```

---

### API 4: Set Active Function Version Command

**Problem:**
Implement the `setActiveFunctionVersion` API, which sets a specific version of a function as the active one on the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def setActiveFunctionVersion(function_name: str, version: str) -> bool:
    pass
```

**Description:**
- The `setActiveFunctionVersion` API sets a specific version of a function as the active version, making it the default version that gets invoked by users.

**Input:**
- `function_name`: The name of the function. (string)
- `version`: The version to set as active. (string)

**Output:**
- `True` if the active version is successfully set, `False` otherwise.

**Sample Input:**
```python
response = setActiveFunctionVersion("addNumbers", "2.0")
```

**Sample Output:**
```python
response = True
```

---

### API 5: Get Active Function Version Command

**Problem:**
Implement the `getActiveFunctionVersion` API, which retrieves the currently active version of a function.

**Type:** Function

**Function Signature:**
```python
def getActiveFunctionVersion(function_name: str) -> str:
    pass
```

**Description:**
- The `getActiveFunctionVersion` API retrieves the version number of the currently active version for the given function.

**Input:**
- `function_name`: The name of the function. (string)

**Output:**
- The currently active version number of the function. (string)

**Sample Input:**
```python
active_version = getActiveFunctionVersion("addNumbers")
```

**Sample Output:**
```python
active_version = "2.0"
```

---

### API 6: Rollback Function to Previous Version Command

**Problem:**
Implement the `rollbackToPreviousVersion` API, which rolls back a function to its previous version, making it the active one.

**Type:** Function

**Function Signature:**
```python
def rollbackToPreviousVersion(function_name: str) -> bool:
    pass
```

**Description:**
- The `rollbackToPreviousVersion` API automatically rolls back a function to its immediate previous version.
- The previous version is set as the new active version.

**Input:**
- `function_name`: The name of the function. (string)

**Output:**
- `True` if the rollback is successful, `False` otherwise.

**Sample Input:**
```python
response = rollbackToPreviousVersion("addNumbers")
```

**Sample Output:**
```python
response = True
```

---

### API 7: Compare Function Versions Command

**Problem:**
Implement the `compareFunctionVersions` API, which compares two versions of a function and highlights the differences in code.

**Type:** Function

**Function Signature:**
```python
def compareFunctionVersions(function_name: str, version1: str, version2: str) -> dict:
    pass
```

**Description:**
- The `compareFunctionVersions` API compares the source code of two versions of a function and returns the differences.
- It highlights changes between the two versions.

**Input:**
- `function_name`: The name of the function. (string)
- `version1`: The first version to compare. (string)
- `version2`: The second version to compare. (string)

**Output:**
- A dictionary containing the differences between the two versions' code.

**Sample Input:**
```python
diff = compareFunctionVersions("addNumbers", "1.0", "2.0")
```

**Sample Output:**
```python
diff = {
    "changes": [
        {"line": 2, "old": "return a + b", "new": "return a - b"}
    ]
}
```

---

### API 8: Delete Function Version Command

**Problem:**
Implement the `deleteFunctionVersion` API, which deletes a specific version of a function from the Osiris platform.

**Type:** Function

**Function Signature:**
```python
def deleteFunctionVersion(function_name: str, version: str) -> bool:
    pass
```

**Description:**
- The `deleteFunctionVersion` API deletes a specific version of a function from the platform, removing its code and metadata.
- It ensures that the version is no longer available for invocation.

**Input:**
- `function_name`: The name of the function. (string)
- `version`: The version to delete. (string)

**Output:**
- `True` if the version is successfully deleted, `False` otherwise.

**Sample Input:**
```python
response = deleteFunctionVersion("addNumbers", "1.0")
```

**Sample Output:**
```python
response = True
```

---

### API 9: Archive Function Version Command

**Problem:**
Implement the `archiveFunctionVersion` API, which archives a function version to keep it inactive but accessible for future reference.

**Type:** Function

**Function Signature:**
```python
def archiveFunctionVersion(function_name: str, version: str) -> bool:
    pass
```

**Description:**
- The `archiveFunctionVersion` API archives a specific version of a function, making it unavailable for use but still accessible in the system for reference or future rollback.

**Input:**
- `function_name`: The name of the function. (string)
- `version`: The version to archive. (string)

**Output:**
- `True` if the version is successfully archived, `False` otherwise.

**Sample Input:**
```python
response = archiveFunctionVersion("addNumbers", "1.0")
```

**Sample Output:**
```python
response = True
```

---

### API 10: Restore Archived Function Version Command

**Problem:**
Implement the `restoreArchivedVersion` API, which restores an archived version of a function, making it available again.

**Type:** Function

**Function Signature:**
```python
def restoreArchivedVersion(function_name: str, version: str) -> bool:
    pass
```

**Description:

**
- The `restoreArchivedVersion` API restores an archived function version and makes it available for use again.
- The restored version can be set as the active version if desired.

**Input:**
- `function_name`: The name of the function. (string)
- `version`: The archived version to restore. (string)

**Output:**
- `True` if the version is successfully restored, `False` otherwise.

**Sample Input:**
```python
response = restoreArchivedVersion("addNumbers", "1.0")
```

**Sample Output:**
```python
response = True
```

---

These specifications handle the versioning and rollback functionality of functions on the Osiris platform. This allows developers to create, manage, and compare different versions of functions, as well as roll back to previous versions if needed.