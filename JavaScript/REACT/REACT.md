# **Introduction**

### What is REACT?
- REACT is a JavaScript library used to create websites

- REACT allow us to easily create **Single Page Apps** - **SPA**

- Traditional websites send a request to server for a new HTML page whenever the user clicks on a new link

- **SPA** means the server only need to send a single HTML page to the browser to run fully, then REACT takes over and manages the whole website in the browser, including:

1. Website Data
2. User Interactivity
3. Routing between pages (new pages are not sent from browser)

- New pages are loaded quickly and results in a very speedy UX

### How to use EMMET? (if we type .hello, automatically creates a div tag with hello as class)
1. Go to **Settings**
2. Type **EMMET**
3. Search for **Emmet: Include Language**
4. Click **Add Item**
5. Input **javascript** for ITEM and **javascriptreact** for VALUE
6. This will allow us to use EMMET insider REACT components when generating the templates in **JSX**

# **What is Document Object Model DOM?**
- programming API for HTML and XML documents
- defines the logical structure of document and how document is accessed and manipulated
- XML present data as documents, and DOM manages these datas
- programmers can add,modify,delete anything found in HTML or XML using DOM

# **Creating a React Application**

[Download the latest Node.js here](https://nodejs.org/en/)

### Command to generate a REACT project:

```
npx create-react-app "name of the project"
```
Example:
```
npx create-react-app KELVIN-BLOG
```

 1. **node_modules** -> where all the project dependencies live including the REACT library, any package or library installed goes into here
 2. **public** -> all the public files, public to the browser stays here
 3. **index.html** in **public** -> the HTML file that is served to browser and all REACT code is injected into **\<div id="root">\</div>**
 4. **src** -> all REACT components that we write are going to live inside here
 5. **index.js** in **src** -> the core file the application, is responsible for taking all REACT components and mounting them to the **DOM**
 6. **reportWebVitals.js** -> a performance file, not really needed, can delete (remember to delete the related lines in **index.js**)

### Command to preview a project in browser:

```
npm run start
```
1. This command will spin up a lcoal development server so we can preview the web application in browser
2. It is a live server, if any changes is made and saved, the changes will also get reflected in browser

### Command to download all node-modules / dependencies:

```
npm install
```
1. This command will look inside the **package.json** folder that contain all the project dependencies and install all of them
   
# **Components & Templates**

### What are Components?

- Components are the building blocks of REACT applications
- A typical webpage built with REACT might be made up with several different components
- Each component is a self-contained section of content, eg: **Navbar**, **Article**, **Sidebar**
- REACT developers create components which are then rendered to the **DOM** and shown in the webpage by REACT
- Each components contains their own **TEMPLATE** & **LOGIC**
- Every component must have a **function** that should return some values (generally **JSX** templates), and the name of **function** MUST always start with CAPITAL LETTER
- We can write any valid JavaScript functions before the **return** statement
- At the end of component files, we must export the component function so that we can use it in other files:
```javascript
function App() {
    JavaScript functions
    return(
        JSX codes
    )
}
export default App;
```

### What is JSX?

- A syntax almost identical to HTML
- It allow us to easily create HTML style templates and components
- In JSX, we add classess to elements using **className**, we can't use **class** beacuse **class** is a reserved keyword in JavaScript, and when JSC is converted to HTML **className** is converted to **class** as well

### In REACT version < 17, we need to **import REACT** at the top of the component files:

```javascript
import React from 'react'
```

# **Dynamic Values in Templates**

- **JSX** templates in REACT allow us to output dynamic values or variables
- Use curly braces "**{ }**" to output a dynamic value or variable
- REACT is going to convert whatever data type to **STRING** before outputing it
- REACT **CANNOT** output **BOOLEANS** or **OBJECTS** as dynamic values

Example:
```javascript
function App() {
    const title = 'Welcome to my new blog!';
    const likes = 50;
    return(
        <h1> {title} </h1>
        <h1> Liked {likes} times </h1>
    )
}
export default App;
```

# **Multiple Components**

- In REACT components are structured in a way that makes up a component tree
- Root componenet sits at the top of the tree, and is the component that is initially rendered inside the HTML file
- New components are nested inside the root component, eg: **NavBar**, **BlogDetails**

### How to use snippet to create functional component?

```
Install the VS Code extension below:
Simple React Snippets

Type sfc (Stateless Functional Component) and then TAB
```

### How to nest new component inside other component?

```javascript
-------------------------
Navbar.js
-------------------------

function Navbar(){
    return(
        some JSX template
    )
}
export default Navbar;

-------------------------
Home.js
-------------------------

function Home(){
    return(
        some JSX template
    )
}
export default Home;

-------------------------
App.js
-------------------------

import Navbar from './Navbar'
import Home from './Home'

function App(){
    return(
        <div className = "App">
            <Navbar> </Navbar> <!--nest the Navbar component here, can close as usual HTML tags-->
            <Navbar /> <!--or self-closing tag-->
            <div className = "content">
                <Home /> <!--nest the HOME component here-->
            </div>
        </div>
    );
}
```

# **Adding Styles**

- **CSS** to a particular file applies to all the displayed component in browser at that time
- It is recommended to create a main **CSS** file as a global stylesheet, and add all the **CSS** styling into that file
- For example we create **index.css** as the global stylesheet, we then import this **index.css** into **index.js**

### In-line styling in JSX
```javascript
const Navbar = () =>{
    return(
        <a href ='/Home' style={{
            color: "white",
            backgroundColor: "f1356d",
            borderRadius: '8px'
        }}> <!-- rememember to use camel case for in-line JSX CSS styling-->
    );
}
```

# **Click Events**

### How to create a Click Event?
```javascript
const Home = () => {

    const handleClick = () => {
        javascript code to handle click event
    }

    return(
        <h2> Homepage </h2>
        <button onClick={handleClick}> Click me </button> 
        //insert the function name in the curly brackets to handle the click events
    );
}
```
### The code below [with **( )**] will invoke the function regardless user click on the button:
```javascript
const Home = () => {

    const handleClick = () => {
        javascript code to handle click event
    }

    return(
        <h2> Homepage </h2>
        <button onClick={handleClick()}> Click me </button> 
        //this will trigger the "handleClick" function regardless whether the user clicked 
        // on the button; we just want to set a reference to the function 
        // so when a user click then only it will invokes the function
    );
}
```

### How can we pass argument to the event handler function: (Wrap the function inside an anonymous function)
```javascript
const Home = () => {

    const handleClick = (name) => {
        console.log("hello" + name);
        javascript code to handle click event
    }

    return(
        <h2> Homepage </h2>
        <button onClick={ () => handleClick("mario") }> Click me </button>
        // this function will get fired when user clicks on the button
        // 'mario' is pass as an argument to the 'handleClick" function when the button is click
        // the outter curly braces must be kept as it indicates dynamic values
    );
}
```

### Event object in event handler function if we just reference a function
```javascript
const Home = () => {

    const handleClick = (e) => {
        // the first parameter is automatically assign as the event object
        console.log(e); // e is the event parameter
        // we can log it to the console to see the event object
        javascript code to handle click event
    }

    const handleClickAgain = (name,e) => {
        // the first parameter is automatically assign as the event object
        console.log("hello" + name ,e.target);
        // we can log it to the console to see the event object
        javascript code to handle click event
    }

    return(
        <h2> Homepage </h2>
        <button onClick={ handleClick }> Click me </button>
        // if we are just referencing the function
        <button onClick={ (e) => handleClick("mario",e) }> Click me </button>
    );
}
```

# **Using State ( useState Hook)**

- **State** of a component means the data being used in that component at a snapshot, eg: **strings**, **booleans**, **arrays**
- Normal varaiable are not **REACTIVE**, meaning whenever there is any changes or updates, it doesn't trigger REACT to re-render the template with that new value inside it
- If a variable is **REACTIVE**, whenever the value of that variable changes, REACT detects it and re-render the template
- We use something called **HOOK** (particulary named **useState**) to make something **REACTIVE**
- **HOOK** is a special type of function that does a certain job
- **useState** is pretty self-explanatory from the name itself, it allow us to create **REACTIVE** value and change the value whenever we want

### How to use **useState** in REACT:
```javascript
import {useState} from 'react';

const Home = () => {
    const [ name, setName ] = useState("mario");
    // we use array destructuring to grab 2 values that this hook returns
    // 1st value is the name of REACTIVE variable
    // 2nd value is a function that can be used to update the REACTIVE variable's value
    // 2nd value mostly is called "set(variableName)", eg: setName
    const [ age, setAge ] = useState(25);

    const handleClick = () => {
        setName("luigi");
        // when this event handler function is triggered, it updates "name" -> "luigi"
        // then it triggers REACT to re-render the template
        setAge(30);
    }

    return(
        <p> {name} is {age} years old </p>
        // "name" is REACTIVE, whenver the value changes, it will change in the template as well
        <button onClick={ handleClick }> Click me </button>
    );
}
```

# **React Developer Tools**

- Chrome Web Store: [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?utm_source=chrome-ntp-icon)
- It integrates with browser development tools and give us extra features
- **Components** tab: gives a component diagram or component tree of the website / application

# **Outputting Lists**

```javascript
import {useState} from 'react';

const Home = () => {
    const [ blogs, setBlogs ] = useState([
        { title: "Website 1", body: "Lalala", author: "John", id: 1},
        { title: "Website 2", body: "Hahaha", author: "Kelvin", id: 2},
        { title: "Website 3", body: "Lululu", author: "John", id: 3},
    ]);
    // id has to be unique as it will be used by REACT when outputting the list later
    
    return(
        <div className = "Blogs">
            {blogs.map((iterator) => (
                <div className = "blog-preview" key = {iterator.id}>
                    <h2> {iterator.title} </h2>
                    <p> Written by {iterator.author} </p>
                </div>
            ))}
        </div>
        // we use map to loop through the "blogs" array
        // "iterator" is the item that we get each time we iterate through the array
        // when we loop through the list using the "map" method, each root element returned must have a "key" property
        // this "key" property is something that REACT uses to keep track of each item in the DOM as it iterates through it
        // if data chanegs at any point (adding or removing new items to the array), REACT can keep track of those items
        // this "key" property is usually an ID property (must be UNIQUE)
    );
}
```

# **Props & Reusable Components**

- Reusbale components comes in handy where the same logic (codes) has to be applied in different components
- We can pass data from one particular component to another reusbale component template by using **PROPS**, the good-sides are:
1. It makes the reusable component template more clean and reusable
2. It allows the data to be used in the original component

```javascript
-------------------------
BlogList.js // this is Props .js file
-------------------------
const BlogList = (props) => {
    const blogs = props.blogs;
    const title = props.title;

const BlogList = ({blogs,title}) => {

    return (
        <div className = "Blogs">
            {blogs.map((iterator) => (
                <div className = "blog-preview" key = {iterator.id}>
                    <h2> {iterator.title} </h2>
                    <p> Written by {iterator.author} </p>
                </div>
            ))}
        </div>
    );
}

export default BlogList;

-------------------------
Home.js //.js file that use the "BlogList.js" props
-------------------------

import BlogList from "./BlogList"

const Home = () => {
    return (
        <div className="home">
            <BlogList blogs = {blogs} title = "All the Blogs!">
            <!--{blogs} can be retrieved with props.blogs-->
            <!-- the variable passed here can be dynamic or fixed-->
        </div>
    );
}
```

# **Reusing Components**

```javascript
-------------------------
Home.js //.js file that use the "BlogList.js" props
-------------------------

import BlogList from "./BlogList"

const Home = () => {
    return (
        <div className="home">
            <BlogList blogs = {blogs.filter((blog) => blog.author === 'mario')} title = "All the Blogs!">
            <!--return blogs with author === 'mario' only-->
        </div>
    );
}
```

# **Functions as Props**
- We can pass in function as props

```javascript
const BlogList = ({blogs,title,handleDelete}) => {

    return (
        <div className = "Blogs">
            {blogs.map((iterator) => (
                <div className = "blog-preview" key = {iterator.id}>
                    <h2> {iterator.title} </h2>
                    <p> Written by {iterator.author} </p>
                    <button onClick = { () => handleDelete(blog.id)}>delete blog</button>
                </div>
            ))}
        </div>
    );
}

export default BlogList;

-------------------------
Home.js //.js file that use the "BlogList.js" props
-------------------------

import BlogList from "./BlogList"

const Home = () => {

    const [ blogs, setBlogs ] = useState([
        { title: "Website 1", body: "Lalala", author: "John", id: 1},
        { title: "Website 2", body: "Hahaha", author: "Kelvin", id: 2},
        { title: "Website 3", body: "Lululu", author: "John", id: 3},
    ]);

    const handleDelete = (id) => {
        const newBlogs = blogs.filter(blog => blog.id !== id);
        setBlogs(newBlogs);
    } 

    return (
        <div className="home">
            <BlogList blogs = {blogs} title = "All the Blogs!">
            <!--{blogs} can be retrieved with props.blogs-->
            <!-- the variable passed here can be dynamic or fixed-->
        </div>
    );
}
```

# **useEffect Hook**

- using "useEffect" will invoke everytime there is a re-render

``` javascript
import {useEffect} from 'react';
import BlogList from "./BlogList";

const Home = () => {

    const [ blogs, setBlogs ] = useState([
        { title: "Website 1", body: "Lalala", author: "John", id: 1},
        { title: "Website 2", body: "Hahaha", author: "Kelvin", id: 2},
        { title: "Website 3", body: "Lululu", author: "John", id: 3},
    ]);

    const handleDelete = (id) => {
        const newBlogs = blogs.filter(blog => blog.id !== id);
        setBlogs(newBlogs);
    } 

    useEffect(() =>{
        console.log("the webpage is re-render")
    });
    // the funtion inside "useEffect" gets triggered everytime there is a re-render

    return (
        <div className="home">
            <BlogList blogs = {blogs} title = "All the Blogs!">
            <!--{blogs} can be retrieved with props.blogs-->
            <!-- the variable passed here can be dynamic or fixed-->
        </div>
    );
}
```

# **useEffect Dependencies**

- dependencies array controlled when the "useEffect" runs

``` javascript
import {useEffect} from 'react';
import BlogList from "./BlogList";

const Home = () => {

    const [ blogs, setBlogs ] = useState([
        { title: "Website 1", body: "Lalala", author: "John", id: 1},
        { title: "Website 2", body: "Hahaha", author: "Kelvin", id: 2},
        { title: "Website 3", body: "Lululu", author: "John", id: 3},
    ]);

    const handleDelete = (id) => {
        const newBlogs = blogs.filter(blog => blog.id !== id);
        setBlogs(newBlogs);
    } 

    useEffect(() =>{
        console.log("the webpage is re-render")
    },[] );
    // [] is called dependency array
    // if dependency array is empty, "useEffect" function will only run during the first initial render

    useEffect(() =>{
        console.log("the webpage is re-render")
    },[blogs] );
    // "useEffect" function will get triggered whenever blogs values has any changes

    return (
        <div className="home">
            <BlogList blogs = {blogs} title = "All the Blogs!">
        </div>
    );
}
```

# **using JSON server**

```
npx json-server --watch {file path} --port {port number}
eg: npx json-server --watch data/db.json --port 8000
```

end-points that JSON server provides with:

| Endpoint    | API    | Description         |
| ----------- | ------ | ------------------- |
| /blogs      | GET    | Fetch all blogs     |
| /blogs/{id} | GET    | Fetch a single blog |
| /blogs      | POST   | Add a new blog      |
| /blogs/{id} | DELETE | Delete a blog       |

# **Fetching Data with useEffect**

``` javascript
import {useEffect} from 'react';
import BlogList from "./BlogList";

const Home = () => {

    const [ blogs, setBlogs ] = useState(null);
    // the value of "blogs" is initially empty

    const handleDelete = (id) => {
        const newBlogs = blogs.filter(blog => blog.id !== id);
        setBlogs(newBlogs);
    } 

    useEffect(() =>{
        fetch('https://localhost:8000/blogs')
        .then(res => {
            return res.json();
        })
        .then(data => {
            setBlogs(data);
            setIsPending(false);
        })
    },[]);
    // when the webpage is first rendered, it called the JSON server endpoint
    // and fetch the data from the JSON server, then updates it with setBlogs

    return (
        <div className="home">
            { Blogs && <BlogList blogs = {blogs} title = "All the Blogs!"> }
            <!--because initially Blogs is empty, before the "useEffect" function fetches the data from the JSON server "blogs" is empty, so we add "Blogs" in front to ensure this function is run when "blogs" is updated-->
        </div>
    );
}
```

# **Conditional Loading Messages**

``` javascript
import {useEffect} from 'react';
import BlogList from "./BlogList";

const Home = () => {

    const [ blogs, setBlogs ] = useState(null);
    const [isPending,setIsPending] = useState(true);

    const handleDelete = (id) => {
        const newBlogs = blogs.filter(blog => blog.id !== id);
        setBlogs(newBlogs);
    } 

    useEffect(() =>{
        fetch('https://localhost:8000/blogs')
        .then(res => {
            return res.json();
        })
        .then(data => {
            setBlogs(data);
            setIsPending(false);
        })
    },[]);
    // when the webpage is first rendered, it called the JSON server endpoint
    // and fetch the data from the JSON server, then updates it with setBlogs

    return (
        <div className="home">
            { isPending && <div> Loading... </div>}
            { Blogs && <BlogList blogs = {blogs} title = "All the Blogs!"> }
            <!--because initially Blogs is empty, before the "useEffect" function fetches the data from the JSON server "blogs" is empty, so we add "Blogs" in front to ensure this function is run when "blogs" is updated-->
        </div>
    );
}
```

# **Handling Fetch Errors**

```javascript

const [error,setError] = useState(null);

useEffect(() =>{
    fetch('https://localhost:8000/blogs')
    .then(res => {
        if(!res.ok)
        {
            throw Error ("Could not fetch data for that resources")
            // if res.ok is false, it will throw the error above
            // and then jump to the catch statement below
        }
        return res.json();
    })
    .then(data => {
        setError(null);
        setBlogs(data);
        setIsPending(false);
    })
    .catch(err =>{
        setIsPending(false);
        setError(true);
    })
},[]);

return (
    <div className="home">
        { error && <div> {error} </div>}
        { isPending && <div> Loading... </div>}
        { Blogs && <BlogList blogs = {blogs} title = "All the Blogs!"> }
        <!--because initially Blogs is empty, before the "useEffect" function fetches the data from the JSON server "blogs" is empty, so we add "Blogs" in front to ensure this function is run when "blogs" is updated-->
    </div>
);
```

# **Making a Custom Hook**

- Custom hooks in REACT must start with the word "use"

```javascript
-------------------------
useFetch.js //custom Hook .js file
-------------------------

import {useEffect,useState} from react;

const useFetch = () => {

    const [data, setData ] = useState(null);
    const [isPending,setIsPending] = useState(true);
    const [error,setError] = useState(null);

    useEffect((url) =>{ //url here is the API endpoint
        fetch(url)
            .then(res => {
                if(!res.ok)
                {
                    throw Error ("Could not fetch data for that resources")
                    // if res.ok is false, it will throw the error above
                    // and then jump to the catch statement below
                }
                return res.json();
            })
            .then(data => {
                setError(null);
                setData(data);
                setIsPending(false);
            })
            .catch(err =>{
                setIsPending(false);
                setError(true);
            })
    },[url]);

    return {data,isPending,error};
    // can also return an array here
    // but if we return object the order of the properties doesnt matter
}

export default useFecth;

-------------------------
Home.js
-------------------------
import useFetch from './useFetch';

const Home = () =>{

    const url = 'https://localhost:8000/blogs';
    const {data:blogs,isPending,error} = useFetch(url);
    // grab the 'data' and pass it into blogs
}
```

# **REACT Router**

- when we make the first initial request to the server, it sends back a HTML file + compiled REACT javascript files which control the REACT applications, where REACT and REACT router take full control of the application
- When user clicks on a new link on the webpage REACT is going to intercept the request and handle the routing (by injecting the content requested)
- with REACT router we make less request to server and it makes the server faster

### How to install REACT router:
```
npm install react-router-dom
```
```javascript
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function App() {
    return(
        <Router>
        <Navbar />
        <!--"Navbar" is going to show at all time because it is not inside the Switch statement-->
            <div className = 'content'>
                <Switch>
                    <Route path = ''/>\
                        <Home />
                    </Route>
                    <!--path is the directory where the component is stored-->
                    <!--Displays the 'Home' Componenet visit the home page (path="/")-->
                    <!--The content inside Switch is going to change depending on the route-->
                </Switch>
            </div>
        </Router>
        // <Switch> make sure only one routes shows at one time
        // all components that got nested inside <Router> have access to Router
    )
}
```

# **Exact Match Routes**

```javascript
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function App() {
    return(
        <Router>
        <Navbar />
            <div className = 'content'>
                <Switch>
                    <Route exact path = ''/>
                    <!--'Exact" keyword means EXACT match-->
                        <Home />
                    </Route>
                    <Route path = '/create'>
                        <Create />
                    </Route>
                </Switch>
            </div>
        </Router>
    )
}
```
- when request is make to Route, REACT will look at the request and go from top to bottom inside \<Switch>
- REACT will stop at the first match it finds and render the component inside the route

# **Router Links**

- use \<Link> to let REACT handle the requests
- \<Link> prevents request send to server, it looks at the url / path and matches against the routes

```javascript
import { Link } from 'react-router-dom';

const Navbar = () => {
    return (
        <nav className = 'navbar'>
            <div className = 'links'>
                <Link to = '/'> Home </Link>
                <Link to = '/create'> Create </Link>
            </div>
        </nav>
    )
}
```

# **useEffect Cleanup**

- if data A is still trying to be fetched (loading), and we visit another page for data B, we will get an error
- ABORT controller and cleanup function is to stop the old request when user clicks on a new page

```javascript
-------------------------
useFetch.js //custom Hook .js file
-------------------------

import {useEffect,useState} from react;

const useFetch = () => {

    const [data, setData ] = useState(null);
    const [isPending,setIsPending] = useState(true);
    const [error,setError] = useState(null);

    useEffect((url) =>{ //url here is the API endpoint

        const abortController = new AbortController();
        // declare a new Abort Controller
        // associate it with a fetch request, and can Abort Controller to stop the fetch

        fetch(url, { signal:abortCont.signal } )
            .then(res => {
                if(!res.ok)
                {
                    throw Error ("Could not fetch data for that resources");
                }
                return res.json();
            })
            .then(data => {
                setError(null);
                setData(data);
                setIsPending(false);
            })
            .catch(err =>{
                if (err.name === 'AbortError') {
                    console.log("Abort Fetch");
                } 
                // if the ftech is aborted
                else {
                    setIsPending(false);
                    setError(true);
                }
            })

        return () => abortController.abort();
        // abort whatever fetch it is associated with

    },[url]);

    return {data,isPending,error};
}

export default useFecth;
```

# **Route Parameters**

- the changable part of a path is called the route parameter

```javascript
------------------------------
App.js
------------------------------
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function App() {
    return(
        <Router>
        <Navbar />
            <div className = 'content'>
                <Switch>
                    <Route exact path = ''/>
                    <!--'Exact" keyword means EXACT match-->
                        <Home />
                    </Route>
                    <Route path = '/create'>
                        <Create />
                    </Route>
                    <Route path = '/blogs/:id'>
                    <!--the ":id" here is the route parameter-->
                        <BlogDetails/>
                    </Route>
                </Switch>
            </div>
        </Router>
    )
}

------------------------------
BlogDetails.js
------------------------------
import { useParams } from "react-router-dom";

const BlogDetails = () => {
    const { id } = useParams();
    // allow us to grab route parameters from the route

    return (
        <div className = 'blog-details'>
            <h2> Blog Details - { id } </h2>
        </div>
    );
}

------------------------------
BlogList.js
------------------------------
import { useParams } from "react-router-dom";

const BlogDetails = () => {
    return (
        <div className='blog-list'>
            {blogs.map((blog) => (
                <Link to ={`blogs/${blog.id}`}>
                <!--${blog.id} is the dynamic route parameter-->
                    <h2> {blog.title} </h2>
                </Link>
            ))}
        </div> 
    )
}
```

# **Reusing Custom Hooks**

```javascript 
------------------------------
BlogDetails.js
------------------------------
import { useParams } from "react-router-dom";
import useFetch from './useFetch';

const BlogDetails = () => {
    const { id } = useParams();
    const { data, error, isPending} = useFetch('https://localhost:8000/blogs/' + id);
    // the "id" in useFetch is retrieved from useParams

    return (
        <div className = 'blog-details'>
            { isPending && <div>Loading....</div> }
            { error && {error} }
            { data && (
                <h2> {data.title} </h2>
                <article> {data.body} </article>
            )}
        </div>
    );
}
```

# **Controlled Inputs (Form)**

```javascript
import {useState} from 'react';

const Create = () => {

    const [title,setTitle] = useState(''); // intialize it with an empty string
    const [body,setBody] = useState('');
    const [author,setAuthor] = useState('mario'); // set 'mario' as the default value

    return (
        <div className='create'>
            <h2> Add a New Blog </h2>
            <form>
                <label> Blog Title: </label>
                    <input type = 'text'
                    required
                    value = {title} // <!--asign "title" to this input field-->
                    onChange = {(e) => setTitle(e.target.value) }
                    <!--when we try to change the value of this input field it triggers the setTitle function to update "title" value-->
                    />
                <label> Blog Body: </label>
                    <textarea required
                    value = {body}
                    onChange = {(e) => setBody(e.target.value)} > 
                    </textarea>
                <label> Blog author: </label>
                    <select
                    value = {author}
                    onChange = {(e) => setAuthor(e.target.value)} >
                        <option value="mario"> mario </option>
                        <option value="yoshi"> yoshi </option>
                    </select>
                <button> Add Blog </button>
            </form>
        </div>
    )
}
```

# **Submit Events**

- when making a POST request to JSON server, we dont have to assign an ID, JSON server will automatically assigns it an unique ID

```javascript
import {useState} from 'react';

const Create = () => {

    const [title,setTitle] = useState('');
    const [body,setBody] = useState('');
    const [author,setAuthor] = useState('mario');

    const handleSubmit = (e) => {
        e.preventDefault(); // prevent the page from doing default stuffs (ie: refreshing)
        const blog = [title, body, author]; // create an object with the info input
    };

    return (
        <div className='create'>
            <h2> Add a New Blog </h2>
            <form onSubmit = {handleSubmit}> '
            <!--Invokes the 'handleSubmit' function when user clicks Submit-->
                <label> Blog Title: </label>
                    <input type = 'text'
                    required
                    value = {title}
                    onChange = {(e) => setTitle(e.target.value) }
                <label> Blog Body: </label>
                    <textarea required
                    value = {body}
                    onChange = {(e) => setBody(e.target.value)} > 
                    </textarea>
                <label> Blog author: </label>
                    <select
                    value = {author}
                    onChange = {(e) => setAuthor(e.target.value)} >
                        <option value="mario"> mario </option>
                        <option value="yoshi"> yoshi </option>
                    </select>
                <button> Add Blog </button>
            </form>
        </div>
    )
}
```

# **Making a POST Request**

```javascript
import {useState} from 'react';

const Create = () => {

    const [title,setTitle] = useState('');
    const [body,setBody] = useState('');
    const [author,setAuthor] = useState('mario');
    const [isPending,setIsPending] = useState(false); 
    // a state to check whether the webpage is making POST request

    const handleSubmit = (e) => {
        e.preventDefault();
        const blog = [title, body, author];

        setIsPending(true);
        // we are going to make POST request

        fetch("https://localhost:8000/blogs",{
        method:"POST",
        headers: {"Content-Type":"application/json"}
        // headers is to tell the server the type of content with this request
        body: JSON.stringify(blog);
        // need to turn this object into a JSON string
        // this will make a POST request to the endpoint with "blog" as data
        }).then(()=>{
            setIsPending(false);
            // code to execute when the POST request has completed
        })
    };

    return (
        <div className='create'>
            <h2> Add a New Blog </h2>
            <form onSubmit = {handleSubmit}>
            <!--Invokes the 'handleSubmit' function when user clicks Submit-->
                <label> Blog Title: </label>
                    <input type = 'text'
                    required
                    value = {title}
                    onChange = {(e) => setTitle(e.target.value) }
                <label> Blog Body: </label>
                    <textarea required
                    value = {body}
                    onChange = {(e) => setBody(e.target.value)} > 
                    </textarea>
                <label> Blog author: </label>
                    <select
                    value = {author}
                    onChange = {(e) => setAuthor(e.target.value)} >
                        <option value="mario"> mario </option>
                        <option value="yoshi"> yoshi </option>
                    </select>
                {!isPending && <button> Add Blog </button>} 
                {isPending && <button disabled> Adding Blog...</button>}
            </form>
        </div>
    )
}
```

# **Programmatic Redirects**

```javascript
import {useState} from 'react';
import {useHistory} from 'react-router-dom';

const Create = () => {

    const [title,setTitle] = useState('');
    const [body,setBody] = useState('');
    const [author,setAuthor] = useState('mario');
    const [isPending,setIsPending] = useState(false); 
    const history = useHistory();

    const handleSubmit = (e) => {
        e.preventDefault();
        const blog = [title, body, author];

        setIsPending(true);
        // we are going to make POST request

        fetch("https://localhost:8000/blogs",{
        method:"POST",
        headers: {"Content-Type":"application/json"}
        body: JSON.stringify(blog);
        }).then(()=>{
            setIsPending(false);
            history.go(-1); // go back one step to previous webpage / history
            history.push('/'); // the path want to be redirected after adding a new blog
            // '/' means redirect back to the home page
        })
    };

    return (
        <div className='create'>
            <h2> Add a New Blog </h2>
            <form onSubmit = {handleSubmit}> '
            <!--Invokes the 'handleSubmit' function when user clicks Submit-->
                <label> Blog Title: </label>
                    <input type = 'text'
                    required
                    value = {title}
                    onChange = {(e) => setTitle(e.target.value) }
                <label> Blog Body: </label>
                    <textarea required
                    value = {body}
                    onChange = {(e) => setBody(e.target.value)} > 
                    </textarea>
                <label> Blog author: </label>
                    <select
                    value = {author}
                    onChange = {(e) => setAuthor(e.target.value)} >
                        <option value="mario"> mario </option>
                        <option value="yoshi"> yoshi </option>
                    </select>
                {!isPending && <button> Add Blog </button>} 
                {isPending && <button disabled> Adding Blog...</button>}
            </form>
        </div>
    )
}
```

# **Deleting Blogs**

```javascript 
------------------------------
BlogDetails.js
------------------------------
import { useParams,useHistory } from "react-router-dom";
import useFetch from './useFetch';

const BlogDetails = () => {
    const { id } = useParams();
    const { data, error, isPending} = useFetch('https://localhost:8000/blogs/' + id);
    const history = useHistory();

    const handleDelete= () => fetch("https://localhost:8000/blogs"+data.id,{
        method:"DELETE",
        }).
        then(()=>{
            history.push('/');
        }))

    return (
        <div className = 'blog-details'>
            { isPending && <div>Loading....</div> }
            { error && {error} }
            { data && (
                <h2> {data.title} </h2>
                <article> {data.body} </article>
                <button onClick={handleDelete}>delete</buttton>
            )}
        </div>
    );
}
```

# **404 Pgaes**

```javascript
------------------------------
App.js
------------------------------
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import NotFound from './NotFound'

function App() {
    return(
        <Router>
        <Navbar />
            <div className = 'content'>
                <Switch>
                    <Route exact path = ''/>
                    <!--'Exact" keyword means EXACT match-->
                        <Home />
                    </Route>
                    <Route path = '/create'>
                        <Create />
                    </Route>
                    <Route path = '/blogs/:id'>
                    <!--the ":id" here is the route parameter-->
                        <BlogDetails/>
                    </Route>
                    <Route path='*'>
                    <!--if none of the route above is matched, catch this route-->
                        <Not Found/>
                    </Route>
                </Switch>
            </div>
        </Router>
    )
}

------------------------------
App.js
------------------------------

const NotFound = () =>{
    return(
        <h2>Sorry</h2>
        <p>Webpage not found</p>
        <Link to = "/"> back to homepage... </Link>
    );
}
```