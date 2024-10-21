Here are the specifications for **Team 12: Index Ledger Core Implementation**, written in the same LeetCode-style format. These APIs manage the core functionality of the index ledger in the Osiris platform, including recording, updating, querying, and auditing transactions.

---

### API 1: Record Transaction Command

**Problem:**
Implement the `recordTransaction` API, which records a new transaction in the ledger.

**Type:** Function

**Function Signature:**
```python
def recordTransaction(transaction_id: str, sender: str, receiver: str, amount: float, timestamp: str) -> bool:
    pass
```

**Description:**
- The `recordTransaction` API records a new transaction in the ledger with a unique transaction ID, sender, receiver, amount, and timestamp.
- The function returns `True` if the transaction is successfully recorded, `False` otherwise.

**Input:**
- `transaction_id`: The unique identifier for the transaction. (string)
- `sender`: The account initiating the transaction. (string)
- `receiver`: The account receiving the transaction. (string)
- `amount`: The amount of the transaction. (float)
- `timestamp`: The date and time of the transaction in ISO 8601 format (e.g., `"2024-10-20T12:00:00Z"`). (string)

**Output:**
- `True` if the transaction is successfully recorded, `False` otherwise.

**Sample Input:**
```python
response = recordTransaction("txn-123", "user1", "user2", 100.0, "2024-10-20T12:00:00Z")
```

**Sample Output:**
```python
response = True
```

---

### API 2: Update Transaction Command

**Problem:**
Implement the `updateTransaction` API, which updates the details of an existing transaction in the ledger.

**Type:** Function

**Function Signature:**
```python
def updateTransaction(transaction_id: str, sender: str = None, receiver: str = None, amount: float = None) -> bool:
    pass
```

**Description:**
- The `updateTransaction` API updates the sender, receiver, or amount of an existing transaction based on the `transaction_id`.
- Any field not provided in the input will remain unchanged.

**Input:**
- `transaction_id`: The unique identifier for the transaction to be updated. (string)
- `sender`: The updated sender account (optional). (string)
- `receiver`: The updated receiver account (optional). (string)
- `amount`: The updated amount (optional). (float)

**Output:**
- `True` if the transaction is successfully updated, `False` otherwise.

**Sample Input:**
```python
response = updateTransaction("txn-123", amount=120.0)
```

**Sample Output:**
```python
response = True
```

---

### API 3: Get Transaction Details Command

**Problem:**
Implement the `getTransactionDetails` API, which retrieves detailed information about a specific transaction in the ledger.

**Type:** Function

**Function Signature:**
```python
def getTransactionDetails(transaction_id: str) -> dict:
    pass
```

**Description:**
- The `getTransactionDetails` API retrieves the details of a transaction based on its `transaction_id`, including sender, receiver, amount, and timestamp.

**Input:**
- `transaction_id`: The unique identifier for the transaction. (string)

**Output:**
- A dictionary containing the transaction details (e.g., `transaction_id`, `sender`, `receiver`, `amount`, `timestamp`).

**Sample Input:**
```python
details = getTransactionDetails("txn-123")
```

**Sample Output:**
```python
details = {
    "transaction_id": "txn-123",
    "sender": "user1",
    "receiver": "user2",
    "amount": 120.0,
    "timestamp": "2024-10-20T12:00:00Z"
}
```

---

### API 4: List Transactions Command

**Problem:**
Implement the `listTransactions` API, which retrieves a list of all transactions stored in the ledger.

**Type:** Function

**Function Signature:**
```python
def listTransactions(limit: int = 100) -> list:
    pass
```

**Description:**
- The `listTransactions` API retrieves a list of transactions, with an optional limit on the number of transactions to return.
- Each transaction in the list includes its `transaction_id`, `sender`, `receiver`, `amount`, and `timestamp`.

**Input:**
- `limit`: The maximum number of transactions to retrieve (default is 100). (integer)

**Output:**
- A list of transactions, with each entry containing the transaction details.

**Sample Input:**
```python
transactions = listTransactions(limit=10)
```

**Sample Output:**
```python
transactions = [
    {"transaction_id": "txn-123", "sender": "user1", "receiver": "user2", "amount": 120.0, "timestamp": "2024-10-20T12:00:00Z"},
    {"transaction_id": "txn-124", "sender": "user2", "receiver": "user3", "amount": 50.0, "timestamp": "2024-10-20T12:10:00Z"}
]
```

---

### API 5: Delete Transaction Command

**Problem:**
Implement the `deleteTransaction` API, which removes a transaction from the ledger based on its `transaction_id`.

**Type:** Function

**Function Signature:**
```python
def deleteTransaction(transaction_id: str) -> bool:
    pass
```

**Description:**
- The `deleteTransaction` API removes a transaction from the ledger permanently.
- The function returns `True` if the transaction is successfully deleted, `False` otherwise.

**Input:**
- `transaction_id`: The unique identifier for the transaction to be deleted. (string)

**Output:**
- `True` if the transaction is successfully deleted, `False` otherwise.

**Sample Input:**
```python
response = deleteTransaction("txn-123")
```

**Sample Output:**
```python
response = True
```

---

### API 6: Audit Ledger Command

**Problem:**
Implement the `auditLedger` API, which audits the ledger for discrepancies or invalid entries and generates a report.

**Type:** Function

**Function Signature:**
```python
def auditLedger() -> dict:
    pass
```

**Description:**
- The `auditLedger` API audits the entire ledger for inconsistencies, such as invalid transactions or discrepancies in amounts.
- It returns a report of any found issues or an empty result if no issues are detected.

**Input:**
- None

**Output:**
- A dictionary containing the audit results, including any discrepancies found in the ledger.

**Sample Input:**
```python
audit_report = auditLedger()
```

**Sample Output:**
```python
audit_report = {
    "discrepancies_found": 0,
    "issues": []
}
```

---

### API 7: Search Transactions by User Command

**Problem:**
Implement the `searchTransactionsByUser` API, which retrieves all transactions where a specific user is either the sender or receiver.

**Type:** Function

**Function Signature:**
```python
def searchTransactionsByUser(user_id: str) -> list:
    pass
```

**Description:**
- The `searchTransactionsByUser` API retrieves all transactions where the specified user is either the sender or the receiver.
- Each transaction includes the `transaction_id`, `sender`, `receiver`, `amount`, and `timestamp`.

**Input:**
- `user_id`: The user ID to search for (either as sender or receiver). (string)

**Output:**
- A list of transactions involving the specified user.

**Sample Input:**
```python
transactions = searchTransactionsByUser("user1")
```

**Sample Output:**
```python
transactions = [
    {"transaction_id": "txn-123", "sender": "user1", "receiver": "user2", "amount": 120.0, "timestamp": "2024-10-20T12:00:00Z"},
    {"transaction_id": "txn-125", "sender": "user1", "receiver": "user3", "amount": 30.0, "timestamp": "2024-10-20T13:00:00Z"}
]
```

---

### API 8: Get Account Balance Command

**Problem:**
Implement the `getAccountBalance` API, which retrieves the current balance of a user based on their transactions in the ledger.

**Type:** Function

**Function Signature:**
```python
def getAccountBalance(user_id: str) -> float:
    pass
```

**Description:**
- The `getAccountBalance` API calculates the total balance for a user by summing all incoming transactions and subtracting outgoing transactions.
- It returns the calculated balance as a floating-point number.

**Input:**
- `user_id`: The user ID for which to calculate the balance. (string)

**Output:**
- The current balance of the user. (float)

**Sample Input:**
```python
balance = getAccountBalance("user1")
```

**Sample Output:**
```python
balance = 300.0
```

---

### API 9: Calculate Total Ledger Value Command

**Problem:**
Implement the `calculateTotalLedgerValue` API, which calculates the total value of all transactions recorded in the ledger.

**Type:** Function

**Function Signature:**
```python
def calculateTotalLedgerValue() -> float:
    pass
```

**Description:

**
- The `calculateTotalLedgerValue` API calculates the sum of all transaction amounts recorded in the ledger.
- It returns the total value of all transactions as a floating-point number.

**Input:**
- None

**Output:**
- The total value of all transactions in the ledger. (float)

**Sample Input:**
```python
total_value = calculateTotalLedgerValue()
```

**Sample Output:**
```python
total_value = 50000.0
```

---

### API 10: Verify Transaction Integrity Command

**Problem:**
Implement the `verifyTransactionIntegrity` API, which checks the integrity of a specific transaction in the ledger by ensuring that it has not been altered.

**Type:** Function

**Function Signature:**
```python
def verifyTransactionIntegrity(transaction_id: str) -> bool:
    pass
```

**Description:**
- The `verifyTransactionIntegrity` API verifies that a specific transaction has not been tampered with or altered after being recorded.
- It returns `True` if the transaction's integrity is intact, `False` if any discrepancies are detected.

**Input:**
- `transaction_id`: The unique identifier for the transaction to verify. (string)

**Output:**
- `True` if the transaction's integrity is verified, `False` otherwise.

**Sample Input:**
```python
response = verifyTransactionIntegrity("txn-123")
```

**Sample Output:**
```python
response = True
```

---

These specifications handle the core operations of an index ledger in the Osiris platform, including recording, updating, querying, auditing, and verifying transactions. This allows for secure and transparent management of all transactions in the ledger.