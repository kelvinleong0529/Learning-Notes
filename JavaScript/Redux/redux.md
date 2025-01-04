# **What is Redux**
- JavaScript state management library, similar to **FLUX**, **MOBX**
- In reality when some part of the data on the website changes (could be due to user or network requests), the other parts might need to get updated as well, and we might need to write a lot codes to keep everything in sync
- in **REDUX**, instead of scateering application state in various parts of the UI, we store the application state inside a central repository (ssingle Javascript object called the **STORE**, like a database for front-end,a dn is stored on the client-side)
- different pieces of UI no longer maintain their own state, instead they get what they need from the **STORE** to update whatever data they need
- **REDUX** also makes it easy to understand how the data chanes in our application, and if something goes wrong we can easily keep track why/where/when/how
- **REDUX** is built on top of functional programming principles, we shouldn't mutate (change) any data in **REDUX**
## **Pros**:
1. Centralize application's state
2. Makes data flow transparent and predictable
3. Easy debugging
4. Preserve page state
5. Undo/redo
## **Cons**:
6. Complexity 
7. Verbosity (boilerplate, a lot of repetitive codes)

## **Time-travel Debugging**
- In **REDUX** we can jump to / restore any of the previous state in **REDUX** to and check on the details
- We can also save the entire application state in a single file and reload the application from it later

![Redux Architecture](https://labs.tadigital.com/wp-content/uploads/2020/04/getting-started-with-redux-1096x453.png)

# **Redux Architecture**
- a funtion that takes the current instance of an oject, and return the update version of the object
- **Action** is a JS object (similar to an Event) that describes what properties need to be updated for the object
- **Reducer** is like the **Event Handler**
- Usually we will have one reducer each to update a slice of the store
```javascript
function reducer(object,action) {
    const updated = {...object}
}
```

# **Pure Functions in Redux**
- Self-documenting, can easily understand from the code itself
- easy testable
- because we don use global state hence we can run these pure funtions in parallel (concurrency)
- cachebale (since the ouput is guarantee if the same parameter is provided, can save time for computation extensive functions)

## **Steps to create Redux App**
1. Design the store (decide what we want to keep in the store)
2. Define the actions
3. Create a reducer
4. Setup the store
## **1. Defining the actions**
```javascript
{
    type: "itemAdded",
    payload : {
        id: 1,
        description: "..."
    }
}
{
    type: "itemRemoved",
    payload : {
        id: 1,
        description: "..."
    }
}
{
    type: "itemPaid",
    payload : {
        id: 1,
        description: "..."
    }
}
```
## **2. Defining the reducer**
```javascript
let lastId = 1

// set the initial state to be an empty array
// when the app begins it will call this reducer function\
// changing the state from undefined to an empty array
const reducer = function (state=[],action) {
    switch (action.type) {
        case "itemAdded":
            return [
                ...state,
                {
                    id: ++id,
                    description: action.payload.description,
                    paid:false
                }
            ];
        case "itemRemoved":
            return state.filter(item => item.id !== action.payload.id);
        case: "itemPaid":
            return state.map(item => 
            item.id !== action.payload.id? item : {...item,paid:true})
            // if payload id match the overwrite the "paid" property to true
        default:
            return state;
    }
}
module.exports = [reducer]
```
## **3. Creating the store**

```javascript
import {createStore} from "JavaScript/Redux/redux";
import {reducer} from "./reducer";

// pass in the reducer function as the argument to "createStore"
// "createStore" is a higher-order function
const store = createStore(reducer);
module.exports = [store]
```
## **4. Dispatching Actions**
- we can use a method called **subscribe** in the store object, to get updated and notified everytime the state of the store changes (used by UI layer)
- we can only **getState()** from the store, to change the state of the store we have to dispatch an action, and we need to send the action through the same entry point
- **subscribe** method will get called everytime the state of the store gets changed
- **subscribe** methods will return a function for unsubscribing, this is important as a user might navigate to a new page and some UI component is no longer needed, as we dont need to subscribe to the store anymore and this will cause memory leak
```javascript
import {store} from "./store";

// subscribe function
const unsubscribe = store.subscribe(()=>{
    console.log("State of the store has changed",store.getState())
})

// dispatch action to add item
store.dispatch({
    type:"itemAdded",
    payload:{
        description:"iceCream"
    }
})

// store's state = {id:1,description:"iceCream",paid:false}

// dispatch action to remove item
store.dispatch({
    type:"itemRemoved",
    payload:{
        id:1
    }
})

// store's state = []

unsubscribe()
```