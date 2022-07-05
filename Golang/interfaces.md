# **Structs**
- an easy way to allow user to create their own desired data types
```golang
type Circle struct {
    x float64
    y float64
    r float64
}

type Circle struct {
    x, y, r float64
}

// Initialization
var c Circle
c := new(Circle)
c := Circle{x: 0, y: 0, r: 5}

func circleArea(c Circle) float64 {
    return math.Pi * c.r * c.r
}
```

# **Methods**
- a function with a special reciever argument, typically associated with `struct`
- can de defined for either pointer or value receiver
- `Go` automatically handles the conversion between values and pointers for method calls, but typically we use pointer receiver type to avoid copying on method calls or to allow method to mutate and modify the receiving struct
```golang
func (c Circle) circleArea() float64 {
    return math.Pi * c.r * c.r
}

func (c *Cicrle) circleArea() float64 {
    return math.Pi * c.r * c.r
}
```