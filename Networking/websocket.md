# **Websocket**
- a communication protocol that use full-duplex channels over a single durable Transmission Control Protocol (TCP) connection
- both server and client can trasmit and receive data simultaneously without being blocked, reducing overhead in comparison to alternatives that use half-duplex communication like HTTP polling
- with less overhead, websockets enable real-time communication and rapid data transferring between web server and web browser or client application
- websocket communication initiates a handshake, which uses the HTTP `Upgrade()` header to change from HTTP protocol to Websocket protocol
- data can be transferred from server without a prior request from the client, allowing messages to be passed back and forth and keeping the connection open until the client or the server kills it, allow two-way-real-time data transfer to take place between the client and server
![Webscoket](https://assets.website-files.com/5ff66329429d880392f6cba2/617a911c0c264f7bfbe7be5f_websocket%20work.png)