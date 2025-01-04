### **1. Shared Locks**
- let us read the row or the table that is being locked
- multiple transactions can acquire a shared lock on the same resource and read from it
- no transaction is allowed to update the resource while at least one shared lock is acquired on the resource

### **2. Exclusive Locks**
- locks the row or the table entirely, and let the transaction to update the row in isolation
- only one transaction can acquire an exclusive lock on a certain resource at one point in time
- while exclusive lock is acquired on the resource, other processes that want to acquire the lock on the same resource will have to wait
- once the lock is released, the remaining processes can acquire it and make modifications
- multiple shared locks can be acquired on a resource at one time, but if the resource has a shared lock then another process cannot acquire an exclusive lock on it
- a process cannot acquire shared lock on a resource that is locked by an exclusive lock

### **3. Optimistic Lock**
- a lock that allows other process to continue with the update and changes
- only when the process successfully commits its changes, the other processes are then told there exists a conflict due to which the other process will have to attempt the transaction again

### **4. Pessimistic Lock**
- lock the row as soon as one process attempts to modify it (delete it), and ask other processes to wait before doing anything

# **Problems arise without isolation**
- ACID-compliant databases need to make sure that each transaction is carried out in isolation
- meaning the result of the transaction is only visible after a commit to the database happens
- other processes should not be aware of what's going on with the records while the transaction is carried out

### **1. Dirty Read**
- happens when a transaction is updating a row or a table, and the database let a transaction to read the changes (before it's committed)
- because if first transaction rolls back its changes, the other transaction which reads the row/table has stale data
- happens in concurrent system where multiple transactions are going on in parallel

### **2. Non-repeatable read**
- consecutive read can retrieve different results if we allow another transaction to do updates in between
- if a transaction is querying a row twice, by in between the reads, there is another transaction updating the same row, the reads will give different results

### **3. Phantom read**
- similar to non-repeatable read, only difference is that the other transaction inserts or deletes rows leading to a change in the number of rows retrieved in by the first transaction in its second read
- instead of having inconsistencies in the values of the new row, the number of rows retrieved by the queries will be different

# **Isolation levels**
- database implements different levels of isolation to avoid the problems above
- while locks were supposed to be used for complete isolation of transaction, if they are going to limit other transactions from doing anything while the resource is locked then lock contentions might create a problem
- the solution is to have different levels of isolation

### **1. Read uncommitted**
- lets other transaction read data that was not committed to the database by other transactions
- no isolation is happening here
- if transaction A is performing an update and before it's able to commit, transaction B tries to access the updated data, it will will see the new data

### **2. Read committed**
- let other transaction to only read data that is committed to the database
- only solves dirty read problem mentioned above
- can still cause non-repeatable read and phantom reads because read-committed does not lock rows to ensure they remain unchanged throughout the transaction

### **3. Repeatable read**
- resource is locked throughout the transaction
- if a transaction contains two SELECT queries and in between, if another tries to update the same rows, it would be blocked from doing so
- still not immune to phantom reads
- DEFAULT level of isolation in many database

### **4. Serializable**
- highest level of isolation
- all concurrent transactions "appear" to be executed serially