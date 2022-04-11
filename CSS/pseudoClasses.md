# **Pseudo-classes**
- pseudo-class is used to defined a speical state of an element:
1. Style an element when a user mouses over it
2. Style visited and unvisited links differently
3. Style an element when it gets focus
```css
/* unvisited link */
a:link {
  color: #FF0000;
}

/* visited link */
a:visited {
  color: #00FF00;
}

/* mouse over link */
a:hover {
  color: #FF00FF;
}

/* selected link */
a:active {
  color: #0000FF;
}

/* combine pseudo-classes with HTML classes */
a.highlight:hover {
  color: #ff0000;
}
```
```css
/* select the first <p> element that is the first child of any element*/
p:first-child {
  color: blue;
}

/* match the first <i> element in all <p> elements */
p i:first-child {
  color: blue;
}
```
## **lang Pseudo-class** 
- allows us to define special rules for different languages
```css
<html>
<head>
<style>
q:lang(no) {
  quotes: "~" "~";
}
</style>
</head>
<body>

<p>Some text <q lang="no">A quote in a paragraph</q> Some text.</p>

</body>
</html>

/* result:
Some text~A quote in a paragraph~Some text.

In this example, :lang defines the quotation marks for q elements with lang="no": */
```