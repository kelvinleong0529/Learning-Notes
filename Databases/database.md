# **Relational Database**
- mariaDB, MySQL, PostgreSQL, SQLite, SQL server, Db2
- each table migh have relation with the other
- table structure has to be defined, and each data must conform to it
- changing table structure isnt straightforward and can lead to loss of data
- good: **Data consisntency**
- bad: **Hard to scale**, **Resource intensive**
- scale vertically, but not horizontally
- vertical scaling is only possible to a certain extend
- **ACID** Compliant: Atomicity, Consistency, Isolation and Durability
1. Atomicity: Ensure all operation within a work unit are complete successfully (either do all or don't do at all)
2. Consistency - Ensure database properly change states upon successfully committed transaction
3. Isolation - ensure transaction to operate independently of and transparent to each other
4. Durability - Ensure that result or effect of a commited transaction presists in the case of a system failure
- **best for**: Most Apps
- **not ideal for**: unstructured data

# **NoSQL Database**
- every item in the database stands on its own
- they are key-value stores
- each item only has 2 fields: unique keys and a value
- for eg: every item has a unique ID as the key and a JSON data for the value part
- we can store the data in multiple servers if 1 single server is not enough to store all the data or handle the queries, then each server (called **partition**) will only be responsible for part of the database
- each **PARTITION** is mirrored accross multiple servers (for fault tolerance)
- NoSQL database use hash function to convert each item's primary key into a shorter key (a fixed number that falls into a fixed range) (called **keyspace**), which determines where to solve new items and where to find them
- it's **SCHEMALESS**, good for data that is constantly evolving
- **bad**: can only retrieve item based on primary keys, eventually consistent (due to copying of data between mirrored databases when inserting new data)
- Cloud providers heavily promotes NoSQL because of it's scalability (AWS=>DynamoDB, GCP=>BigTable, Azure=>CosmosDB)

# **Key-balue Database**
- Example: **REDIS**
- every data has a unqiue key and one value
- **good**: FAST
- **bad**: limited space, no queries (join)

# **Wide Column Database**
- Example: Cassandra, Apache HBASE
- every data has a unique key and value (more than 1 column of value)
- **good**: SCHEMA-LESS
- **bad**: cant join between db
- **best for**: time-series, historical records, high-write & low-read

# **Document Database**
- Example: MongoDB
- data is stored in a document, where each document is a container for key-value pair
- documents are group together according to collection
- unstructured and doesnt require schema
- **good**: SCHEMA-LESS
- **bad**: cant join between db
- **best for**: most apps, games, IOT
- not ideal for **GRAPHS**

# **Graph Database**
- data is represented as nodes, and the relationship between them as edges
- when querying many-to-many relation db, can just declare the edges
- **best for**: Graphs, Knowledge graphs, recommendation engines

# **Search Database**
- when user input a text, the database need to return the most relevant result
- it will analyze all the text in the data, and create an index for the searchable terms
- **best for**: Search Engines, Typeahead

# **Multi-model Database**
- Hybrid, a db management system designed to support multiple data models
- can sotre data as key/value paris, graphs pr documents
- can access data with 1 declarative query language