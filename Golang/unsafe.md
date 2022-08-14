# **Unsafe Pointer**
- `unsafe` contains operations that step around the type safety of `Go` programs
- `unsafe.Pointer` allows us to bypass Go's type system and enbales conversion between arbitrary types and the `uintptr` built-in type
- there are 4 operations available for `unsafe.Pointer` that cannot be performed with other types:
1. a pointer value of any type can be converted to an `unsafe.Pointer`
2. an `unsafe.Pointer` can be converted to a pointer value of any type
3. A `uintptr` can be converted to `unsafe.Pointer`
4. an `unsafe.Pointer` can be converted to a `uintptr`
```golang
func Float64bits(f float) uint64 {
    return *(*uint64)(unsafe.Pointer(&f))
}
// converts a float to uint64
```
1. `&f` takes a pointer to the `float64` value stored in `f`
2. `unsafe.Pointer(&f)` converts the `*float64` to an `unsafe.Pointer`
3. `(*uint64)(unsafe.Pointer(&f))` converts the `unsafe.Pointer` to `*uint64`
4. `*(*uint64)(unsafe.Pointer(&f))` dereferences the `*uint64`, yielding a `uint64` value