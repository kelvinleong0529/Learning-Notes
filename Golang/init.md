# **Go init function**
- `init()` function in `Go` provides us a way to set up some form of state on the initial startup of our program
- `init()` function is more preferential when compared to having explicitly call our own setup functions
```golang
package main

func init() {
    fmt.Println("This will get called on main initialization")
}

func main() {
    fmt.Println("Inside Go main function")
}

// Output
This will get called on main initialization
My Wonderful Go Program
```