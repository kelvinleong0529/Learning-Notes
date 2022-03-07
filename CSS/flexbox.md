
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

# **Flex Conatiner (Parents)**

## **Flex Direction**
![alt text](https://css-tricks.com/wp-content/uploads/2018/10/flex-direction.svg)
```css
.container {
  display: flex; /* or inline-flex */
}
/* defines a 'flex' container */

.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```


## **Flex-wrap**
![alt text](https://css-tricks.com/wp-content/uploads/2018/10/flex-wrap.svg)
- By default, flex items will all try to fit onto one line. You can change that and allow the items to wrap as needed with this property
1. nowrap (default): all flex items will be on one line
2. wrap: flex items will wrap onto multiple lines, from top to bottom.
3. wrap-reverse: flex items will wrap onto multiple lines from bottom to top.
```css
.container {
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

## **Flex Direction + Flex-wrap**
```css
.container {
  flex-flow: column wrap;
}
/* flex direction => column, flex-wrap => wrap */
```
## **Justify Content**
![alt text](https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg)
- defines the alignment along the main axis
- helps distribute extra free space leftover when either all the flex items on a line are inflexible, or are flexible but have reached their maximum size
1. flex-start (default): items are packed toward the start of the flex-direction.
2. flex-end: items are packed toward the end of the flex-direction.
3. start: items are packed toward the start of the writing-mode direction.
4. end: items are packed toward the end of the writing-mode direction.
5. left: items are packed toward left edge of the container, unless that doesn’t make sense with the flex-direction, then it behaves like start.
6. right: items are packed toward right edge of the container, unless that doesn’t make sense with the flex-direction, then it behaves like end.
7. center: items are centered along the line
8. space-between: items are evenly distributed in the line; first item is on the start line, last item on the end line
9. space-around: items are evenly distributed in the line with equal space around them. Note that visually the spaces aren’t equal, since all the items have equal space on both sides. The first item will have one unit of space against the container edge, but two units of space between the next item because that next item has its own spacing that applies.
10. space-evenly: items are distributed so that the spacing between any two items (and the space to the edges) is equal.

## **Align-Items**
![alt text](https://css-tricks.com/wp-content/uploads/2018/10/align-items.svg)
- defines the default behavior for how flex items are laid out along the **cross axis** on the current line

## **Align-Content**
![alt text](https://css-tricks.com/wp-content/uploads/2018/10/align-content.svg)

## **Gap**
![alt text](https://css-tricks.com/wp-content/uploads/2021/09/gap-1.svg)
- controls the space between flex items
- applies that spacing only between items not on the outer edges
```css
.container {
  display: flex;
  ...
  gap: 10px;
  gap: 10px 20px; /* row-gap column gap */
  row-gap: 10px;
  column-gap: 20px;
}
```

# **Flex Items (Children)**

## **Flex-grow**
![alt text](https://css-tricks.com/wp-content/uploads/2018/10/flex-grow.svg)
- defines the ability for a flex item to grow if necessary
- accepts a unitless value that serves as a proportion
- dictates what amount of the available space inside the flex container the item should take up.
- If all items have flex-grow set to 1, the remaining space in the container will be distributed equally to all children. If one of the children has a value of 2, that child would take up twice as much of the space either one of the others (or it will try, at least)