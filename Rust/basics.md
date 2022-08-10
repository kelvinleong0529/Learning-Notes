# **Literals**
- underscores can be inserted in numeric literals to improve readability, `1_000` is the same as `1000`, `0.000_001` is the same as `0.000001`
```rust
fn main() {

    println!("1 + 2 = {}",1u32+2u32);
    // 1u32 means the data type for "1" is unsigned 32

    println!("1 - 2 = {}",1u32-2)
    // this will result in error because of arithmetic overflow
    // unsigned cannot have negative value
}
```

# **Functions**
```rust
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    // Corner case, early return
    if rhs == 0 {
        return false;
    }

    // This is an expression, the `return` keyword is not necessary here
    lhs % rhs == 0
}

// Functions that "don't" return a value, actually return the unit type `()`
fn fizzbuzz(n: u32) -> () {
    if is_divisible_by(n, 15) {
        println!("fizzbuzz");
    } else if is_divisible_by(n, 3) {
        println!("fizz");
    } else if is_divisible_by(n, 5) {
        println!("buzz");
    } else {
        println!("{}", n);
    }
}

// When a function returns `()`, the return type can be omitted from the
// signature
fn fizzbuzz_to(n: u32) {
    for n in 1..=n {
        fizzbuzz(n);
    }
}
```