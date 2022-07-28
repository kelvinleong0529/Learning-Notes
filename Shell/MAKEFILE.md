# **MAKEFILE**
- `MAKEFILE` is a text file that contains the recipe for building a program (often use to compile final executable binary files from source code, which can then be installed using `make install`)
- we can use the `make` command to run or update a task when certain files are updated, and this `make` command requires a `MAKEFILE`
```MAKEFILE
say_hello:
    echo "Hello World"
# say_hello behaves like a function name (called 'target')
# 'prerequisites' or 'dependencies' follows after the target
# echo "Hello World" is called the 'recipe'
# 'target', 'prerequisites' and 'recipes' together make a 'rule'
```
```MAKEFILE
all: hello  
hello: main.o function1.o function2.o  
    g++ main.o function1.o function2.o -o hello  
main.o: main.cpp  
    g++ -c main.cpp  
function1.o: function1.cpp  
    g++ -c function1.cpp  
function2.o: function2.cpp  
    g++ -c function2.cpp  
clean:  
    rm -rf *o hello  
```