# **RPC**
- `Remote Procedure Call (RPC)` is a software communication protocol that one program can use to request a service from a program located in another computer on a network without having to understand the network's detail
- `RPC` is used to call other processes on the remote systems like a local system, a procedure call is sometimes known as a `function call` or `subroutine call`
- `RPC` uses the `client-server` model, the requesting program is a client, and the service-providing program is the server
- like local procedure call, `RPC` is a synchronous operation requiring the requesting program to be suspended until the results of the remote procudure are returned; however the use of lightweight processes or `threads` that share the same address space enables multiple `RPCs` to be performed concurrently
- `Interface Definition Language (IDL)` is a specification language used to describe a software component's `application programming interface (API)`, is commonly used in `RPC` software; `IDL` provides a bridge between the machines at either end of the link that may be using different operating systems and computer languages
- `RPC` is perfect for intensive and efficient communication as it supports client and server streaming
- it's faster than REST, because it utilizes `HTTP/2` protocol, which offers multiple ways to improve performance:
1. Header compression and reuse to reduce the message size
2. Multiplexing to send multiple requests and receive multiple responses simultaneously over a single TCP connection
3. Persistent TCP connections for multiple sequential requests and responses on a single TCP connection
4. Binary format support such as protocol buffers