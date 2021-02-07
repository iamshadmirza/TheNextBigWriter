Hello, I am Shivam Verma. Today we are going to understand one of the most frequently asked questions in interviews. 
What is **Hoisting** in JavaScript? 

First of all, let us understand the concept of **Hoisting**. Let's Begin

## Understanding "Hoisting"

Let us take a look at a code example.

```javascript
var x = 7;
function sayHi() {
     console.log("Hello World");
}
sayHi();
console.log(x);
```

Output: 

```javascript
Hello World
7
```
Simple right.
 Let's tweak the code a little bit and see

```javascript
sayHi();
console.log(x);
var x = 7;
function sayHi() {
     console.log("Hello World");
}
```

Output: 

```javascript
Hello World
undefined
```

Well something strange in the output there, isn't it? How is the function executed at the top even before declaration? Why is the value of `x` shown as `undefined`?

This is possible because of **Hoisting**

**Hoisting** is a concept by which you can access variables and functions even before initializing them.

## How does **Hoisting** work?

You might be thinking that the title says "The real way". Hmmm, what is this real way?
Is **Hoisting** done in more than one way in JavaScript?

No, it's not done in more than one way, there is just some incomplete and little incorrect information spread about **Hoisting**.

Let me clear your doubts. You might have heard the popular definition of **Hoisting** available in numerous blogs and videos on the internet which is somewhat like,

"Variable and function declarations are moved "magically" to the top of the JavaScript code"

Well, we are writing code, not in Hogwarts 😂. Behind every code there lies logic and not magic.

Ok, enough joking, nobody writes magically in the definition, It was put there sarcastically to show why that definition is wrong.

To know the "real" working of **Hoisting**, you should have a clear understanding of the `Execution Context`. If you don't know about it, then no need to worry. I have written a very informative blog about it which you can find [here](https://blog.theshivamverma.com/how-does-javascript-work-1)

Now let's look at some more variations of the above code and then understand it with the `Execution Context`

```javascript
sayHi();
console.log(x);

var x = 7;

function sayHi() {
     console.log("Hello World");
}
console.log(sayHi);
```

Output: 

```javascript
Hello World
undefined
function sayHi() {
     console.log("Hello World");
}
```

Let me take the last `console.log` and shift it to the top and then see

```javascript
sayHi();
console.log(x);
console.log(sayHi);

var x = 7;

function sayHi() {
     console.log("Hello World");
}
```

Output: 

```javascript
Hello World
undefined
function sayHi() {
     console.log("Hello World");
}
```

As you can see, in the case of `x` we get `undefined` if we access it before initializing. But in the case of the function `sayHi` we can invoke it as well as get the whole function code even before initializing it.
 
This is happening because of `Execution Context`. What actually is happening is that the `Execution Context` as we know works in two phases. So in the **Memory Creation Phase** it goes through all the code line by line and allocates memory to all the variables and functions.

It stores a special value of `undefined` for variables and stores the whole function code as it is for the functions. The real value of the variable which we want it to have will get replaced from `undefined` in the **Code Execution Phase**

So when we run the code i.e the **Code Execution Phase**, the `console.log(x)` statement when executes it gets the value of `x` which is still stored as `undefined` in the memory.

And the function `sayHi` it's whole code is stored so it can easily get executed in the second line and `console.log(sayHi)` can also print the function code as it is.

And that is how variables and functions are accessible even before initialization through **Hoisting** because of the `Execution Context` and not by **Wingardium Leviosa**.

Before wrapping up let me explain about different types of functions and their **Hoisting**.

What if we use an arrow function, let's see

```javascript
console.log(sayHi);

var sayHi = () => {
     console.log("Hello World");
}
```

Output:
```javascript
undefined
```

What if it was a function expression

```javascript
console.log(sayHi);

var sayHi = function() {
     console.log("Hello World");
}
```

Output:
```javascript
undefined
```

Now you might be confused as I said function gets stored as it is in the memory and we can access it but the recent examples are not following what I said.

This is happening because in both the examples it is getting treated as a **variable** and not as a function by JavaScript. The function code is the value of the variable which will get stored later during initialization.

If we try to invoke any of the above functions either the arrow function or the function expression before initialization then we will get an error 

`Uncaught TypeError: sayHi is not a function`.

Because we are trying to invoke `sayHi` which is a variable.

The function declaration which we used in the early examples gets treated as a proper function and gets hoisted.

So in the case of functions, we can say that:

**Only function declaration gets hoisted in JavaScript.**

That's all about **Hoisting** for today.

I got to learn about Hoisting in this much detail from **Akshay Saini**'s awesome playlist on YouTube called *"Namaste JavaScript"*. Do check it out [here](https://www.youtube.com/playlist?list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP)

Now you can definitely give a proper answer with a good explanation if anyone asks you about hoisting.

Share with your friends and colleagues if you like it.

Leave a comment for the feedback or any suggestion of topic for upcoming blogs.

Or connect with me on [Twitter](https://twitter.com/the_shivamverma)