# **CSS Box Model**
- Everything displayed by the CSS is a box
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

## **Content And Sizing**
- Extrinsic Sizing => User control the box sizing on their own, there's a limit on how much content we can add before it overflows out of the box's bounds
- Intrinsic Sizing => Let the browser to make decision for us based on the content sizing