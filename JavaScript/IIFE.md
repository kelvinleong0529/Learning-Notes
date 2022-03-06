# **Immediately-invoked Function Expression**
- a way to execute functions immediately, as soon as they are created
- useful as they don't pollute the global object, and a simple way to iolsate variable declarations
- make JavaScript code maintainable
```javascript
(function() {
  /* */
})()

OR 

function() {
  /* */
}())

OR ARROW FUNCTIONS:
(() => {
  /* */
})()

OR

(() => {
  /* */
}())
```