# **Type Assertion**
- a way to tell the compiler the type of a variable to access the intellisense
- this will not change the type of the variable at runtime
```typescript
// allows the function the validate the input parameter
let employeeFunction = (employee:Employee) {
    // ..
}

let message; // TypeScript will assume the type to be any at this point
message = "abc";
let endsWithC = (<string>message).endsWith("C");
let endsWithC = (message as string).endsWith("C")  // explicitly tell TypeScript that message is of type string
```

# **Pick Utility Type**
- `Pick` type is a utility type which is used to create a new custom type, based off an already existing one; comes in handy when we have an already existing typem and want to create a new type using only a couple of fields from that type
- opposite of `Omit` type
```typescript
type User = {
    firstName: string,
    lastName: string,
    age: number
}
```
- suppose we have a `User` type that looks like the above, in another part of the code, we want to refer to a `user`, but we know the data only gives the first and last name
- as such, we can't actually use the `User` type as all fields are required, if we want to create a new type based off `User`, we can use `Pick`
```typescript
type User = {
    firstName: string,
    lastName: string,
    age: number
}
type UserName = Pick<User, "firstName" | "lastName">

let user:UserName = {
    firstName: "John",
    lastName: "Doe"
}
```
- `Pick` has 2 arguments, 1st is the `Type` which is the type we want to use, 2nd is a `union type` or list of fields we want to select from the type we are using