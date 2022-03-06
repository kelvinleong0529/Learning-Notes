# **Document Object Model (DOM)**
- an API for manipulating HTML documents
- represents HTML documents as tree of nodes
- provides function that allow us to add, remove and modify the documents
- is cross-platform and language-independant ways of manipulating HTML and XML documents
```HTML
<html>
    <head>
        <title>JavaScript DOM</title>
    </head>
    <body>
        <p>Hello DOM!</p>
    </body>
</html>
```
![alt text](https://www.javascripttutorial.net/wp-content/uploads/2020/01/JavaScript-DOM.png)

# **Node & Element**
- NODE => a generic name of any object in the DOM tree. It can be any built-in DOM element such as the document. Or it can be any HTML tag specified in the HTML document like \<div> or \<p>
- ELEMENT => a node with a specific node type **Node.ELEMENT_NODE**, which is equal to 1
- In other words, the node is the generic type of element. The element is a specific type of the node with the node type Node.ELEMENT_NODE
![alt text](https://www.javascripttutorial.net/wp-content/uploads/2020/01/Document-Object-Model-in-JavaScript.png)
- Compare the **nodeType** property:
```javascript
if (node.nodeType == Node.ELEMENT_NODE) {
    // node is the element node
}
```
- Node has 2 important properties: **nodeName** and **nodeValue**
- If node type is the element node, the **nodeName** is always the same as the element’s tag name and **nodeValue** is always null
```javascript
if (node.nodeType == Node.ELEMENT_NODE) {
    let name = node.nodeName; // tag name like <p>
}
```

### **Short Summary**
- An HTML or XML document can be represented as a tree of nodes, like a traditional family tree.
- Each markup can be represented as a node with a specific node type.
- Element is a specific type of node with the node type Node.ELEMENT_NODE.
- In the DOM tree, a node has relationships with other nodes.

# **Selecting Elements**
1. document.getElementById()
```HTML
<html>
    <head>
        <title>JavaScript getElementById() Method</title>
    </head>
    <body>
        <p id="message">A paragraph</p>
    </body>
</html>
```
```javascript
const p = document.getElementById('message');
console.log(p); // prints "<p id="message">A paragraph</p>"
```
- returns an Element object that represents an HTML element with an id that matches a specified string
- If the document has no element with the specified id, the document.getElementById() returns null
- If the HTML document has multiple elements with the same id, the document.getElementById() method returns the first element it encounters.
2. getElementsByName()
- Unlike the id attribute, multiple HTML elements can share the same value of the name attribute
- The getElementsByName() accepts a name which is the value of the name attribute of elements and returns a live NodeList of elements.
- The return collection of elements is live. It means that the return elements are automatically updated when elements with the same name are inserted and/or removed from the document.
```HTML
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>JavaScript getElementsByName Demo</title>
</head>

<body>
    <p>Please rate the service:</p>
    <p>
        <label for="very-poor">
            <input type="radio" name="rate" value="Very poor" id="very-poor"> Very poor
        </label>
        <label for="poor">
            <input type="radio" name="rate" value="Poor" id="poor"> Poor
        </label>
        <label for="ok">
            <input type="radio" name="rate" value="OK" id="ok"> OK
        </label>
        <label for="good">
            <input type="radio" name="rate" value="Good"> Good
        </label>
        <label for="very-good">
            <input type="radio" name="rate" value="Very Good" id="very-good"> Very Good
        </label>
    </p>
    <p>
        <button id="btnRate">Submit</button>
    </p>
    <p id="output"></p>
    <script>
        let btn = document.getElementById('btnRate');
        let output = document.getElementById('output');

        btn.addEventListener('click', () => {
            let rates = document.getElementsByName('rate');
            rates.forEach((rate) => {
                if (rate.checked) {
                    output.innerText = `You selected: ${rate.value}`;
                }
            });

        });
    </script>
</body>

</html>
```
3. getElementsByTagName()
- accepts a tag name and returns a live HTMLCollection of elements with the matching tag name in the order which they appear in the document
- The return collection of the getElementsByTagName() is live, meaning that it is automatically updated when elements with the matching tag name are added and/or removed from the document
```HTML
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript getElementsByTagName() Demo</title>
</head>
<body>
    <h1>JavaScript getElementsByTagName() Demo</h1>
    <h2>First heading</h2>
    <p>This is the first paragraph.</p>
    <h2>Second heading</h2>
    <p>This is the second paragraph.</p>
    <h2>Third heading</h2>
    <p>This is the third paragraph.</p>

    <button id="btnCount">Count H2</button>

    <script>
        let btn = document.getElementById('btnCount');
        btn.addEventListener('click', () => {
            let headings = document.getElementsByTagName('h2');
            alert(`The number of H2 tags: ${headings.length}`);
        });
    </script>
</body>

</html>
```

4. getElementsByClassName()
- Returns an array-like of objects of the child elements with a specified class name
- When calling the method on the document element, it searches the entire document and returns the child elements of the document
- When calling the method on a specific element, it returns the descendants of that specific element with the given class name

5. querySelector() and querySelectorAll()
- **querySelector()** method allows you to select the first element that matches one or more CSS selectors, if no element matches the CSS selectors, the querySelector() returns null
- **querySelectorAll()** method returns a static NodeList of elements that match the CSS selector. If no element matches, it returns an empty NodeList
```javascript
let firstHeading = document.querySelector('h1'); 
// finds the first h1 element in the document
let heading2 = document.querySelectorAll('h2');
// finds all h2 elements
```

### **Short Summary**
- The getElementsByTagName() is a method of the document or element object.
- The getElementsByTagName() accepts a tag name and returns a list of elements with the matching tag name.
- The getElementsByTagName() returns a live HTMLCollection of elements. The HTMLCollection is an array-like object.
- Use the JavaScript getElementsByClassName() method to select the child elements of an element that has one or more give class names.
- The querySelector() finds the first element that matches a CSS selector or a group of CSS selectors.
- The querySelectorAll() finds all elements that match a CSS selector or a group of CSS selectors.
- A CSS selector defines elements to which a CSS rule applies
