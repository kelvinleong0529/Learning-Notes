# **SQLite**
- `SQLite` is a software library that provides a relational database management system
- `lite` in `SQLite` means lightweight in terms of setup, database administration, and required resources
- has the following noticeable features:
1. self-contained
2. serverless
3. zero-configuration
4. transactional

## **Serverless**
- usually RDBMS such as `MySQL`, `PostgreSQL`, etc requires a seperate server process to operate, the application what wants to access the database server use TCP/IP protocol to send and receive requests, which is called `client/server architecture`
![RDBMS client/server architecture](https://www.sqlitetutorial.net/wp-content/uploads/2015/12/RDBMS-Client-Server-Architecture.jpg)
- `SQLite` does not require a server to run, it is integrated with the application that access the databases, it interacts with `SQLite` database read and write directly from the database files stored on disk
![SQLite serverless architecture](https://www.sqlitetutorial.net/wp-content/uploads/2015/12/What-is-SQLite.jpg)

## **Self-Contained**
- `SQLite` requires minimal support from the operating system or external library, makes it usable in any environment especially in embedded devices like iPhones, Android phones, game consoles, handheld media players, etc

## **Zero Configuration**
- because of its `serverless architecture`, we don't need to install `SQLite` before using it
- there is no server process that needs to be configured, started and stopped
- in addtion, it does not need any configuration files

## **Transactional**
- all transactions in `SQLite` are fully ACID-compliant, meaning all queries and changes are Atomic, Consistent, Isolated and Durable
- all changes within a transaction take place completely or not at all even when an unexpected situation like application crash, power failure, or operating system crash occurs

## **Distinctive Features**
- use dynamic types for tables, it means we can store any value in any column, regardless of the data type
- allows a single database connection to access multiple database files simultaneously, brining many nice features suck as joining tables in different datavases or copying data between databases in a single command
- is capable of creating in-memory databases that are very fast to work with