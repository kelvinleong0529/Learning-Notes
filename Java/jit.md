# ByteCode
1. when we compile Java source code, it's translated into bytecode instead of machine code
2. bytecode is a set of instructions that can be executed by JVM
3. it's platform-independent, meaning the same bytecode can run on any device with a JVM, regardless of the underlying hardware and operating system
4. bytecode has a .class extension
5. JVM interprets or compiles (using JIT compilation) this bytecode into native machine code at runtime
6. the same Java source code can have different performance characteristics on different processor architectures, this is due to the differences in instruction sets, cache size, pipeline structures and other architectural features
7. even within the same processor family, different models can yield different performance for the same Java code, influencing factors include: clock speed, cache size and structure, number of cores, specific optimizations in newer processor generations

# Just-In-Time compilers
1. a component used in runtime environments to optimize the execution of programs by compiling code into native machine code at runtime, rather than ahead of time
2. it translates bytecode into native machine code that processor can execute directly, typically results in faster execution compared to interpreting the bytecode line by line

## Performance Optimization
- can make optimization based on runtime information, such as which methods are frequently called, allowing for efficient machine code

## Dynamic Compilation
- compiles code on the fly, meaning it only compiles the methods that are needed during the program execution
- can reduce the initial startup time of applications compared to ahead-of-time (AOT) compilation
- allows runtime environment to make optimization based on the current state of the program, which might not be possible with static compilation

## Memory Efficiency
- by compiling code as it's needed, JIT can save memory compared to ahead-of-time compilation because it avoids loading and compiling unnecessary code

## Adaptive Optimization
- can adapt to the program's behaviour during execution, perform optimization like inlining frequently called methods, eliminating dead codes, optimizing loops, which can improve performance over time as the program runs