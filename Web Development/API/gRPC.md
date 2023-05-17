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

# **Protocol Buffer Data Format**
- `protocol buffers` are essentialy data format, like JSON, XML
- the main advantage of `protocol buffers` is that it's a lot smaller compared to the likes of XML or even JSON
- Imagine we have a person, who's data we wanted to represent in XML, JSON and protocol buffer data format:
### **1. XML**
```xml
<person>
  <name>Elliot</name>
  <age>24</age>
</person>
```
### **2. JSON**
```json
{
  "name": "Elliot",
  "age": 24
}
```
### **2. Protocol Buffer Data Format**
```
[10 6 69 108 108 105 111 116 16 24]
```
- if we look closely at the above wire encoded output, we may see that starting from position 2, the name `elliot` is spelled out, `e=69`, `l=108` and so on