# **Components**
- `components` let us split the UI into independent, reusable pieces, and think each piece in isolation
- conceptually, `components` are like `JavaScript` functions, they accept arbitrary inputs (called `props`) and return React elements describing what should appear on the screen
- simplest way to define a `component` is to define a JavaScript function:
```javascript
function Welcome(props) {
    return <h1> Hello, {props.name} <\h1>;
}

// ES6 way to define a component
class Welcome extends React.Component {
    render() {
        return <h1> Hello, {props.name} <\h1>;
    }
}
```

# **Props**
- `props` are read-only, whether we declare a `component` as a function or class, it should never modify its own props (should always be declared as `pure` functions)
- `pure` functions do not attempt to change their inputs, and always return the same result for the same inputs:
```javascript
// pure function:
function sum(a, b) {
    return a + b;
}

// impure function:
function withdraw(account, amount) {
    account -= amount;
}
```
- all React `components` must act like pure functions with respect to their props