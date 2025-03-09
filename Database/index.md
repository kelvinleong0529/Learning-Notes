# **Global Secondary Index**
- in partitioned databases, a regular index (also called local index) is limited to the partition where the data is stored
- a global secondary index (GSI) allows queries to be executed efficiently across all partitions
- assuming we have the following table:
```SQL
CREATE TABLE user(
     id bigint,
     user_id bigint,
     name varchar(10),
     PRIMARY KEY(id)
) PARTITION BY KEY(user_id);
```
- if the following query is executed:
```SQL
SELECT * FROM user where name = 'Alice'
```
- with local index:
  1. the database does not know which partitions contain record with name = 'Alice', it must search all partitions, leading to slow performance
  2. this happens because each partition only knows about its own data, and a local index is limited to its partition

- with GSI:
  1. index is stored separately from the main table and spans all partitions
  2. database knows exactly where "Alice" is stored without scanning every partition
  3. the lookup becomes much faster, just like a regular index in a non-partitioned table

### **How it Works**
- separate storage 
  - database creates a new, separate index table that stores mappings of the GSI column (for the example above is `name`) to the actual data location
- different partitioning 
  - this index table is partitioned by `name` instead of `user_id`
- auto-sync 
  - when new data is added or updated in the main table, GSI is also updated automatically
- fast lookups
  - when we search by `name`, the database looks at the GSI first to find which partition has the data, instead of scanning all partitions

# **Clustered Global Secondary Index (Clustered GSI)**
- a special type of GSI that:
  1. stores a full copy of the main table (instead of just selected columns like a regular GSI)
  2. avoids full partition scans when searching by non-partition keys
  3. avoids the need for additional queries (回表) for fetching full row data
- assuming we have a table that is partitioned by `order_id`, and we create a clustered GSI:
```SQL
CLUSTERED INDEX `cg_i_user`(user_id) PARTITION BY HASH(user_id)
```
- this will create a copy of the original table, partitioned by `user_id` instead of `order_id`
- the entire table (all columns) is stored in `cg_i_user` index
- when searching by `user_id`, we can directly query `cg_i_user` and get the full data, without any full table scan or additional lookups

### Impact
- global secondary indexes is essentially sacrificing some write performance in exchange for a significant improvement in read performance