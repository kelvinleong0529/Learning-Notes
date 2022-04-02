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

#para1 {   /* select all HTML elements with id="para1" */
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
