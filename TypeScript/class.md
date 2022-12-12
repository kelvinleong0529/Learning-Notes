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