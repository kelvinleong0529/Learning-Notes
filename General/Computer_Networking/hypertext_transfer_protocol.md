# **HTTP/1.1 vs HTTP/2**
## **1. Binary Data Format**
- HTTP/1.1 messages are transmitted in plaintext, makes request and response easy to format and even read using `packet analysis tool`, but results in increased size due to unnecessary whitespace and inefficient compression
- HTTP/2 encapsulates data using a binary protocol, allows for more compact, mroe easily compressible and less error-prone transmissions

## **2. Persistent TCP Connections**
- In early versions of HTTP, a new TCP connection had to be created for each request and response. HTTP/1.1 introduced persistent connections, allowing multiple requests and responses over a single connection. The problem was that messages were exchanged sequentially, with web servers refusing to accept new requests until previous requests were fulfilled
- HTTP/2 allows multiple simultaneous downloads over a single TCP connection. After a connection is established, clients can send new requests while receiving responses to earlier requests, this reduce the latency in establishing new connections, servers also no longer need to maintain multiple connections to the same clients

## **3. Multiplexing**
- With HTTP/2, multiple resources can be transferred simultaneously, clients no longer need to wait for earlier resources to finish downloading before the next one begins
- Website developers used workarounds such as `domain sharding` to “trick” browsers into opening multiple connections to a single host; however, this led to browsers opening multiple TCP connections. HTTP/2 makes this entire practice obsolete

## **4. Header Compression and Reuse**
- In HTTP/1.1, headers are incompressible and repeated for each request. As the number of requests grows, so does the volume of duplicate header information
- HTTP/2 eliminates redundant headers and compresses the remaining headers to drastically decrease the amount of data repeated during a session

## **5. Server Push**
- Instead of waiting for clients to request resources, servers can now push resources. This allows websites to preemptively send content to users, minimizing wait times.