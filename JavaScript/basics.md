# **Variables**

| Keyword | Scope          | Hoisting | Can Be Reassigned | Can Be Redeclared |
|---------|----------------|----------|-------------------|-------------------|
| var     | Function scope | Yes      | Yes               | Yes               |
| let     | Block scope    | No       | Yes               | No                |
| const   | Block scope    | No       | No                | No                |
- **var** variabels are **function-scoped**, meaning they recognize functions as having a separate scope
- **let** and **const** are **block-scoped**. This means that a new, local scope is created from any kind of block, including **FUNCTION** blocks, **IF** statements, and **FOR** and **WHILE** loops
```javascript
// Initialize a global variable
var species = "human";
 
function transform() {
  // Initialize a local, function-scoped variable
  var species = "werewolf";
  console.log(species);
}

// Log the global and local variable
console.log(species);
transform();
console.log(species);

OUTPUT:
human
werewolf
human
```
```javascript
var fullMoon = true;

// Initialize a global variable
let species = "human";

if (fullMoon) {
  // Initialize a block-scoped variable
  let species = "werewolf";
  console.log(`It is a full moon. Lupin is currently a ${species}.`);
}

console.log(`It is not a full moon. Lupin is currently a ${species}.`);

OUTPUT:
It is a full moon. Lupin is currently a werewolf.
It is not a full moon. Lupin is currently a human.
```
```javascript
// Use var to initialize a variable
var species = "human";

if (fullMoon) {
  // Attempt to create a new variable in a block
  var species = "werewolf";
  console.log(`It is a full moon. Lupin is currently a ${species}.`);
}

console.log(`It is not a full moon. Lupin is currently a ${species}.`);

OUTPUT:
It is a full moon. Lupin is currently a werewolf.
It is not a full moon. Lupin is currently a werewolf.
```

# **Hoisting**
- Behaviour of JavaScript in which variable and function declarations are moved to the top of their scope
```javascript
// The code we wrote
console.log(x);
var x = 100;

// How JavaScript interpreted it
var x;
console.log(x);
x = 100;
```

# **Closures**
- feature in JavaScript where inner function can access the variables of the enclosing function
- has 3 scope chains:
1. it has access to its own scope — variables defined between its curly brackets
2. it has access to the outer function’s variables
3. it has access to the global variables
```javascript
function outer() {
var b = 10;
var c = 100;
   function inner() {
         var a = 20; 
         console.log("a= " + a + " b= " + b);
         a++;
         b++;
    }
   return inner;
}
var X = outer();  // outer() invoked the first time
var Y = outer();  // outer() invoked the second time
//end of outer() function executions
X(); // X() invoked the first time
X(); // X() invoked the second time
X(); // X() invoked the third time
Y(); // Y() invoked the first time

OUTPUT:
a=20 b=10
a=20 b=11
a=20 b=12
a=20 b=10
```

