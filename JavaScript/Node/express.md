# **Express**
- Easy and flexible routing system
- Integrates with many templating engines
- Contains a middleware framework

```javascript
var express = require("express")
var app = express()

app.get("/",funciton(request,response){
    // how to send a file as a response
    response.sendFile(__dirname + "/hello.html")
})
```