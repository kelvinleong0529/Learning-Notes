# **Transactions**
- we can use **ROLLBACK** to erase a mistake, for instance: a user would like to delete a particular row from a table, but he fired a **DELETE** statement without a **WHERE** condition (by mistake), which would delete all records from the table, however he can easily recover from mistakes if the statement is inside a transaction block (by firing the **ROLLBACK** command)
- other concurrent user will not get affected by a transaction unless it gets locked
## **1. BEGIN**
- **BEGIN** keyword is used to start a transaction block
- all SQL statements that follow **BEGIN** will be executed as a ginel transaction unit
- transaction block will end after it reached **COMMIT** or **ROLLBACK** keyword
```sql
BEGIN;
    DELETE FROM TABLE WHERE AGE > 50;
COMMIT;
```
## **2. COMMIT**
- **COMMIT** save changes to the database
## **3. ROLLBACK**
- undoes the changes that were issued in the transaction block before it
```sql
BEGIN;
    DELETE FROM TABLE WHERE GENDER = "MALE";
ROLLBACK;
```
## **4. SAVEPOINT**
- gives user the ability to roll the transaction back to a certain point without rolling back the entire transaction
```sql
BEGIN;
    DELETE FROM TABLE WHERE AGE > 50;
    SAVEPOINT savepoint_1; 
    -- savepoint_1 is the name of the savepoint
    DELETE FROM TABLE WHERE GENDER = "MALE";
    SAVEPOINT savepoint_2;
    DELETE FROM TABLE WHERE COUNTRY = "MALAYSIA";
    RELEASE savepoint_2;
    -- delete savepoint_2
    ROLLBACK TO SAVEPOINT savepoint_1;
    -- return the database status back to savepoint_1
COMMIT;
```