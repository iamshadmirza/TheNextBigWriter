# Title - What is `this` inside foo.bar()? 

## The problem

![Code showing - method which is passed as callback loses reference to original obj as this, but calling obj.method() directly works](https://cdn.hashnode.com/res/hashnode/image/upload/v1584584613992/rwNrFCElj.png)

When we pass a method as callback, it loses reference to the original object (as `this`) when it is called.
But calling a method directly works as expected.

Why is that? **Can the spec help us explain this difference?**

*(For simplicity, let's assume the caller doesn't intend to pass a different `this` value here, and calls onClick() directly)*

------

## The explanation

##### For methods,
⭐️ `foo.​bar()` translates to `foo.bar.call(foo)`.

That is, when a method (function which is accessed as a object property) is called, the object gets passed as `this` inside the function.

So, in this case -  
*What* →  foo is passed as `this` inside bar  
*When* →  if bar is a function and *accessed as object property* (i.e. foo.bar).  

##### For functions, 
⭐️ `fn()` translates to `fn.​call(this)`   
(where `this` is taken from caller's scope)

##### Method to function, 
Now, if we were to rewrite `foo.bar()` using a intermediate variable - ` bar1 = foo.​bar;  bar1()`,  
then the value of `this` inside bar will change from `foo` to the `outer this`.

If `bar` was referencing other values from foo using `this`, those values will be undefined or resolve to a wrong variable.

🧠 This is exactly the reason why passing methods as callback changes the value of `this` passed within it. Instead of calling a method directly, callback is passed as a function and called later.

##### In other words,

⭐️ When `foo.bar` is called, the function `bar` is not aware that it is "attached" to the object foo. Based on the exact syntax of a function call, if the language can figure out a clear `someThing.someFunction()` structure, then it will happily forward someThing as this.

So, if you take out a function from a object and call it, there is no way to figure out which object it was originally attached to. Hence, `this` will be set from caller's scope.

-------

## 📖 What does the spec say? 

![EvaluateCall- if IsPropertyReference, set this to base object](https://cdn.hashnode.com/res/hashnode/image/upload/v1584625813403/gPjSBUHIZ.png)

![IsPropertyReference- reference where base is object or primitive](https://cdn.hashnode.com/res/hashnode/image/upload/v1584625822167/ZmBSyVj95.png)

Link - 1. https://tc39.es/ecma262/#sec-evaluatecall, 2. https://tc39.es/ecma262/#sec-ispropertyreference

This `foo.bar` structure is defined in the spec as a [PropertyReference](https://tc39.es/ecma262/#sec-ispropertyreference).  
Think of PropertyReference as anything that is valid as the left side of an assignment expression, if you were assigning to the property of a object or primitive.  

**PropertyReference = Reference + base is object or primitive**

Some examples of valid and invalid PropertyReference -

%[https://gist.github.com/bendtherules/3467664a9c567617342b73c3681c1dc7]


⭐️ If it is a PropertyReference, then set `thisValue` to base of the PropertyReference (i.e. `foo` in `foo.bar`).  
⭐️ Or else, take thisValue from surrounding Environment Record.

The obtained `thisValue` is forwarded to the abstract operation [Call](https://tc39.es/ecma262/#sec-call), which in turn verifies that the resolved value of `foo.bar` is a function and then calls the internal method [function.[[Call]]](https://tc39.es/ecma262/#sec-built-in-function-objects-call-thisargument-argumentslist) with the same thisValue.  
This [[call]] interface is very similar to the `function.call` public interface and can be approximated with that.

#### A few interesting things to note -
1. `foo.bar` is resolved as a string or symbol "bar" within the object `foo` - and goes through the [usual resolution process](https://tc39.es/ecma262/#sec-getvalue) honoring getters, proxies and prototype chains.
2. The function `foo.bar` doesn't need to be a  [simple function object](https://tc39.es/ecma262/#sec-ecmascript-function-objects), but it can be anything with a [[call]] interface like a exoctic bound function or a proxy.  
 [Bound functions](https://tc39.es/ecma262/#sec-bound-function-exotic-objects-call-thisargument-argumentslist), for example, ignore the `thisValue` that was passed in and instead uses internal [[BoundThis]] as the actual this. This is why one solution is to bind a function before passing it as a callback.

----

*That's all! Hope you had a interesting read.  
I would really appreciate if you leave some feedback.*

*If you want to start reading ecmascript specification yourself, https://timothygu.me/es-howto/ is a great starting point.*