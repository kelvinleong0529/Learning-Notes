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

# **Interfaces**
- `interfaces` is a set of signatures, when a `type struct` provides definitions for all the methods in the interface, it is said to implement the interface. `Interfaces` specifies what methods a type should have and the type decides how to implement these methods
```golang

// define the "geometry" basic interface
type geometry interface {
    area() float64
    perim() float64
}

// define "rect" struct
type rect struct {
    width, height float64
}

// define "circle" struct
type circle struct {
    radius float64
}

// to implement an interface, we need to implement all the methods in the interface
// we implement the interface methods for "rect" type
func (r rect) area() float64 {
    return r.width * r.height
}
func (r rect) perim() float64 {
    return 2*r.width + 2*r.height
}

// we implement the interface methods for "circle"
func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}
func (c circle) perim() float64 {
    return math.Pi * 2 * c.radius
}

// if a variable has interface type, we can call methods that are in the named interface, for example:
func measure (g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}

// since "rect" and "circle" both implement the "geometry" interfaces, we can use instances of these structs as argument to "measure()"
func main() {
    r := rect{width: 3, height: 4}
    c := circle{ radius: 5}

    measure(r)
    measure(c)
}
```