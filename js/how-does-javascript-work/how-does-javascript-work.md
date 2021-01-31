Hello, 👋 this is Shivam Verma, this is my first blog and in this, I will help you to understand the working of JavaScript. Let's Begin!!

#### Ever wondered how JavaScript works under the hood?     

Well by the end of this blog you will have a clear understanding of that by knowing two important concepts that make it possible
1. **Execution Context**
1. **Call Stack**          

### 1. Execution Context

Before diving deep into the working of `JavaScript` remember one thing
> "Everything in JavaScript happens inside an `Execution Context`" 

`Execution Context(EC)` can be classified into two main types:
- Global Execution Context(GEC)
- Functional Execution Context(FEC)

I will specify when which `EC` is created, other than that we will refer to it commonly as `Execution Context`

So the `Execution Context` is divided into 2 parts
- **Memory Component**
- **Code Component** 
 
The **Memory Component** also known as the **Variable Environment** allocates memory and stores variables and functions as *key: value* pairs.

The **Code Component** also known as the **Thread of Execution** runs through the JavaScript program and executes line by line.

Now If I may present the `Execution Context` visually as a diagram it can be shown as:

![Group 6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611776579826/9DOXVBrgh.png)

Another line to keep in mind for working of JavaScript
> " JavaScript is **Synchronous Single-Threaded** language "

This means that JavaScript can only execute one command at a time in a specific order. It can only go to the next line only if the current line is finished executing.

I know you might be thinking that, What about asynchronous programming in JavaScript? Is there no asynchronous programming in JavaScript? Did I get fooled by that Indian guy on YouTube?
Calm down I will write about that in upcoming blogs, let's stick to our topic for this blog.

So coming back to `Execution Context` just remember for now that only one line at a time can be executed in JavaScript.

Let's understand the working in more detail with the help of a code example.

![code_ec.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611832015671/EjLaexeUw.png)


Now when we run this code a `Global Execution Context(GEC)` is created

The `Execution Context` is created in two phases.
1. **Memory Creation Phase**
1. **Code Execution Phase**

In the first phase i.e the **Memory Creation Phase**, JavaScript allocates memory to all the variables and functions.
The JS Engine goes through the code line by line. It encounters variable declaration at line 1 and allocates memory to the variable `n`. Then it goes to line 2 and allocates memory for a function named `square`.

In the case of variable `n`, a special value `undefined` is stored with it whereas the whole function code is stored as it is in the case of the function.
Coming to line 6 and 7 it encounters two more variables `square2` and `square4` and as they are variables assigns their value as `undefined`.

After completion of **Memory Creation Phase** the `Execution Context` might look like this

![EC2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611834569752/7qZBtgAcE.png)

Now the second phase i.e **Code Execution Phase** begins
The JS Engine again goes through the code line by line and executes the code.
It executes the first line `var n = 2` and replaces the `undefined` value of `n` from the Memory block with the actual value `2`.

Then it comes to line 2 and encounters a function `square` and skips the code from line 2 to line 5.

Then when it goes to line 6 and encounters a function call or a function invocation.
Now it knows that it has to execute a function.

> " Functions are the heart of JavaScript " - Akshay Saini

Whenever a function is invoked a new `Execution Context` will be created and this will be a brand new `Functional Execution Context(FEC)` inside the `Global Execution Context(GEC)`

This new `Execution Context` will again consist of two blocks, **Memory** and **Code**, and will also follow the two phases of creation.

In its **Memory Creation phase**, it will allocate memory to variables and functions used in its execution.

It scans for variables and it finds `num` as a parameter and `ans` in the body and assigns `undefined` to them.

In the **Code Execution phase** the value of `n` which is 2 is passed to `num`.

Now in the function body, it executes `num * num` and the evaluated value is replaced for `undefined` in `ans` inside the `FEC`.

After execution of line 3, it encounters a `return` keyword on line 4, so the function knows its execution is finished and now it's time to return the control back to the `Execution Context` from where it was invoked which is the `GEC`.

While returning it returns the value of `ans` from its `Execution Context` to the Global one so the value of `square2` is changed from `undefined` to `4`.

**The whole `Functional Execution Context` is deleted after the return of control.**

A visual representation of the whole process discussed: 

![FEC1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611861952440/MPoJltLlU.png)

Now the control moves to line 7, where it finds another function invocation `square(4)` with value 4 as an argument. Again brand new `FEC` will be created and the whole procedure used to invoke `square(n)` as explained above will be repeated and the value will be evaluated and returned into square4.

If there is a function inside a function then a nested `FEC` will be created inside the `FEC` which is inside the `GEC`. This has no end it can go beyond and beyond.

After the execution of the whole program is finished, The `Global Execution Context` also gets deleted.

Phew, that was all about the **"Execution Context"**, now you know how is it created and how it executes the code which we write in JavaScript.

Remember I said all this nested `Execution Context` can go on and on, so how does JavaScript handle all this complicated nesting and control of the program.
Luckily JavaScript engine has a stack to manage all these things and we call it 
**The Call Stack**, let's learn more about it in detail.

### 2. Call Stack
You must be familiar with the stack data structure. If not please read about it.
So as we know Stack is a LIFO(Last in First Out) Data Structure.
To enter data in the stack we use `push` and to delete we use the `pop` operation.
The same is the working of the **Call Stack** in JS.

So for better understanding let us see a diagram of the working of **Call Stack** for the mini-program we saw earlier along with `Execution Context`.

![call stack.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611863907602/5oqYN3PEv.png)

Initially the **Call Stack** is empty.
The `Global Execution Context` is at the bottom of **Call Stack**. Whenever a program is run, the **Call Stack** is populated with the `GEC`.

Whenever a new function is invoked a new `FEC` is created and pushed into the stack. Only when it is finished executing, It is popped out of the stack.

At the end, the `GEC` is also popped off and the **Call Stack** becomes empty.

This **Call Stack** is used to manage all these `EC's`.

**Call Stack** maintains the order of execution of `Execution Contexts`

That was it. Now you know two major core concepts behind the working of JavaScript.
How is code executed in JS? 
Now you can confidently answer that question in an interview if asked.

I learned about this stuff from an amazing Youtube Series 
*"Namaste JavaScript" by Akshay Saini*
Awesome content by Akshay, visit the link and watch the videos.
 
**Link to the videos which I followed to write this blog.**

 [Namaste JavaScript Playlist](https://www.youtube.com/playlist?list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP) 

That's all from my side.
How much did you understand and like learning through this blog and the visual diagrams? Let me know in the comments.

If you really liked it then do share it with your friends or colleagues.

Have any doubt or want to work on a project together then follow me on Twitter and message me there.
Also, comment on what should be the next topic and I will try to make that possible.


