# **GCC**
- `GNU` is an operating system and a collection of software made to be "Unix like" wuthout using Unix
- `GCC` stands for `GNU Compiler Collection`, is a piece of GNU software that includes a compiler with front-ends for multiple languages based on a common core compiler and linker
  
# **MinGW**
- `MinGW` stands for `Minimalist GNU for Windows`, it is essentially a tool set that includes some `GNU` software, including a port of GCC
- it is a copy of `GCC` + other common utilities and libraries used in compiling and linking `C` or `C++` code using the GNU tools
- a collection of `GNU` development tools (GCC, etc.) that have been recompiled to run on Windows, purpose is to let us use GNU development tools to build applications that use the native Windows API

# **Cygwin**
- let us take source code written to use `POSIX APIs`, and build them to run on Windows
- since the applications compiled using `Cygwin` are built to use `POSIX API`, they required users to install the `Cygwin DLL`, which is responsible for handling the applications' POSIX API calls into native Windows API calls

| Field                                   | MinGW | Cygwin |
|-----------------------------------------|-------|--------|
| GNU Development Tools (GCC, etc         | Yes   | Yes    |
| Full Set of POSIX tools                 | no    | yes    |
| Compile native Windows API applications | yes   | yes    |
| Compile POSIX API applications          | no    | yes    |

# **Compiler Specification (Function)**
- `__declspec(dllimport)` specifies that the function is to be imported from a sepearte dll, depending on the CRT static / dynamic linking settings
- `__cdecl` is the calling convention used for a funciton, it tells the compiler how the funciton expects to be called (in which order parameters are pushed on to the stack, if any registers is used for parameters, where is the return value stored, who is responsible for stack cleanup,..)