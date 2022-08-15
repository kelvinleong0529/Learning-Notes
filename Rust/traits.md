# **Traits**
- `traits` allow us to share behaviour across types and facilitates code reuse
- when we want to define a function that can be applied to any type with some required behaviour, we use `traits`
```rust
trait WithName {
    fn new(name: String) -> Self;

    fn get_name(&self) -> &str;

    fn print(&self) {
        println!("My name is {}", self.get_name())
    }
}
```
- `Self` is a special keyword that is only available within type definitions, trait definition, and `impl` blocks
- in `trait` definitions, it refers to the implementing type, in other words, if we were to declare a struct `A` and implement the `WithName` trait for it, then the `Self` type that is returned by the `new` method would be `A`. For a struct `B`, the type would be `B`
- `&self` argument is a syntactic sugar for `self:&Self`, this means that the first argument to a method is an instance of the implementing type. To require a mutable reference to self, use `&mut self`

# **Methods**
- as the `&self` argument in a trait method requires an instance of the implementing 
type, these methods are know as `instance methods`
- trait methods that don't require an instance are called static methods, which are commonly used to instantiate types that implement the trait
- methods can also have `default implementations`, such as `WithName` trait's `print` method, which makes implementing this method optional when implementing the trait, if it's not overridden, the default implementation is used

# **Implementing a trait**
- use the syntax: `impl <trait> for <type>` to implement a trait for the `type` we want
- we will need to implement all the methods that don't have default implementations
```rust
struct Name(String);

impl WithName for Name {
    fn new(name: String) -> Self {
        Name(name)
    }

    fn get_name(&self) -> &str {
        &self.0
    }
}
```

# **Trait bounds, Trait functions**
```rust
use std::fmt::Debug;

fn f(a: &Debug, b: &Debug) {
    todo!()
}

fn g<T: Debug>(a: &T, b: &T) {
    todo!()
}
```
- ignoring the fact that they don't do anything, function `f` will accept any 2 arguments that implement the `Debug` trait, even if they are 2 different types
- function `g` will only accept 2 arguments of the **SAME** type, but that type can be any type that implements `Debug`
```rust
use std::fmt::Debug;

fn dyn_trait(n: u8) -> Box<dyn Debug> {
    todo!()
}

fn impl_trait(n: u8) -> impl Debug {
    todo!()
}
```
- `dyn_trait` function can return any number of types that implements the `Debug` trait and can even return a different type depending on the input argument, known as the `trait object`
- `impl_trait` method can only return a single type that implements the `Debug` trait, in other words, the function will always return the same type

# **Supertraits**
- Rust has a way to specify that a trait is an extension of another trait, giving us something similar to subclassing in other languages
- to implement a new subtrait, we must implement all the required methods on the supertait as well as any required methods on the subtrait
```rust
trait MyDebug : std::fmt::Debug {
    fn my_subtrait_function(&self);
}
```