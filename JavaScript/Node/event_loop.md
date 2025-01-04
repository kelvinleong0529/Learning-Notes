# **Event Loop**
- whenever we run a Node program, a thread is automatically created, and this thread is the only place where the entire codebase is going to get executed
- event loop is a tool that schedule which operations this only thread should be performing at any given point in time
- every iteration of the event loop is called a **tick**
![node.js event loop](https://blog.logrocket.com/wp-content/uploads/2019/07/image1-1.png)

## **1. performChecks**
- check the condition to see if the loop needs to iterate again or not
- node.js program operations can be split into 3 main types, **Peding timer operations, pending OS tasks, pending execution of long running executions**
## **2. Performing a tick**
- Phase 1: Node looks at its inner collection of pending timers and checks which callback functions passed to setTimeout() and setInterval() are ready to be called in case of an expired timer
- Phase 2: Node looks at its inner collection of pending OS tasks and checks which callback functions are ready to be called. An example of this could be the completed retrieval of a file from our machine’s hard drive
- Phase 3: Node pauses its execution waiting for new events to occur. With new events, we include: a new timer completion, a new OS task completion, a new pending operation completion
- Phase 4: Node checks if any function related to pending timers related to the setImmediate() function are ready to be called
- Phase 5: Manage close events, used to clean the state of our application