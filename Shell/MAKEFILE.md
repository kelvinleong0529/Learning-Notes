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

# **Function**
- we can define custom functions in Makefile via the following syntax:
```MAKEFILE
define generate_file
    sed 's/{NAME}/$(1)/' greetings.tmpl > $(2).txt
    # here we pass the first parameter $(1) to the {NAME} variable inside 'greetings.tmpl'
    # 'sed' stands for 'stream editor' and it can perform lots of functions on file like searching, find and replace, insertion and deletion
endef

all:
$(call generate_file,John Doe, 101)
$(call generate_file,Peter Pan, 102)

# Contents of greeting.tmpl:
Hello {NAME}
```
- when we run `make`, it produces the following files:
```
// 101.txt
Hello John Doe

// 102.txt
Hello Peter Pan
```
- inside the function the first parameter becomes $(1), the second becomes $(2) and so on...
- we execute / call our custom function via the following syntax:
```MAKEFILE
$(call <name_of_the_function>[,<param>][,<param>][...])
```

# **.PHONY**
- by default, `MAKEFILE` **targets** are "file targets" - they are used to build file from other files, `MAKE <testing>` interprets the rule to mean **execute such-and-such recipe to create the file named `testing`**
- However, sometimes we might need `MAKEFILE` to run commands that do not represent physical files in the file system, some of the good example for this are the common targets such as `clean` and `all`
- But sometimes we might potentially have a file name `clean` in our main directory, and in such case `make` will be confused because by default the `clean` target would be associated with this file, and `make clean` will do nothing because  
- `PHONY` can explicitly tell `make` that there are not associated with files, with the following syntax:
```MAKEFILE
.PHONY: clean

clean:
    rm -rf *.0

# another way to declare phony targets is to use :: without prerequisites
clean::
    ...
distclean::
    ...
```
- with the syntax above, `MAKE` will run as expected even though we have a file name `clean`
- some common `make` targets that are often **phony** are `all, install, clean, distclean, TAGS, info, check`