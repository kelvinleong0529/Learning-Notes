# Data Block
- the smallest unit of data storage in a database
- a fixed-size chunk of space that the database uses to read from and write to the storage medium
- contain the actual data for database tables and indexes
- their size can impact the performance and efficiency of database operations

## What happens to data block if we add a new column to row-wise storage?
- assumption: initially the size of data block == one record
### 1. Data Block Reorganization
- since each data block currently stores exactly one record and the block size matches the record size, adding a new column means each record will now be larger
- it will necessitate a reorganization of the existing data blocks to accommodate the new column

### 2. Rewriting Records
- each existing record will need to be rewritten to include the new column
- the process generally involves:
- a) Allocating New Space: New data blocks with enough space to store the expanded records will be allocated.
- b) Copying Data: Existing data will be copied into the new structure, and the new column will be filled with a default value (NULL or another specified default).
### 3. Impact on Storage
- since the new records are larger, more data blocks will be required to store the same number of records, could lead to increased storage usage
- the old blocks might be marked as free or available for reuse, depending on the database management system's (DBMS) implementation

## Can data block size be dynamic?
- in most relational database management systems (RDBMS), the data block size is not dynamic for a given table
- it is usually fixed for a given storage structure or tablespace
- however, different tablespaces or storage structures within the same database can have different block sizes
### 1. Fixed Block Size per Tablespace
#### a) Tablespace Level Block Size: 
- in many databases, the block size is defined at the tablespace level
- a tablespace is a storage location where the actual data for database tables and indexes is kept
- all tables and indexes within a particular tablespace share the same block size
- for example, in Oracle, when you create a tablespace, you can specify the block size
#### b) Consistent Block Size for Tables in the Same Tablespace: 
- all tables and indexes within a given tablespace use the same block size
- within a specific tablespace, the block size is consistent across all contained objects.
### 2. Different Block Sizes for Different Tablespaces
#### a) Multiple Tablespaces with Different Block Sizes: 
- a database can have multiple tablespaces, each with a different block size
- this allows you to optimize storage and I/O performance for different types of workloads
- for example, a tablespace for small, frequently accessed tables might use a smaller block size, while a tablespace for large, sequentially accessed tables might use a larger block size.
### 3. Implications of Fixed Block Size
#### a) Efficiency and Performance: 
- the fixed block size within a tablespace can impact performance
- a block size too small might lead to inefficiency with large rows (requiring multiple blocks per row), while a block size too large might lead to wasted space (with many partially filled blocks).