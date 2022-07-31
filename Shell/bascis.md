# **Export**
- `export` is a built-in command of the bash shell, which is used to mark variables and functions to be passed to child process
- when under a shell and we launch some shell script, our shell will fork a new shell (sub-shell) that will execute the commands of the sub-shell
- When a program is invoked it's given an array of strings called the `environment` (in the form of name-value pairs)
- If the vakue of a parameter in the environment is modified, it replaces the old value and the new value becomes part of the environment
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