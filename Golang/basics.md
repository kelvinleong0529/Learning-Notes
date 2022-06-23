# **Go Modules**
- Go module keeps track on our code's dependencies, it include the name of the module and the Go version our code supports
- create a Go module using the following command:
```
go mod init kelvin.leong/examples
```

# **Variadic Functions**
- Variadic functions are functions that can be called with multiple arg
```golang
func sum(nums ...int) {
    total := 0
    for _,num := range nums {
        total += num
    }
    fmt.Println(total)
}

func main() {
    sum(1,2)
    sum(1,2,3)

    // if we aldy have multiple args stored in a slice
    // we can apply them to a variadic function using 'func(slice...)'
    nums := []int{1,2,3,4}
    sum(nums...)
}
```

# **Advanced Function**
```golang
func test2 (myFunc func(x int) int) func(string) int{}
// test2 => function where arg is 'another function with int as arg and return int'
// test 2 => return type is a function that takes string as arg and return int
```
```golang
func main() {
    test := func(x int) int {
        return x * -1
    }(8)    // immediately pass '8' as an argument and call the function
    fmt.Println(test) // prints -8
}
```
```golang
func returnFunc(x string) func() {
    // returnFunc returns a reference to a function
    return func() {fmt.Println(x)}
}

func main() {
    returnFunc("Hello World")()
    // we need the 2nd () to call the function returned by 'returnFunc'
    x := returnFunc("goodbye")
    x() // prints "goodbye"
}
```


# **Slice**
- lightweight data structure of variable length sequence for storing homogeneous data, **more convenient, powerful and flexible** than array
- has 3 components:
1. pointer - This is used for pointing to the first element of the array accessible via slice, doesn’t need to be the first element of the array
2. length - This is used for representing the total elements count present in the slice.
3. capacity - This represents the capacity up to which the slice can expand.

![slice](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/001/744/original/slice.png?1637335112)