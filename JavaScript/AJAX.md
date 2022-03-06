# **Asynchronous JavaScript and XML**

### **Asynchronicity**
- Computer are asynchronous by design
- **Asychronous** means things can happen independently of the main program flow
- Most programs run for a specific time slot and then it stops its execution to let another program continue their execution
- Programming Languages are synchronous by default and some provides a way to manage asynchronicity in the language or through libraries
![alt text](https://www.freecodecamp.org/news/content/images/size/w2000/2021/09/freeCodeCamp-Cover-2.png)

# **JavaScript**
- JavaScript is synchronous by default and is single-threaded
- JavaScript's main job is to respond to user actions, and hence browser provides a set of APIs that handle this kind of functionality (asynchronous)

# **JavaScript Function Execution Stack**
- JavaScript engine maintains a stack data structure called **function execution stack**
- The purpose of the stack is to track the current function in execution
1. When the JavaScript engine invokes a function, it adds it to the stack, and the execution starts.
2. If the currently executed function calls another function, the engine adds the second function to the stack and starts executing it.
3. Once it finishes executing the second function, the engine takes it out from the stack.
4. The control goes back to resume the execution of the first function from the point it left it last time.
5. Once the execution of the first function is over, the engine takes it out of the stack.
6. Continue the same way until there is nothing to put into the stack.
- **Synchronous**: everything that happens inside the function execution stack is sequential
- JavaScript's main thread makes sure that it takes care of everything in the stack before it starts looking into anything elsewhere
![alt text](https://www.freecodecamp.org/news/content/images/size/w1000/2021/09/stack.png)

# **Callbacks**
- Callback -> a function which is to be executed after another function has finished execution
- A callback function executes when an asynchronous operation completes
- The first parameter in any callback function is the error object: **error-first callbacks**
```javascript
fs.readFile('/file.json', (err, data) => {
  if (err) {
    //handle error
    console.log(err)
    return
  }

  //no errors, process data
  console.log(data)
})
```

# **JavaScript Callback Queue**
![alt text](https://www.freecodecamp.org/news/content/images/size/w1000/2021/09/taskQ.png)
- JavaScript maintains a queue of callback functions called **callback queue** or **task queue**
- JavaScript engine keeps executing the functions in the call stack
- It doesn't put the callback function straight into the stack, there is no question of any code waiting for/blocking execution in the stack
- The engine creates a loop to look into the queue periodically to find what it needs to pull from there
- The engine creates a **loop** to look into the queue periodically to find what it needs to pull from there. 
- It pulls a callback function from the queue to the call stack when the stack is empty. 
- Now the callback function executes generally as any other function in the stack. The loop continues. This loop is famously known as the **Event Loop**
```javascript
function f1() {
    console.log('f1');
}

function f2() {
    console.log('f2');
}

function main() {
    console.log('main');
    
    setTimeout(f1, 0);
    
    f2();
}

main();

OUTPUT:
main
f2
f1
```

# **Promise**
Imagine that you’re a top singer, and fans ask day and night for your upcoming song.

To get some relief, you promise to send it to them when it’s published. You give your fans a list. They can fill in their email addresses, so that when the song becomes available, all subscribed parties instantly receive it. And even if something goes very wrong, say, a fire in the studio, so that you can’t publish the song, they will still be notified.

Everyone is happy: you, because the people don’t crowd you anymore, and fans, because they won’t miss the song.

- A “producing code” that does something and takes time. For instance, some code that loads the data over a network. That’s a “singer”.
- A “consuming code” that wants the result of the “producing code” once it’s ready. Many functions may need that result. These are the “fans”.
- A promise is a special JavaScript object that links the “producing code” and the “consuming code” together. In terms of our analogy: this is the “subscription list”. The “producing code” takes whatever time it needs to produce the promised result, and the “promise” makes that result available to all of the subscribed code when it’s ready.
```javascript
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```
- When the executor obtains the result, be it soon or late, doesn’t matter, it should call one of these callbacks:
1. **resolve(value)** — if the job is finished successfully, with result value.
2. **reject(error)** — if an error has occurred, error is the error object.
- The function passed to new Promise is called the executor. The executor runs automatically and attempts to perform a job. When it is finished with the attempt, it calls resolve if it was successful or reject if there was an error.
- The promise object returned by the new Promise constructor has these internal properties:
1. **state** — initially "pending", then changes to either "fulfilled" when resolve is called or "rejected" when reject is called.
2. **result** — initially undefined, then changes to value when resolve(value) called or error when reject(error) is called.
![alt text](https://miro.medium.com/max/875/1*IyTbrwCs9zaC5n-hVLI5LA.png)
- To summarize, the executor should perform a job (usually something that takes time) and then call resolve or reject to change the state of the corresponding promise object.
- The executor should call only one resolve or one reject. Any state change is final. All further calls of resolve and reject are ignored

# **Then**
- The first argument of .then is a function that runs when the promise is resolved, and receives the result.
- The second argument of .then is a function that runs when the promise is rejected, and receives the error
```javascript
promise.then(
  function(result) { /* handle a successful result */ },
  function(error) { /* handle an error */ }
);

eg 1: 
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => resolve("done!"), 1000);
});

// resolve runs the first function in .then
promise.then(
  result => alert(result), // shows "done!" after 1 second
  error => alert(error) // doesn't run
);

eg 2:
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => reject(new Error("Whoops!")), 1000);
});

// reject runs the second function in .then
promise.then(
  result => alert(result), // doesn't run
  error => alert(error) // shows "Error: Whoops!" after 1 second
);
```

# **Catch**
- If we’re interested only in errors, then we can use null as the first argument: **.then(null, errorHandlingFunction)**. Or we can use **.catch(errorHandlingFunction)**
```javascript
let promise = new Promise((resolve, reject) => {
  setTimeout(() => reject(new Error("Whoops!")), 1000);
});

// .catch(f) is the same as promise.then(null, f)
promise.catch(alert); // shows "Error: Whoops!" after 1 second
```

# **Finally**
- Just like there’s a finally clause in a regular try {...} catch {...}, there’s finally in promises
- The call **.finally(f)** is similar to **.then(f, f)** in the sense that f always runs when the promise is settled: be it resolve or reject.
- Finally is a good handler for performing cleanup, e.g. stopping our loading indicators, as they are not needed anymore, no matter what the outcome is
- A finally handler has no arguments. In finally we don’t know whether the promise is successful or not. That’s all right, as our task is usually to perform “general” finalizing procedures
- A finally handler passes through results and errors to the next handler
```javascript
new Promise((resolve, reject) => {
  /* do something that takes time, and then call resolve/reject */
})
  // runs when the promise is settled, doesn't matter successfully or not
  .finally(() => stop loading indicator)
  // so the loading indicator is always stopped before we process the result/error
  .then(result => show result, err => show error)
```

# **Job Queue in JavaScript**
![alt text](https://www.freecodecamp.org/news/content/images/size/w1000/2021/09/JObQ.png)
Every time a promise occurs in the code, the executor function gets into the job queue. The event loop works, as usual, to look into the queues but **gives priority to the job queue items over the callback queue items when the stack is free**.
- Item in the callback queue is called a **macro task**
- Item in the job queue is called a **micro task**
- Job Queue always comes before Callback Queue
- Priority Order: Call Stack > MicroTasks > Callback
```javascript
function f1() {
    console.log('f1');
}

function f2() {
    console.log('f2');
}

function main() {
    console.log('main');
    
    setTimeout(f1, 0);
    
    new Promise((resolve, reject) =>
        resolve('I am a promise')
    ).then(resolve => console.log(resolve))
    
    f2();
}

main();

OUTPUT:
main
f2
I am a promise
f1
```
```javascript
function f1() {
 console.log('f1');
}

function f2() { 
    console.log('f2');
}

function f3() { 
    console.log('f3');
}

function main() {
  console.log('main');

  setTimeout(f1, 50);
  setTimeout(f3, 30);

  new Promise((resolve, reject) =>
    resolve('I am a Promise, right after f1 and f3! Really?')
  ).then(resolve => console.log(resolve));
    
  new Promise((resolve, reject) =>
    resolve('I am a Promise after Promise!')
  ).then(resolve => console.log(resolve));

  f2();
}

main();

OUTPUT:
main
f2
I am a Promise, right after f1 and f3! Really?
I am a Promise after Promise!
f3
f1
```