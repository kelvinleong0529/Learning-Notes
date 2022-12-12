# **TypeScript**
- superset of JavaScript
- Strong typing, validates the data type during compile time
- Object-oriented features, such as interfaces
- compile-time errors, catch erros at compile time instead of run-time, easier to debug
- most browser do not understand TypeScript, we will need to compile (transpile) TypeScript to JavaScript
- TypeScript Compiler might generate erros when compiling code, but it still geneartes valid JavScript files
```typescript
var name:string = "John"
var score:number = 1
let a:number;
let b:string;
let c:boolean;
let d:any;
let e:number[];

// TypeScript constants
// initial value for constants is a must
const ColorRed = 0;
const ColorGreen = 1;
const ColorBlue = 2;

enum Color = {Red =0, Green =1, Blue= 2}
let backgroundColor = Color.Red
// the following will result in compiltation error
var num:number = "Hello"
```

# **Inferred Typing**
- TypeScript also supports dynamic typing of varaible, which means declaring a variable whithout a type
- compiler will determine the type of variable on the basis of the value assign to it, it will find the first usage of the variable within the code, determine the type to which it has been intially set and then assume the same type for this variable in the rest of the code block