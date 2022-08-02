# **Libraries**
- on virtually on Operating Systems have 2 types of libraries, `static library(.lib)` and `dynamic library(.dll)`
- main difference is that static libraries are linked to the executable at compile time, whereas dynamic linked libraries are not linked until run-time.

# **Static Libraries**
- we dont normally see static libraries on our computer, because static library is usually embedded directly inside of a module (EXE or DLL)
- static library cannot be changed once it is compiled within EXE

# **Dynamic Link Libraries (DLL)**
- DLL files are like EXEs but they are not directly executable, they are Microsoft implementation of shared libraries
- DLL are stand-alone files
- DLL contains functions, classes, variables, UIs and resources (such as icons, images, files...) that an EXE, or other DLL uses
- DLL can be changed at any time and is only loaded at runtime when an EXE explicitly loads the DLL, it can also be updated individually without updating the EXE itself
- a program loads a DLL at startup, via the `WIN32 API library`, or when it is a dependency of another DLL. Program uses the `GetProcAddress` to load a function or `LoadResource` to load a resource
- Check [MSDN](https://docs.microsoft.com/en-us/cpp/build/dlls-in-visual-cpp?redirectedfrom=MSDN&view=msvc-170) for more information
- DLL files cannot be opened by end-users, they can only opened by their associated application, which usually happens when the application starts up
- a single DLL file can run multiple programs, so multiple programs could potentially be comprised in a DLL hijacking attack
- usually ends with `.dll, .drv, .drov, .exe` extension

# **DLL Hijacking**
- a method of injecting malicious code into an application by exploiting the way some Windows applications search and load DLL
- Only Microsoft OS are suspectible to DLL hijacks
- by replacing a required DLL file with an infected version and placing it within the search parameters of an app, the infected file will be called upon when the application loads, acitiving it's malicious operations
- if applications that are automatically loaded upon startup are compromised with a tainted DLL file, cybercriminals will be granted access to the infected computer whenver it loads
- **Hence, it is extremely dangerous to release an application together with it's DLL file**