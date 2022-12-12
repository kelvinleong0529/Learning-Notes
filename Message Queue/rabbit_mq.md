# **Rabbit MQ**
- `RabbitMQ` is a message broker that enables services and applications to communicate with each other, it supports multiple messaging protocols like `AMQP (Advanced Message Queueing Protocol)`, and `MQTT (MQ Telemetry Transport)`, `STOMP (Simple Text Orientated Messaging Protocol)` and a few more
- provides powerful powerful routing capabilities that are fluid and can adapt to the ever-changing needs of the user and servuces
- recevies messages from producers and pushes them to queues depending on the rules defined by the `RabbitMQ exchange type`
- can handle a wide range of protocols and can be utilized to meet high-scale and high-availability requirements in both distributed and federated environments
- its server is written in `Erlang` and is clustered and failover-ready

# **Rabbit MQ Exchanges**
- in `Rabbit MQ`, a producer never delivers a message directly to a message queue, instead it makes use of `exchange` as a routing middleman
- `RabbitMQ` exchange determines if the message is routed one queue, several queues, or is simply discarded
- `RabbitMQ` exchanges are message routing agents configured by the virtual host in `RabbitMQ`, and is in charge of routing messages to different queues using header attributes, bindings and routing keys
- is used a `routing mediator`, to receive messages from producers and push them to message queues according to rules provided `RabbitMQ` exchange type
- each exchange type uses a seperate set of parameters and bindings to route the message, client get the option to create their own exchange or use the default exchange
![RabbitMQ Exchanges](https://miro.medium.com/max/1400/0*gFwb04MsfqtVB5bY.png)

# **Rabbit MQ Message Cycle**
1. an exchange message is sent out by the producer
2. after communication has been received, the exchange is responsible for sending it, it uses information from the `RabbitMQ` exchange type to direct the message to the relevant queues and exchanges
3. the queue receives the message and stores it until the consumer receives it
4. finally, the consumer handles the message
![RabbitMQ Message Cycle](https://lh5.googleusercontent.com/r0vO5bbEBvW6NyYESRbhRNGC7-h1dLwm1iBOCCrBvunmqLSAEPkhMPBPUCREGC-mzkwejLqNGALNdwpDlwvNb8bkyDvkLfSTzMRYfaQXKRY8Dvj1MLTTEtZ992OuaAfVTHets2NZ)

## **1. Direct Exchange**
- uses a `message routing key` to transport messages to queues
- routing key is a message attribute that the producer adds to the message header, which is used to determine how the message should be routed
- a message is delivered to the queue with the binding key that exactly matches the message's routing key
- direct exchange's default exchange is `amq.direct`, which AMQP brokers must offer for communication
![Direct Exchange](https://lh4.googleusercontent.com/yOraFrUZeQVNWc2nean2p-66nvfue7SatpC0Ob8W2MD22P1hNTHIc5wR4EZwr_xx3sTGnUc5PBUOLL5y6QykCBO_pwWQSYJ2SL6NSHbWz5XxZGEgPzFZcPLIQu_ivOTsKyP_UdOZ)
- as shown in the figure above, queue A (create_pdf_queue) is tied to a direct exchange (pdf_events) with the binding key “pdf_create”
- When a new message arrives at the direct exchange with the routing key “pdf_create”, the exchange sends it to the queue where the binding key = routing key; which is queue A in this example (create_pdf_queue)

## **Topic Exchange**
- sends messages to queues depending on `wildcard matches between the routing key and the queue binding's routing pattern`
- message are routed to one or more queues based on a pattern that matches a message routing key, a list of words seperated by a period must be used as the routing key
- in `topic exchange`, consumers indicate which topics are of interest to them, consumer establish a queue and binds it to the exchange using a certain routing pattern
- The routing patterns may include an asterisk (`*`) to match a word in a specified position of the routing key (for example, a routing pattern of “`agreements.*.*.b.*`” only matches routing keys with “agreements” as the first word and “b” as the fourth word). A pound symbol (“#”) denotes a match of zero or more words
- all message with a routing key that matches the routing pattern are routed to the queue, where they will remain until the consumer consumes them
- `amq.topic` is the default topic exchange that AMQP brokers must provide for message exchange
![Topic Exchange](https://lh3.googleusercontent.com/NxL1v4ajiS0AQV3LEfUMOZunSbBxT-GCefbhAsVTZpjzgKXsPSg5PBXdl2vzSD3_FYujyJyFkayIr8xxItqtXuOEbB9GTTTxliEvqS5ozkQimKAkrgx9zk66utu25lMTXxknltjQ)