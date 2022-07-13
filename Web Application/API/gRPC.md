# **gPRC**
- `Remote Procedure Call (RPC)` is an `action-based` paradigm, similar to remotely calling a function from another microservice; it's a type of `inter-process communication (IPC)` protocol build around `Protobufs` to handle messaging between client and server
- gRPC is perfect for intensive and efficient communication as it supports client and server streaming
- it's faster than REST, because it utilizes `HTTP/2` protocol, which offers multiple ways to improve performance:
1. Header compression and reuse to reduce the message size
2. Multiplexing to send multiple requests and receive multiple responses simultaneously over a single TCP connection
3. Persistent TCP connections for multiple sequential requests and responses on a single TCP connection
4. Binary format support such as protocol buffers