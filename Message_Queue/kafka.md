# **Kafka**
- open source stream-processing software platform that aims to provide a unified, high-throughput, low-latency platform for handling real-time data feeds
- core architectural concept is an immutable log of messages that can be organized into topics for consumption by multiple users or applications; a file system or database commit log keeps a permanent record of all messages so Kafka can replay them to maintain a consistent system state
- stores data durably, in a serialized fashion, it distributes data across a cluster of nodes, providing performance at scale that is resilient to failures

# **What is Kafka used for?**
1. **Log aggregation**.  Kafka provides log or event data as a stream of messages.  It removes any dependency on file details by gathering physical log files from servers and storing them in a central location. Kafka also supports multiple data sources and distributed data consumption.
2. **Stream processing**.  Kafka is valuable in scenarios in which real-time data is collected and processed.  This includes raw data that’s consumed from Kafka topics and then enriched or processed into new Kafka topics for further consumption as part of a multi-step pipeline.
3. **Commit logs**.  Any large-scale distributed system can use Kafka to represent external commit logs. Replicated logs across a Kafka cluster help data recovery when nodes fail.
4. **Clickstream tracking**.  Data from user click stream activities, such as page views, searches, and so on, are published to central topics, with one topic per activity type.

# **Event-driven Architecture**
- `Kafka` recevied and sedns data as events called messages which are organized into topics which are "published" by data producers and "subscribed" to by data consumers
- an `event` has a key, value, timestamp, and optional metadata headers
```kafka
event key: 'Daniel'
event value: 'added an ergonomic keyboard to his wishlist'
event timestamp: 'June 10, 2022, at 5:03 p.m'
```
![Kafka Architecture](https://www.upsolver.com/wp-content/uploads/2022/07/Kafka-cluster-1024x861.png)

# **Kafka Cluster**
- multiple `Kafka` brokers form a `Kafka` cluster, main goal of a cluster is to spread workloads evenly across replicas and partitions
- `Kafka` clsuters can scale without interruption, they manage the persistence and replication of data messages, if one broker fails, other `Kafka` broker step in to offer similar services without data loss or degraded latency

## **Kafka Broker**
- broker is a single `Kafka` server, it receives messages from producers, assign them offsets, and commit the message to disk storage
- offset is a unique integer value that `Kafka` increments and adds to each messages as it's generated
- offsets are critical for maintaining data consistency in the event of a failure or outage, as consumers use offsets to return the last-consumed message after a failure
- brokers respond to partition call requests from consumers and return messages that have been committed to disk
- a single broker operates based on the specific hardware and its functional properties
![kafka Broker](https://www.upsolver.com/wp-content/uploads/2022/07/Offset-writes-1024x624.png)

## **Kafka Controller**
- `Kafka` brokers from a cluster by directly or indirectly sharing information
- in `Kafka` cluster, one broker serves as the `controller`, which is responsible for managing the states of partitions and replicas and for performing administrative tasks such as reassigning partitions and registering handlers to be notified about changes

## **Kafka Partitions**
- in `Kafka`, a topic is split into multiple partitions, where each parition is a discrete log file
- `Kafka` writes records to each partition in append-only fashion, in other words, all of the records belonging to a particular topic are divided and stored in partitions
- `Kafka` distributes the partitions of a particular topic across multiple brokers, this distributed layout improves scalability through parallelism
- `Kafka` also replicates partitions and spreads the replicas across the cluster, which provides robust fault tolerance (if one broker failes other brokers can take over and pick up where the failed machine left off)
- when a new message is written to a topic, `Kafka` adds it to one of the topic's partitions, message with the same key are published to the same partition
- `Kafka` assures that any reader of a given topic/partition always consumes messages in their published sequence

## **Kafka Consumers**
- `consumers` are applications or machines that subscribe to topics and process publish message feeds, they read the messages in the order in which they were generated
- it uses the offset to track which message it has already consumed, it stores the offset of the last consumed message for each partition so that it can stop and restart without losing its place

## **Kafka Producers**
- `producers` are client applications that publish (write) events to `Kafka`
- they distribute data to topics by selecting the appropriate partition within the topic, they allocate messages sequentially to the topic partition
- Typically, the producer distributes messages across all partitions of a topic, but the producer may direct messages to a particular partition in certain instances – for example, to keep related events together in the same partition and in the exact order in which they were sent
- The producer can also use a customized partitioner to map messages to partitions based on specific business logic.  However, the producer should take care to distribute keys roughly evenly across partitions to avoid sending too much traffic to one particular broker, which could threaten performance

## **Kafka Topics**
- `topic` classify messages in `Kafka`, a `topic` is roughly analogous to a database table or folder, and are further subdivided into several partitions
- single topic can be scaled horizontally across various servers to deliver performance well beyond the capabilities of a single server
- `kafka` cluster keeps the partitioned log for each topic
- while a `topic` generally has multiple partitions, there is no assurance of message time-ordering throughout the whole topic - only within a single partition
![Kafka topic](https://www.upsolver.com/wp-content/uploads/2022/07/log_anatomy.png)

# **Kafka APIs**
- `kafka` provides 5 key APIs for management and administrative tasks, and also allow developers to communicate with Kafka programmatically
1. Admin API: enables you to manage and analyze Kafka topics, brokers, Access Control Lists, and other objects.
2. Producer API: enables applications to submit (write) data streams to Kafka cluster topics.
3. Consumer API: enables programs to access (read) data streams from topics in the Kafka cluster.
4. Streams API: provides stream processes that convert a data stream into an output stream.
5. Connect API: creates connections that continuously draw data from a source data system into Kafka or push data from Kafka into a target data system.  (The Connect API is not often needed, as you can instead use pre-built connections without writing any code.)