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

// generic trait
impl<V> Point<V> {
    // this is an 'instance method'
    fn x(&self) -> &V {
        &self.x
    }
}

// concrete trait
impl Point<f64> {
    fn y(&self) -> f64 {
        self.y
    }
}

// 'x' method is available to 'Points' of any type
// 'y' method is available to 'Points' of 'f64' type only

impl<T,U> Point<T,U> {
    // this function takes another 'Point'
    // it returns the current 'Point' x field, and also other 'Point' y field
    fn mix_up<V,W>(self,other: Point<V,W>) -> Point<T,W> {
        Point{
            x: self.x,
            y: other.y,
        }
    }
}

fn main() {
    let p1 = Point { x:5, y: 10.4};
    let p2 = Point { x: "Hello", y: 'c'};
    let p3 = p1.mix_up(p2)
    // p1 = Point <i32, f64>
    // p2 = Point <&str, char>
    // p3 = Point <i32, char>
}

fn main() {
    let p1 = Point {x:5, y:10};
    let p2 = Point {x:5.0, y:10.0};
    let p3 = Point {x:5, y:10.0};
}
```

# **Bounds**
- when working with generics, the type parameters often must use `traits` as `bounds` to stipulate what functionality a type implements
- another effect of bounding is that generic instances are allowed to access the methods of traits specified in the bounds
```rust
// Define a function `printer` that takes a generic type `T` which
// must implement trait `Display`.
fn printer<T: Display>(t: T) {
    println!("{}", t);
}

struct S<T: Display>(T);

// Error! `Vec<T>` does not implement `Display`. This
// specialization will fail.
let s = S(vec![1]);
```
```rust
// A trait which implements the print marker: `{:?}`.
use std::fmt::Debug;

trait HasArea {
    fn area(&self) -> f64;
}

impl HasArea for Rectangle {
    fn area(&self) -> f64 { self.length * self.height }
}

#[derive(Debug)]
struct Rectangle { length: f64, height: f64 }
#[allow(dead_code)]
struct Triangle  { length: f64, height: f64 }

// The generic `T` must implement `Debug`. Regardless
// of the type, this will work properly.
fn print_debug<T: Debug>(t: &T) {
    println!("{:?}", t);
}

// `T` must implement `HasArea`. Any type which meets
// the bound can access `HasArea`'s function `area`.
fn area<T: HasArea>(t: &T) -> f64 { t.area() }

fn main() {
    let rectangle = Rectangle { length: 3.0, height: 4.0 };
    let _triangle = Triangle  { length: 3.0, height: 4.0 };

    print_debug(&rectangle);
    println!("Area: {}", rectangle.area());

    //print_debug(&_triangle);
    //println!("Area: {}", _triangle.area());
}
```