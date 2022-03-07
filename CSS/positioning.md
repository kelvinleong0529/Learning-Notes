# **Positioning**
```css
position: static;
position: relative;
position: absolute;
position: fixed;
position: sticky;

/* Global values */
position: inherit;
position: initial;
position: revert;
position: unset;
```

[Refer to this link for more info on CSS positioning](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

1. **Static**: element is positioned according to the normal flow of the document
2. **Relative**: element is positioned according to the normal flow of the document, and then offset relative to itself,the offset does not affect the position of any other elements; thus, the space given for the element in the page layout is the same as if position were static
3. **Absolute**: element is removed from the normal document flow, and no space is created for the element in the page layout. It is positioned relative to its closest positioned ancestor, if any; otherwise, it is placed relative to the initial containing block
4. **Fixed**: element is removed from the normal document flow, and no space is created for the element in the page layout. It is positioned relative to the initial containing block established by the viewport
5. **Sticky**: element is positioned according to the normal flow of the document, and then offset relative to its nearest scrolling ancestor and containing block (nearest block-level ancestor), including table-related elements, based on the values of top, right, bottom, and left. The offset does not affect the position of any other elements