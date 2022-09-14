# **Redis**
- Redis stores data in the form of key-value pair, it's not good in storing sturctured data like in SQL
- Redis does not run on the disk or stores the information on disk, instead it runs on the working memory, the RAM of our computer. means it's incredibily **FAST**, but it also means **HIGH VOLATILITY** becuase if system crashes we will lose all the info unless we backed them up
- Mostly used for **CACHING**, things that we access a lot, or those that need alot of time to compute
- Redis is to be built on top of a traditional database, sitting in front of **MONGODB**, **POSTGRESQL**, if we have data that need to queried frqeuently, can stored the data in **REDIS** (both in the traditional databases as well)

# **Redis Single-Threaded Model**
- Although `redis` is single-threaded, it can provide concurrency at I/O by using an I/O multiplexing mechanism and an event loop
- `parallelism` has a cost, with the multiple sockets / multiple cores that we can find on modern hardware, synchronization between threads is extremely expensive
- the bottleneck of `redis` is often the **network**, well before the CPU, hence isolated event loops (which require no synchronization) are seens as a good design to build efficient, scalable servers
- `redis` are singled-threaded as they are meant to be designed to prevent any lock contention and thus their memory access is blazing fast (the reason developers do not traditionally notice performance speed advantage in single cores is because they are used to working with slow libraries and slow code)

# **Basic Commands**
1. `SET name kelvin`: create a key-value pair with "name" as the key and "kelvin" as the value
2. `GET name`: returns the value of the key "name"
3. `EXISTS name`: check if the key "name" exists
4. `KEYS *`: get all the keys
5. `SETEX name 10 kelvin`: create the key-value pair that lasts for 10 seconds (SET EXPIRE)
- `GET` only work for strings


# **Array**
1. `LPUSH` friends kelvin: "L" stands for **left**-push, push the value "kelvin" into the **beginning** of an array called "friends"
2. `LRANGE` friends 0 -1: get the elements in the array "friends" starting from index 0:-1 (means all the elements)
3. `RPUSH` friends sally: "R" stands for **right**-push, push the value "kelvin" into the **end** of an array called "friends"
4. `LPOP` friends: pop / remove the **left**-most element in the "friends" array
5. `RPOP` friends: pop / remove the **right**-most element in the "friends" array
```
LPUSH friends kelvin
LPUSH friens john
RPUSH sally
LRANGE friends 0 -1
-----------
1)"john"
2)"kelvin"
3)"sally"
-----------
LPOP friends
-----------
"john"
-----------
RPOP friends
-----------
"sally"
-----------
```

# **Sets**
1. `SADD hobbies` "weight lifting": add the value "weight lifting" into a set called "hobbies"
2. `SREM hobbies` "weight lifiting": remove the value "weight lifting" from a set called "hobbies"
3. `SMEMBERS hobbies`: return all the elements in the set called "hobbies"

# **Hashes**
1. `HSET person name kelvin`: add the key-value pair of "name":"kelvin" into a has object called person
2. `HGETALL person`: get all the key-value pairs in the hash object called "person"
3. `HGET person name`: get the value of the "name" key in the hash object called "person"
4. `HDEL person age`: delete the prpoperty of age in the hash object "person"
5. `HEXISTS person name`: check if the "name" property exists in the hash object called "person"
```
HSET person name kelvin
HSET person age 25
HGET person name
-----------
"25"
-----------
HGETALL person
-----------
1)"name"
2)"kelvin"
3)"age"
4)"25"
-----------
HDEL person name
HGETALL person
-----------
1)"age"
2)"25"
-----------
```

# **Transactions**
## **Running Transactions**
- `MULTI` commands tells Redis to begin a transaction block, any subsequent commands will be queued up until we run an `exec` command, which will execute them
```redis
> multi
> set key_MeaningOfLife 1
> incr key_MeaningOfLife
> incrby key_MeaningOfLife 40
> get key_MeaningOfLife
> exec

---------------------------------------
Output
1) OK
2) (integer) 2
3) (integer) 42
4) "42"
```
## **Cancelling Transactions**
- use the `discard` command to cancel a transaction, and prevents any previously-queued commands from running
```redis
> multi
> set key_A 146
> incrby key_A 10
> discard
-----------------------------------------
Output
1) OK
```

# **Connections Pooling**
- `connection pooling` means that connection are reused rather than created each time when the connection is requested
- to facilitate connection reuse, a memory cache of database connections, called `connection pool`, is maintained by a connection pooling module as a layer
- connection pooling is performed in the background and does not affect how an application is coded
- there are some concerns when using Redis with a multi-threaded environment
- Redis connection instance is single-threaded. If we reuse a single Redis connection between multiple threads, it may not be enough to complete the required tasks in a limited time. If we create a separate Redis connection for a thread it will be overhead for the Redis server.
- We need to have a pool of connections in multi-threaded environments to address these challenges. This allows us to talk to Redis from multiple threads while still getting the benefits of reused connections. The idea is, take the connection from the pool and release it back to the pool once we have done. This pool should be configured once and can be reused many times.
- Basic Configurations:
1. `maxTotal`: This property manages the max number of connections that can be produced at a given time. As Jedis connections cannot be shared across threads, this setting affects the amount of concurrency your application can have when interacting with Redis. Note that each connection does have some memory and CPU cost, so setting this to a very high value may have negative side effects. If not set, the default value is 8, which is reasonably too low for most applications. When choosing a value, consider how many concurrent calls into Redis may possible under heavy load.
2. `maxIdle`: This is the max number of connections that can be idle in the pool without being quickly closed. If not set, the default value is 8. The suggested value for this is same as maxTotal to help avoid unnecessary connection costs when your application has many bursts of load in a short period of time. If a connection is idle for a long time, it will still be evicted until the idle connection count hits minIdle. The minIdle is explained below.
3. `minIdle`: This is the number of connections that are ready for immediate use. They remain in the pool even when the load has decreased. If not set, the default is 0. When choosing a value, consider your steady-state simultaneous requests to Redis. For instance, if your application is calling into Redis from 10 threads simultaneously, then you should set this to at least 10 ( a bit higher to give you some room).
4. `blockWhenExhausted`: This controls behaviour when a thread asks for a connection, but there aren’t any that are free and the pool can’t create more (due to maxTotal configuration). If set to true, the calling thread will block for maxWaitMillis before throwing an exception. The default is true and I recommend it truly for production environments. You could set it to false in testing environments to help you more easily discover what value to use for maxTotal.
5. `maxWaitMillis`: How long to wait in milliseconds if calling JedisPool.getResource() will block. The default is -1, which means block indefinitely.
6. `TestOnBorrow`: Controls whether or not the connection is tested before it is returned from the pool. The default is false. Setting to true may increase resilience to connection blips but may also have a performance cost when taking connections from the pool.