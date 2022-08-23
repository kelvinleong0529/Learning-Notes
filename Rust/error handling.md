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
// if we compile the code above without the "hello.txt" file, we will see the error below:
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
// if we compile the code above without the "hello.txt" file, we will see the error below:
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

# **Option**
- sometimes it's desirable to catch the failure of some parts of a program instead of calling `panic`, this can be accomplished using the `Option` enum
- `Option<T>` enum has 2 variants:
1. `None`, to indicate failure or lack of value
2. `Some(value)`, a tuple struct that wraps a `value` with type `T`

```rust
// An integer division that doesn't `panic!`
fn checked_division(dividend: i32, divisor: i32) -> Option<i32> {
    if divisor == 0 {
        // Failure is represented as the `None` variant
        None
    } else {
        // Result is wrapped in a `Some` variant
        Some(dividend / divisor)
    }
}

// This function handles a division that may not succeed
fn try_division(dividend: i32, divisor: i32) {
    // `Option` values can be pattern matched, just like other enums
    match checked_division(dividend, divisor) {
        None => println!("{} / {} failed!", dividend, divisor),
        Some(quotient) => {
            println!("{} / {} = {}", dividend, divisor, quotient)
        },
    }
}

fn main() {
    try_division(4, 2);
    try_division(1, 0);

    // Binding `None` to a variable needs to be type annotated
    let none: Option<i32> = None;
    let _equivalent_none = None::<i32>;

    let optional_float = Some(0f32);

    // Unwrapping a `Some` variant will extract the value wrapped.
    println!("{:?} unwraps to {:?}", optional_float, optional_float.unwrap());

    // Unwrapping a `None` variant will `panic!`
    println!("{:?} unwraps to {:?}", none, none.unwrap());
}
```