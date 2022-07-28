# **Export**
- `export` is a built-in command of the bash shell, which is used to mark variables and functions to be passed to child process
- basically, a variable will be included in child process environments without affecting other environments
```shell
export GOPATH = `pwd`
```

# **Source**
- `source` is a shell built-in command which is used to read and execute the content of a file (generally a set of commands), passed as an argument in the current shell script
- if any positional arguments are provided, they become the postional arguments when filename is executed
```shell
source filename [arguments]
source functions.sh
source /apth/to/functions.sh arg1 arg2
```