# **CSS Box Model**
- When laying out a document, the browser's rendering engine represents each element as a rectangular box
- CSS determines the size, position, and properties (color, background, border size, etc.) of these boxes
- every box is composed of 4 parts: **CONTENT, PADDING, BORDER, MARGIN**
![alt text](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model/boxmodel-(3).png)
1. **CONTENT AREA**
- contains the real content of the element, such as **TEXT, IMAGE, VIDEO**
- Dimensions: Content Width & Content Height
- Often has a background color or background image
2. **PADDING AREA**
- extends the content area to include the element's padding
3. **BORDER AREA**
- extends the padding area to include the element's borders
4. **MARGIN AREA**
- extends the border area to include an empty area used to separate the element from its neighbors

# **Selectors**
1. **CSS Class Selectors**
- class name CANNOT start with number
```CSS
.center {   /* select all HTML elements with class ='center' */
  text-align: center;
  color: red;
}

p {   /* select all HTML elements with <p> tags */
  text-align: center;
  color: red;
}

#para1 {   /* select all HTML elements with if="para1" */
  text-align: center;
  color: red;
}

* { /* the following CSS rule will affect all HTML elements */
  text-align: center;
  color: blue;
}

<p class="center large">This paragraph refers to two classes.</p>
/* the above element will be styled according to class='center' and class='large' */
```

2. **CSS Grouping Selector**
- group elements with the same style definitions together
```CSS
h1, h2, p {
  text-align: center;
  color: red;
}

/* style <h1> <h2> <p> elements with the same stylings */
```

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
- **:lang Pseudo-class** allows us to define special rules for different languages
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

# **Flexbox**
- **Flexbox layout** aims to provide a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic
- A flex container expands items to fill available free space or shrinks them to prevent overflow
![alt text](https://css-tricks.com/wp-content/uploads/2018/11/00-basic-terminology.svg)
1. main axis – The main axis of a flex container is the primary axis along which flex items are laid out. Beware, it is not necessarily horizontal; it depends on the flex-direction property (see below).
2. main-start | main-end – The flex items are placed within the container starting from main-start and going to main-end.
3. main size – A flex item’s width or height, whichever is in the main dimension, is the item’s main size. The flex item’s main size property is either the ‘width’ or ‘height’ property, whichever is in the main dimension.
4. cross axis – The axis perpendicular to the main axis is called the cross axis. Its direction depends on the main axis direction.
5. cross-start | cross-end – Flex lines are filled with items and placed into the container starting on the cross-start side of the flex container and going toward the cross-end side.
6. cross size – The width or height of a flex item, whichever is in the cross dimension, is the item’s cross size. The cross size property is whichever of ‘width’ or ‘height’ that is in the cross dimension.