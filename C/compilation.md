# **Compilation**
- compilation process in `C` involves 4 steps:
1. Preprocessing
2. Compiling
3. Assembling
4. Linking

## **1. Pre-processing**
- the first step in the compilation process in `C` performed using the pre-processor tool
- all statements starting with the `#` symbol are processed by the pre-processor, and it convert the source code into an intermediate file with no `#` statements
1. Comments Removal: `comments` are removed during the compilation process as they are not of particular use for the machine
2. Macros Expansion: `macros` are some constant values or expressions defined using the `#define` directives, the pre-processor creates an intermediate file where some pre-written assembly level instructions replace the defined instructions or constants
3. File inclusion: file inclusion in `C` is the addition of another file containing some pre-written code into the `C` program during the pre-processing, file inclusion cause the entire content of target file to be added into the source code
4. Conditional Compilation: pre-processor replaces all the conditional directives with some pre-defined assembly code and passes a newly expanded file to the compiler
- `intermediate files` has an extension of `.i`, it is expanded from `C` program containing all the content of header files, macros expansion, and conditional compilation

## **2. Compiling**
- `C` uses a inbuilt compiler software tom convert the intermediate `.i` file into an `assembly file` (with extension of `.s`), which have assembly level instructions (low-level code)
- assembly code is a simple english-type language used to write low-level instructions (mostly in micro-contoller programs)
- the whole program is parsed (for syntax analysis, check if there's any syntax error), and it tells us any `syntax error` or `warnings` present in the source code

## **3. Assembling**
- assembly level code (`.s`) is converted into a machine-understandable code (in binary / hexadecimal form) using an `assembler`
- `assembler` is a pre-written program that takes basic instruction from an assembly code file and converts them into binary / hexadecimal code specific to the machine type known as the object code
- the file generated from `assembling` will have the same name as the assembly file and is known as an `object file` (with `.obj` in DOS and `.o` in UNIX OS)

## **4. Linking**
- process of including the library files into the program, `library files` are some predefined files that contain the definition of the functions in machine language (also called static libraries) which have an extension of `.lib`
- we can assume that there are some statements or instructions written in the `object file` where our OS cannot understand, and we will use the dictionary (`library files`) to find the meaning of these "words", meaning we use `library files` to give meaning to some unknown files from the object files
- the linking process generates an `exectuble file` with an extension of `.exe` in DOS and `.out` in UNIX OS