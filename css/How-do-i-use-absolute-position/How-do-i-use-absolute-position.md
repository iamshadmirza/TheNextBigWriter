# How do I use absolute position in CSS 

 The **absolute** position is a powerful weapon in your design. It can literally place your elements anywhere you want. We can apply properties like  **top, right, bottom and left** over any element once the element has been made absolute. 

<img width="100%" src="https://res.cloudinary.com/dbbunxz2o/image/upload/v1597494563/Frame_1_vhzkbl.svg">
 
 We can directly push the element to any extreme side by specifying that direction  to **0**,  
For example **top: 0;** will push the element to the top of the page.     
We can also use normal units like pixels which will move away from the extreme side to the given units,  
For example **top: 50px;** will move away the element 50 pixels away from the top.

However, it can be difficult to use it effectively as it gets removed from the natural flow of other elements and won't follow any of the rules set by other elements of the page. 

```HTML
<div>box 1</div><div>box 2</div><div>box 3</div><div>box 4</div>
<p>four boxes</p>

<style>
.box{
  height: 40px;
  width: 40px;
  background: #C4C4C4;
  margin: 4px;
  text-align: center;
 /* position: absolute; */
}
p{
  color: red;
}
</style>
```

<img width="100%" src="https://res.cloudinary.com/dbbunxz2o/image/upload/v1597489582/Frame_1_lmj1ce.svg">

If we uncomment the position property we can see that the div elements are out of flow with the document and only the p element consumes the space here.  
We can also notice that all elements are overlapping, we can choose which element to be present in the top layer by giving **z-index** value, the element with higher z-index will be present in the front.  

 The element is positioned according to its containing block. By default the containing block is the document's body and not its parent div. In order to act as a child to its parent div we need to add **position: relative;** to its parent.

```HTML
<div class="parent">
<div class="child"> </div>
  </div>

  <style>
  .parent{
 background: dodgerblue;
 position: relative;
 height: 100px;
 width: 100px;
}
.child{
  position: absolute;
  background: hotpink;
  height: 50px;
  width: 50px;
  right: 0;
}
  </style>
```
<img src="https://res.cloudinary.com/dbbunxz2o/image/upload/v1597495812/box_1_shppir.svg">
Here the child element is **relative** to its parent div element and not the whole document.
.The child element is relative to it's nearest parent element having the property **position: relative**.

## Some cool uses for Absolute Position 

- Floating Images 
- Putting an Image on top of an element
- Placing Icons outside containers 
- Badges 
- Floating containers



## Takeaways
We can place some elements where ever we want and choose what to be in front and back layer that would have been difficult or impossible to do with other methods,However it is recommended not to overuse **absolute** positioning because it can be pretty difficult to maneuver especially when  you are making your website responsive.


