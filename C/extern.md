# **Prerequisite**
1. `Declaration`: simply declare that a function or variable exists somewhere in the program, but memory is **NOT** allocated for them
- it tells the pgroams what the type it is going to be `(for variables)`, or the arguments, data types, order of these arguments, and return type the case of `function`
2. `Definition`: in addition to everyhting that a declaration does, it also allocates memory for that variable or function
- `definition` is a superset of `declaration`
- a variable or function can be **declared** any number of times, but it can be **defined** only once


# **Extern**
- short name for `external`
- used when a particular files need to access a variable from another file
```C
# include <studio.h>

extern int a; // int var -> declaration + definition
// extern int var -> declaration

int main() {
    printf("%d",a);

    return 0;
}
```
- when we write `extern some_data_type some_variable_name`, no memory is allocated
- `extern` variables tells the compiler, "go outside my scope and you will find the definition of the variable that I declared"
- compiler believes that whatever that `extern` variable said is true and produce no error, `linker` throws an error when it finds no such variable exists
```C
int var;
int main(void) {
    var = 10;
    return 0;
}
// compiles successfully, 'var' is defined globally
```
```C
extern int var;
int main(void) {
    return 0;
}
// compiles successfully, 'var' is declared only, but is never use so no problem arise
```
```C
extern int var;
int main(void) {
    var = 10;
    return 0;
}
// compilation throws an error
// because 'var' is declared but not defined anywhere
// 'var' isn't allocated any memory, and the program tries to change the value of a variables that doesnt exists at all
```
```C
# include "somefile.h"
extern int var;
int main(void) {
    var = 10;
    return 0;
}
// assume that "somefile.h" contains the definition of "var", the program will compile successfully
```
```C
extern int var = 0;
int main(void) {
    var = 10;
    return 0;
}
// "var" is declared and also initialized, memory is allocated, "var" is considered as defined
// compile successfully
```