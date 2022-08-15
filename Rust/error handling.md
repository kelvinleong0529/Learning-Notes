# **Error Handling**
```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Problem creating the file: {:?}", e),
            },
            other_error => {
                panic!("Problem opening the file: {:?}", other_error);
            }
        },
    };
}
```
# **Match**
- using `match` works well enough, but it can be a bit verbose and doesn't always communicate intent well
- `unwrap` method is a shortcut method implemented just like the `match` expression
- if `Result` value is `Ok` variant, `unwrap` will return the value inside the `Ok`
- if `Result` is the `Err` variant, `unwrap` will call the `panic!` macro for us
```rust
use std::fs::File;

fn main() {
    let greeting_file = File::open("hello.txt").unwrap();
}
// if we the code above without the "hello.txt" file, we will see the error below:
// thread 'main' panicked at 'called `Result::unwrap()` on an `Err` value: Os {
// code: 2, kind: NotFound, message: "No such file or directory" }',
// src/main.rs:4:49
```
# **Expect**
- we can also use `expect` method to choose the `panic!` error message, it provides good error message that can convey our intent and make tracking down the source of panic easier
```rust
use std::fs::File;

fn main() {
    let greeting_file = File::open("hello.txt")
        .expect("hello.txt should be included in this project");
}
// if we the code above without the "hello.txt" file, we will see the error below:
// thread 'main' panicked at 'hello.txt should be included in this project: Os {
// code: 2, kind: NotFound, message: "No such file or directory" }',
// src/main.rs:5:10
```
# **? Operator**
- `?` placed after a `Result` value is defined to work in almost the same way as the `match` expressions
- if the value of `Result` is an `Ok`, the value inside the `Ok` will get returned from this expression, and the program will continue as usual
- if the value is an `Err`, the `Err` will be returned from the whole function as if we had used the `return` keyword so the error value gets propagated to the calling code
```rust
use std::fs::File;
use std::io;
use std::io::Read;

fn read_username_from_file() -> Result<String, io::Error> {
    let mut username_file = File::open("hello.txt")?;
    // if 'Err' is returned from the above statement
    // immediately break the function and return the 'Err' value
    let mut username = String::new();
    username_file.read_to_string(&mut username)?;
    Ok(username)
}
```