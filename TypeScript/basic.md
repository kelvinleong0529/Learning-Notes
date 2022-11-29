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

# **Type Assertion**
- a way to tell the compiler the type of a variable to access the intellisense
- this will not change the type of the variable at runtime
```typescript
// allows the function the validate the input parameter
let employeeFunction = (employee:Employee) {
    // ..
}

let message; // TypeScript will assume the type to be any at this point
message = "abc";
let endsWithC = (<string>message).endsWith("C");
let endsWithC = (message as string).endsWith("C")  // explicitly tell TypeScript that message is of type string
```

# **Class**
- adheres to **cohesion** rule in OOP
- everything related should be grouped in a class
```typescript
class Point {
    private x:number;
    private y:number;
    // private fields are not accessible from public / outside of the class
    // by default field are set to be public


    // question mark means the variable is optional
    // user can choose not to pass in constructor value
    constructor(x?:number,y?:number) {
        this.x = x;
        this.y = y;
    }

    // the above constructor is the same as below
    constructor (private _x?:number, private _y?:number)

    draw() {
        // implementation of the draw logic
    }

    // -------------------------------
    // Property Class
    // -------------------------------

    // egt property X function
    // user can access filed "X" like a normal property
    // for eg: let x = point.X
    get x() {
        return this.x
    }

    // set property function
    set x(value) {
        if (value < 0)
            throw new Error("value cannot be less than 0")

        this.x = value
    }
}

let point = new Point(1,2);
point.draw();
```

# **Inferred Typing**
- TypeScript also supports dynamic typing of varaible, which means declaring a variable whithout a type
- compiler will determine the type of variable on the basis of the value assign to it, it will find the first usage of the variable within the code, determine the type to which it has been intially set and then assume the same type for this variable in the rest of the code block