# **Function types**
```typescript
// declare a variable which has a function type that accepts 2 numbers and returns a number
let add: (x: number, y: number) => number;

// assign a function to 'add' variable
add = function(x: number, y: number) {
    return x+y;
}

// declare a variable and assign a function to a variable
let add: function(a: number, b: number) => number = {
    function (x: number, y: number) {
        return x+y;
    }
}

let add = function (x: number, y: number): number {
    return x+y;
}
```

# **Optional Parameters**
- optional parameters must appear after the required parameters in parameters list
- use `parameter?:type` syntax to make a parameter optional
- use `typeof(parameter) !== 'undefined'` to check if the parameter has been intialized
```typescript
function multiply(a: number, b: number, c?: number): number {

    if (typeof c !== 'undefined') {
        return a * b * c;
    }
    return a * b;
}
```

# **Function Overloading**
```typescript
function addNumbers(a: number, b: number): number {
    return a + b;
}

function addStrings(a: string, b: string): string {
    return a + b;
}

// function overloading
function add(a: number, b: number): number;
function add(a: string, b: string): string;
function add(a: any, b: any): any {
   return a + b;
}
```