# **Go Module**
- `Go module` is Go's new dependency management system, a module is a collection of Go packages that are released together and stored in a directory with a `go.mod` file at its root
- `go.mod` file defines the module's path, which is also the import path used while importing package that are part of this module
- all `import paths` are relative to the **module's path**
```golang
go mod init example/user/hello
```

# **Packages**
- `packages` is a collection of source files in the same directory that are compiled together. Functions, types, variables, constants defined in one source file are visible to all other source files within the same package
- use `go get` command to download 3rd party packages from remote repo
```golang
go get -u github.com/jinzhu/gorm
// fetches 'gorm' package from Github and adds it as a dependency to our go.mod file
```