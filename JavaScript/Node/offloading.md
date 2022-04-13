# **Child Process**
- Node.js processes are **single-threaded**, it won't be utilizing the full power of a multi-core CPU
- to take advantage of multi-core systems, **Cluster module** allows us to easily create a cluster of child process that each run on their own single thread to handle the load
- **Cluster module** uses the **fork** method to spawn different proccess that allow back and forward communication
- **Child process** is another module that allows us to run subprocess {using **exec,execFile, spawn**}. These child process are often used to interact with the shell and run code from different languages, often used to run shell scripts and commands
- **SPAWN** method don't use buffer but instead streams, hence there isn't length limit on the stdout
- **DRAWBACKS**: No shared memory between all child process (all data is cloned), and spawning process is not cheap (OS need to allocate resouces for these process)
- Using **Cluster Module** & **Child_Process** module, each child thread spawned is associated with a process
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
## **Worker threads**
- for each worker thread that we create we will also need to create an instance of V8, node engine, but all the worker threads is running under **ONE PROCESS**
- by default the main thread and worker threads do not share the environment variables
- we can send resource limit to worker threads once the worker reach the limit it will just terminate
## **Worker**
- Worker Events:
1. message: worker thread communicate with parent thread
2. exit: worker has stopped
3. error: worker thread throws an uncaught exception
4. online: worker has started executing JS code
```javascript
const { Worker } = require("worker_threads")

// the script that we want the worker thread to execute
const worker = new Worker("./worker.js")

worker.on("message",message => console.log(message))
worker.postMessage("ping")
```

## **Parent**
```javascript
const { parentPort } = require("worker_threads")
parentPort.on("message",message => parentPort.postMessage({pong:message}))
```

```javascript
const { Worker, isMainThread, workerData } = require("worker_threads")

// spawn a new worker thread if it's the main / parent thread
// else just log the workerData out
if (isMainThread) {
    const worker = new Worker(__filename, {workerData: "Hello"})
} else {
    console.log(workerData) // "Hello"
}
```

```javascript
// by default the main thread and worker threads do not share environment variables
const { Worker, isMainThread } = require("worker_threads")

if (isMainThread) {
    const worker = new Worker(__filename)
    worker.on("exit",()=>{
        console.log(process.env.SET_IN_WORKER)  // undefined
    })
} else {
    process.env.SET_IN_WORKER = "foo"
}

// use env: SHARE_ENV to allow the main and worker thread to share the same env
const { Worker, isMainThread } = require("worker_threads")

if (isMainThread) {
    const worker = new Worker(__filename,{env: SHARE_ENV})
    worker.on("exit",()=>{
        console.log(process.env.SET_IN_WORKER)  // foo
    })
} else {
    process.env.SET_IN_WORKER = "foo"
}
```
```javascript
// messageChannel

const { messageChannel } = require("worker_threads")
const { port1,port2 } = new MessageChannel()

port1.on("message",(message)=> console.log(message))
port2.postMessage({foo:"bar"})
```