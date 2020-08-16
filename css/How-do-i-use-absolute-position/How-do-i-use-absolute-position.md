# How do i use absolute position in css 

The absolute posittion is a powerful weapon in your design. It can literally place your elements anywhere you want .We can apply properties like  **top,right,bottom and left** over any element once the element has been made absolute. 

<img width="100%" src="https://res.cloudinary.com/dbbunxz2o/image/upload/v1597494563/Frame_1_vhzkbl.svg">

We can directly push the element to any extreme side by specifying to **0**,  
for example **top: 0;** will push the element to the top of the page.     
We can also use normal units like pixels which will move away from the extreme side to the given units,  
for example **top:50px;** will move away the element 50 pixels away from the top.

However it can be difficult to use it effectively as it gets removed from the natural flow of other elements and wont follow any of the rules set by other elements of page. 

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

if we uncomment the position property we can see that the div elements are out of flow with the document and only the p element consumes the space here,also all elements are overlapping, we can choose which element to present in top layer by giving **z-index** value,the  element with higher z-index  will be present in the front. 


The element is positioned according to its container block .By default the container block is the document's body and not it's parent div. In order to act as a child to its parent div we need to add **position:relative;** to its parent.

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
The child element is relative to it's nearest parent element having the  property **position: relative**.

## Some cool uses for Absolute Position 

- Floating Images 
- Putting an Images on top on an element
- Placing Icons outside containers 
- Badges 
- Floating containers

## Conclusion
It's is best  not overuse absolute positioning because it can be pretty difficult to maneuver especially when  you are making your website responsive.


