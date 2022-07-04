# **Encoding**
- Most widely accepted encoding is `UTF-8`
- `UTF-8` is a flexible encoding that allows single bytes and multi-bytes char to coexist in one sentence or string
- `Go` supports UTF-8 encoding (type rune), not just ASCII, for eg the code below will work fine in `Go` but maybe not other programming languages
```golang
func main() {
    c := rune("世") // this is a multi-byte character
    // in other languages, char oni support single byte characters (oni ASCII)
    fmt.Println(c)
    ftm.Println(len(c)) // prints 4 (the number of bits)
}
```
- data type for `rune` is int32, supports up to 4-bit characters, also takes up 4 bytes of memory
- In `Go` when we are working with strings, the encoding is UTF-8; if individual character (rune), then it will be 4-byte char by default
- using `rune` may not be memory efficient, `string` is more memory efficient when dealing with multiple characters
- if we know we are only using ASCII characters and we want to save as much memory as possible, we can use `byte` (data type is uint8)
```golang
func main() {
    c := byte(65)
    fmt.Println(c)  // prints 'A', 'A' ASCII = 65
}
```