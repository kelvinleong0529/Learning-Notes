# **Horizontal Scaling**
- adding more machines to the pool of resources (AKA scaling out)
- requires breaking a sequential logic into smaller pieces so that they can be executed accross multiple machines
- **Horizontal Scaling** might be a better option for many use-case

# **Vertical Scaling**
- adding more power (eg: CPU, RAM) to an existing machine (AKA scaling UP)
- vertical scaling is easier because the logic doesn't need to be change, it's just running the same code on higher-spec machines

| Aspects          | Horizontal Scaling        | Vertical Scaling |
| ---------------- | ----------- | ------ | 
| Databases        | In a database world, horizontal scaling is usually based on the partitioning of data (each node only contains part of the data).   | In vertical scaling, the data lives on a single node and scaling is done through multi-core, e.g. spreading the load between the CPU and RAM resources of the machine.|
| Downtime	       | In theory, adding more machines to the existing pool means you are not limited to the capacity of a single unit, making it possible to scale with less downtime.    | Vertical scaling is limited to the capacity of one machine, scaling beyond that capacity can involve downtime and has an upper hard limit, i.e. the scale of the hardware on which you are currently running. |
| Concurrency      | Also described as distributed programming, as it involves distributing jobs across machines over the network. Several patterns associated with this model: Master/Worker*, Tuple Spaces, Blackboard, MapReduce.    | Actor model: concurrent programming on multi-core machines is often performed via multi-threading and in-process message passing.|
| Message passing  | In distributed computing, the lack of a shared address space makes data sharing more complex. It also makes the process of sharing, passing or updating data more costly since you have to pass copies of the data. | In a multi-threaded scenario, you can assume the existence of a shared address space, so data sharing and message passing can be done by passing a reference.|
| Examples  | Cassandra, MongoDB, Google Cloud Spanner | MySQL, Amazon RDS |

# **Which to choose?**
- Performance - Scaling out allows you to combine the power of multiple machines into a single virtual machine with the combined power of all of them. This means you’re not limited to the capacity of a single unit. First, however, it’s worth working out if you have enough resources within a single machine to meet your scalability needs.
- Flexibility - If your system is solely designed for scaling up, you are effectively locked into a minimum price set by the hardware you are using. If you want the flexibility to choose the optimal configuration setup at any time to optimize cost and performance, scaling out might be a better option.
- Regularity of Upgrades - Again, flexibility is important here. Building an application as a single large unit will make it more difficult to add or change pieces of code individually without bringing the entire system down. In order to deliver a more continuous upgrade process, it’s easier to decouple your application and horizontally scale.
- Redundancy - Redundancy is the amount of duplicate or extra resources to support the main system. Horizontal scaling offers built-in redundancy in comparison to having only one system in vertical scaling, and thus a single point of failure.
- Geographical Distribution - When you need to spread out an application across geographical regions or data centers in order to reduce geo-latency, comply with regulatory requirements, or handle disaster recovery scenarios, you don’t have the option of putting your application in a single box. You have to distribute it.
- Cost - As more large multi-core machines enter the market at significantly lower price points, consider if there are instances in which your application (or portions of your application) can be usefully packaged in a single box and will meet your performance and scalability goals. This might lead to reduced costs.