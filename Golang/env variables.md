# **Basic Env Variables**
1. `GOPATH`: defines the root path of our workspace, stores our code base and all the files that are necessary for our development, and contain the following folders:
- `src/`: location of Go source code (for eg: .go, .c, .g, .s)
- `pkg/`: location of compiled package code
- `bin/`: location of compiled executable programs built by Go
2. `GOOS`: Go Operating System
3. `GOARCH`: Go Architecture
```
eg output:
windows/amd64
linux/mips
```

# **Frequently Used Golang Commands**
- `go-bindata` converts any text of binary file into Go source code, making it the perfect tool for embedding data into Go programs.
- For example, we can use to embed assets such as CSS, JavaScript, and image files into our web application, the result will be a fully stand-alone binary that can deployed just as easily as another Go program
- The file data is optionally gzip compressed before being converted to a raw byte slice.