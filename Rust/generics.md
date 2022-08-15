# **Generics**
- `generics` is the topic of generalizing types and functionalities to broader case
```rust
// a function to return the largest element from a list (int, char, etc.)
fn get_largest<T: PartialOrd + Copy>(number_list: Vec<T>) -> T {
    // instead of allowing the generic to be any type
    // here we restirct the generic type has to be a type that can be ordered and "copy"
    let mut largest = number_list[0];
    for number in number_list {
        if number > largest {
            largest = number;
        }
    }
    largest
}
```
```rust
struct Point<T,U> {
    x: T,
    y: U,
    // here we define the type for 'x' and 'y' can be of any type (generic)
    // x and y doesnt have to be the same type, for eg: 'x' can be i32, 'y' can be float
}

fn main() {
    let p1 = Point {x:5, y:10};
    let p2 = Point {x:5.0, y:10.0};
    let p3 = Point {x:5, y:10.0};
}
```