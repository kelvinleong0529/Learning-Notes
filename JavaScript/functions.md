# **Type of functions**
## **1. Immediately-Invoked Function Expression (IIFE)**
- a way to execute functions immediately, as soon as they are created
- useful as they don't pollute the global object, and a simple way to iolsate variable declarations
- make JavaScript code maintainable
```javascript
(function() {
  /* */
})()

OR 

function() {
  /* */
}())

OR ARROW FUNCTIONS:
(() => {
  /* */
})()

OR

(() => {
  /* */
}())
```

## **2. Higher-Order Functions**
- function that takes function as argument or return a function of both
- Examples as follow
```javascript
function sayHello(fun) {
  console.log(fun());
}

function sayHello() {
  return function() {
    return "Hello World!";
  }
}
```

## **3. Functional Composition**
- wraps a function inside another function
- but as the problem gets compelx, the code's readability decreases
```javascript
const trim = str => str.trim();
const toLowerCase = str => str.toLowerCase();

// example of functional composition
const result = toLowerCase(trim(input))
```

## **4. Pure Functions**
- a function that guarantee will return the same result if being provided the same parameters
- Cannot used random values, current date / time, read the global state (DOM,files,databases)

# **Currying technique**
- currying is a technique to narrow all function arguments to only 1 input
```javascript
// the following 2 functions are equivalent
function (a) {
  return function(b) {
    return a+b;
  }
}
const add = a => b => a+b;

// the following 2 statements are equivalent
// 1.
add(1)(5)
// 2.
const add1 = add(1)
add1(5)
```