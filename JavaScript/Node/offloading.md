# **Child Process**
- Node.js processes are **single-threaded**, it won't be utilizing the full power of a multi-core CPU
- to take advantage of multi-core systems, **Cluster module** allows us to easily create a cluster of child process that each run on their own single thread to handle the load
- **Cluster module** uses the **fork** method to spawn different proccess that allow back and forward communication
- **Child process** is another module that allows us to run subprocess {using **exec,execFile, spawn**}. These child process are often used to interact with the shell and run code from different languages, often used to run shell scripts and commands
- **SPAWN** method don't use buffer but instead streams, hence there isn't length limit on the stdout
## **Cluster Module**
```javascript
const cluster = require("cluster")
const express = require("express")
const os = require("os")
const app = express()

const numCpu = os.cpus().length

cluster.worker.kill() // to terminate a forked process

// the master process will fork new process only, wont be listening to request
// only forked worker process will be listening to request
if (cluster.isMaster) {
    for(let i =0; i< numCpu; i++>) {
        cluster.fork()
    }
    cluster.on("exit",(worker,code,signal)=>{
        // whenever a forked worker process dies, fork another new process
        // this can ensure our app has 0 downtime
        console.log(`worker ${worker.process.pid} died`)
        cluster.fork()
    })
} else {
    app.listen(3000,() => {
        console.log(`server ${process.id} @ http://localhost:3000`)
    })
}
```
## **Child_Process Module**
```javascript
const { exec } = require("child_process")

exec('pwd',(error,stdout,stderror)=>{
    if(error) {
        console.log(`error: ${error.message}`)
    }
    if(stderror) {
        console.log(`stderror: ${stderror}`)
    }
    console.log(`stdout: ${stdout}`)
})
```
```javascript
const { execFile } = require("child_process")

// the first argument has to be executable file
// for eg: if we want to run Python script inside node.js
// we will need to feed the python executable file path as the 1st arg
// then the .py script that we wish to execute as the 2nd arg
execFile('./file.exe',(error,stdout,stderror)=>{
    if(error) {
        console.log(`error: ${error.message}`)
    }
    if(stderror) {
        console.log(`stderror: ${stderror}`)
    }
    console.log(`stdout: ${stdout}`)
})
```

```javascript
const { spawn } = require("child_process")

// the following command wouldnt work with exec and execFile
const child = spawn("find",["/"])

child.stdout.on("data",(data)=>{
    console.log(`stdout:${data}`)
})

child.stderr.on("data",(data)=>{
    console.log(`stderr:${data}`)
})

child.on("error",(error)=>{
    console.log(`error:${error}`)
})

child.on("exit",(code,signal)=>{
    if (code) console.log(`Process exit with code: ${code}`)
    if (signal) console.log(`Process exit with signal: ${signal}`)
    console.log(`Spawn child process finsih!`)
})
```