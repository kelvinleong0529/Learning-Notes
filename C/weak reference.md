# **Weak Reference**
```C
// weakly declared symbol
void foo() __attribute__((weak))

// strongly declared symbol (default)
void foo()
```
1. when a `weak reference` to `foo` is linked in a program, the linker need not find a definition of `foo` anywhere in the linkage, it may remain undefined. If a `strong reference` to `foo` is linked in a program, the linker needs to find a definition of `foo`
2. a linkage may contains at most 1 `strong definition` of `foo` (a definition of `foo` that declares it strongly), otherwise a multiple-definition error results, but it may contain multiple weak definitions of `foo` without error
3. if a linkage contains 1 or more `weak definitions` of `foo` and also a `strong definition`, the linker chooses the strong definition of `foo` without error
4. if a linkage contains just 1 `weak definition` of `foo` and no `strong definition`, inevitably the linker uses the 1 `weak definition`
5. if a linkage contains multiple `weak definitions` of `foo` and no `strong definition`, then the linker choose one of the `weak definition` randomly