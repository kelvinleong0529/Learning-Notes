# **Global Object**
- When we write JavaScript the global object is the **window**, but when we write JavaScript in Node **window** is no longer the global object anymore
- Some frequently used methods:
```javascript
setInterval(fun(){},timeInterval)   // execute the funcion every certain interval
clearInterval()                     // clear the interval
setTimeout(fun(){},time)            // execute the function after certain time has passed
__dirname   // variable that can tell us the directory that we are currently in
__filename  // variable that can tell us the directory that we are currently in + file name
```

# **Node Event Emitter**
```javascript
var events = require("events");
var myEmitter = new events.EventEmitter();

// Event Emitter 1
myEmitter.on("someEvent1",function(msg){
    console.log(msg);
})

// the 1st argument is which event to emit, the consective arguments are for the callback functions
myEmitter.emit("someEevent1","Hello from someEvent1") // print "Hello from someEvent1"
```
```javascript
var event = require("events");
var util = require("util");

var Person = function(name) {
    this.name = name;
}

// the 1st argu is the object we want it to inherit something, 2nd is the thing to be inherited
// by this anything created using Person constructor will have custom events attached to it
util.inherits(Person.event.EventEmitter)
```

# **File I/O**
- whenever we use asyn methods, we need to use callback function once the action has completed
## **Reading and Writing Files**
```javascript
var fs = require("fs");

// Below is a synchronous code, it will block any codes after it
// It will first read finish the file first, then only proceed to execute the code after it
var readResult = fs.readFileSync("sample.txt","utf8")
fs.writeFileSync("write.txt",readResult)

// Below is asynchronous code
// the 3rd argument is the callback function
fs.readFile("sample.txt","utf8",function(error, data){
    fs.writeFile("write.txt",data)
})
```
## **Deleting Files and Creating Directory**
```javascript
var fs = require("fs")

// DELETE readme.txt
fs.unlink("readme.txt")

// Creating and Deleting Directories
// Only EMPTY directories can be removed
fs.mkdirSync("stuff")
fs.rmdirSync("stuff")
```

# **Clients and Servers**
- Client and servers have a unique IP address to differentiate them
- When a client wants to communicate with a server, it will first need to open a **SOCKET**, basically is a channel that the information can be sent between the 2 computers, the info sent is structured via different protocols (HTTP, FTP)
- When the protocol has been decided, the info is passed through in the socket between the client and server via TCP, TCP will split the data into packets (smaller chunks of data) and transfer them along the socket
- There can multiple programs running on a server, **PORT** is used to differentiate the incoming requests are meant for which **APPLICATION**
- In request or response data, there is **HEADERS** (contains content-type, status)
```javascript
var http = require("http")

var server = http.createServer(function(request,response){
    response.writeHead(200,{"Content-Type":"text/plain"})
    response.end("Hello World!")
})

server.listen(3000,"127.0.0.1")
```
## **JSON Response**
```javascript
var http = require("http")

var server = http.createServer(function(request,response){
    response.writeHead(200,{"Content-Type":"application/json"})
    var myObj = {
        name: "John",
        age: 28
    }
    response.end(JSON.stringify(myObj))
})

server.listen(3000,"127.0.0.1")
```

# **Buffers**
- temporary storage spot for chunk of data that is being transferred from one place to another
- when buffer is full with data, it is passed down the stream
- transfer small chunks of data at a time

# **Streams**
- Writable Streams: allow node.js to write data to a stream
- Readable Streams: allow node.js to read data from a stream
- Duplex: Can read and Write to a stream
```javascript
var fs = require("fs");

var readStream = fs.createReadStream( __dirname + "/readme.txt","utf8")
var writeStream = fd.createWriteStream( __dirname + "/writeme.txt")

// fires the callback funtion below whenever the read stream receives a chunk of data
// We dont have to wait till the server finsih reading the entire file to proceed
// Can pass the data to user whenver we receive a small chunk of data
readStream.on("data",function(chunk){
    console.log(chunk)
    writeStream.write(chunk)
})
```

# **Pipes**
- pipes in node.js can help us to take data from read stream and pass it into a write stream
- can only **PIPE** from readable stream to a writable stream
- **RESPONSE** is also a writable stream
```javascript
var fs = require("fs");

var readStream = fs.createReadStream( __dirname + "/readme.txt","utf8")
var writeStream = fd.createWriteStream( __dirname + "/writeme.txt")

readStream.pipe(writeStream)

// passing chunk of data to client in server
var http = require("http")

var server = http.createServer(function(request,response){
    response.writeHead(200,{"Content-Type":"text/plain"})
    var readStream = fd.createReadStream( __dirname + "/readme.txt","utf8")
    readStream.pipe(response)
})
```