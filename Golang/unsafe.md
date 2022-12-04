# **Unsafe Pointer**
- `unsafe` contains operations that step around the type safety of `Go` programs
- `unsafe.Pointer` allows us to bypass Go's type system and enbales conversion between arbitrary types and the `uintptr` built-in type
- `unsafe.Pointer(x)`, where `x` is a `memory address`
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

# **uintptr**
- `uintptr` is an integer representation of a memory address
- is generally used to perform indirect arithmetic operations on `unsafe pointers` for unsafe memory access 
- First, `unsafe.Pointer` is converted to `uintptr`, and then arithmetic operation is performed on `uintptr`, finally it's converted back to `unsafe.Pointer`, which now points to a new memory address as a result of the operation
- is also used to store and print the pointer address value, since the type `uintptr` does not reference anything as it's a plain integer, the pointer corresponding to that object can be garbage collected

# **Usage**
## **Incorrect Usage**
```golang
func main() {
    // An array of contiguous uint32 values stored in memory.
    arr := []uint32{1, 2, 3}

    // The number of bytes each uint32 occupies: 4.
    const size = unsafe.Sizeof(uint32(0))

    // Take the initial memory address of the array and begin iteration.
    p := uintptr(unsafe.Pointer(&arr[0]))
    for i := 0; i < len(arr); i++ {
        // Print the integer that resides at the current address and then
        // increment the pointer to the next value in the array.
        fmt.Printf("%d ", (*(*uint32)(unsafe.Pointer(p))))
        p += size
    }
}
```
- the code above is considered `unsafe`, because we store the `uintptr` value in `p` and do not immediately make use of that value, it's possible when a garbage collection occurs, the address (stored in `p` as a `uintptr` inetger) will no longer be valid
- let’s assume this scenario has occurred and that p no longer points at a uint32
- perhaps when we reinterpret p as a pointer, the memory pointed at is now being used to store a user’s authentication credentials or a TLS private key
- we’ve introduced a potential security flaw in our application and could easily leak sensitive material to an attacker through a normal channel such as stdout or an HTTP API’s response body
## **Correct Usage**
```golang

```

# **Unsafe Pointer**
- there are many restrictions from `Go` pointers, they cant participate in arithmetic operations, and for 2 arbitrary pointer types, their values cant be converted to each other
- `unsafe pointer` are powerful, and also dangerous
- `safe pointer` can be explicitly converted to an unsafe pointer, and vice versa