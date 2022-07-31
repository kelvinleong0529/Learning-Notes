# **Go Build**
- `go build` is used to compile packages and dependencies that we have defined / used in our project
- when compiling packages, `build` ignores files that end in **_test.go**
- if we specify a single file as argument it treats as a single package, but if the arguments are a list of .go files then all the source should be specifying / pointing to a single package


```golang
go build -ldflags="flag" sourcefile.go
```
- the **flag** above is related to the linker (**ld** stands for linker), this flag is the overall used flag as it inserts **dynamic information** at build time in our binary file
```golang
// main.go
var mainPackageVariable string

func main() {
    fmt.Println("Main Package Variable"=,mainPackageVariable)
}

// sub.go
var subPackageVariable string

func main() {
    fmt.Println("Sub Package Variable=",subPackageVariable)
}
```