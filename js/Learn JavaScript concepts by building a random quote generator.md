Learning JavaScript is fun. But What's the point if you are not building stuff with it.
So in this article, we will learn javascript basic concepts and create a random quote generator of our own.

I assume you have a basic knowledge of HTML and CSS  as the main objective of this article is to learn javascript. Else you can check these tutorials on [HTML](https://youtu.be/UB1O30fR-EE) and [CSS](https://youtu.be/yfoY53QXEnI). I will try to explain everything in detail and by the time you finish this lesson, you will have an understanding of concepts like strings, arrays, functions, event listeners, template literals in JavaScript. So let's begin.


## Getting started
Lets first create three different files in our folder as 
- index.html for creating the UI and displaying the content,
- style.css to make it attractive by adding styles.
- script.js will contain the actual code which makes our app work.


## 1. creating the content of the app
The first step is to create a UI. Here is our index.html file look like 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <link rel="shortcut icon" href="icons/favicon.png">
    <title>Random quote</title>
</head>
<body>
    <div class="content">
        <div class="card">
          <h2>Random quote</h2>
          <p>wanna see a random quote ?</p>
          <!--button to display random quote-->
          <button class="btn">Generate</button>

        </div>
        <div id="quote">
         <!--Quote will be displayed here.-->
        </div>
    </div>
</body>
<script src="script.js"></script>
</html>
```

![Screenshot (238).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1585025931498/AIvbN-aiu.png)

And this is how it looks like in the browser. Wait a minute, It doesn't look nice right. 
## 2. Styling the content
Let's make it appealing by adding our style.css file

```css
body{background-color: indigo;  margin:auto;}
h2{background-color: #1c1c1c; color:#ffffff;
padding:10px;
font-family: arial;
text-align: center;}

.btn{height:50px; width:150px;
font-size: 18px;
color:#ffffff;
background-color: dodgerblue;
border:none;
padding:5px;
border-radius: 5px;}

.card{padding:15px 30px 15px 30px;
margin:40px auto;
max-width:500px;
max-height:300px;
text-align: center;
background-color: #ffffff;
border-radius: 5px;
} 

p{font-family:'Segoe UI';
font-weight:400;
font-size: 20px;}

img{height:25px;
width:25px;
}
```
And boom ! this looks great now.


![Screenshot (240).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1585027409630/ZG-vq7LdP.png)

Now let's think about how we are going to make it work. We need to figure out a way to display random quotes after clicking a button. And We will go with the simplest way to do it. How? let's see.

Forget coding. let's just think about what we have to do. 
okay. First, we will need quotes. We will have to store them somewhere and do something such that we can display a random quote after clicking a button. That's it. 

## 3. let's learn some javaScript

### Strings

> 
A string is a sequence of one or more characters that may consist of letters, numbers, or symbols. Strings in JavaScript are primitive data types which we are going to use to create quotes.

In JavaScript, there are three ways to write strings. They can be written inside single quotes (' '), double quotes (" "), or backticks (` `). 
Strings with backticks(``) are called template literals which we will learn later.

```javascript
'This is a string'
```
So all our quotes are basically strings like this.
```
'Stay hungry, stay foolish !'
```
 But there are multiple such strings and we need something to store them. Here comes the concept of Arrays. But what's an array?

### Arrays

> 
An array in JavaScript is a type of global object that is used to store data. Arrays consist of an ordered collection or list containing zero or more data types, and use numbered indices starting from 0 to access specific items.
 
```
<!--Creating an array-->
let quotes =[];
```
Arrays can contain any data type, including numbers, strings, and objects. We will be storing our strings in an array like this.
```javascript
let quotes=[
'The secret to life is to love who you are.',
'Look for opportunities in every change in your life.',
'Persist while others are quitting.',
'and so on.'
];
```
### Array.length
The length property of an object which is an instance of type Array sets or returns the number of elements in that array.
```
quotes.length;
<!--Output-->
4
```

#### Accessing Items in an Array
An item in a JavaScript array is accessed by referring to the index number of the item in square brackets.
```javascript
quotes[2];
<!--Output : -->
Persist while others are quitting.

```
But here we will not access like this. We want a random index to display a random quote. Then how do we do that? We will use the math object.

### Using Math object

> 
Math is a built-in object that has properties and methods for mathematical constants and functions.

![Screenshot (242).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1585047447641/KLYjO52E1.png)

If you type math in console, you will see there are so many built-in methods for Math object. We will be using a few of them.

### Math.random() 
The Math.random() function returns a floating-point, pseudo-random number in the range 0 to less than 1. See how it returns every time we call it in the console.


![Screenshot (243).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1585151170351/FFMTnGRBt.png)


But this is not what we want. We want a whole number and not a floating type. For this, the Math object provides another method called Math.floor()

### Math.floor()
Math.floor() returns a number representing the largest integer less than or equal to the specified number. So if we pass the math.random() as a parameter to math.floor() we will get a whole number.
But Math.floor() is always rounding down to the nearest decimal, therefore, every decimal between 0 and 1 will always revert back to 0.


![Screenshot (245).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1585047247928/aNY04WDp2.png)

In order to get a random number between 0 to the length of our array, we will multiply the math.random() by quotes.length. 
Finally the random index we want is 
```javascript
let index=Math.floor(Math.random()*quotes.length);
<!--This will give a random quote-->
quotes[index];
```
index will always generate a valid array index number for our quotes array.
So we figured out how to retrieve a random quote from the quotes array. But we don't want to display just a string. We are going to do it nicely using template literals.

### Template Literals
> 
The Template Literal, introduced in ES6, is a new way to create a string. With it comes new features that allow us more control over dynamic strings in our programs.

Template literals are string literals allowing embedded expressions. It can contain placeholders. These are indicated by the dollar sign and curly braces (${expression}).
```
`string text ${expression} string text`;
```

### HTML Templates
With the ability to have multi-line strings and use Template Expressions to add content into our string, this makes it really nice to use for HTML templates in our code. So we will create a HTML template for our quote and store it in a variable. We used the placeholder to pass our quotes in the template.
```
let quote=`<div class="card">
<img src="icons/favicon.png">
<p>${quotes[index]}</p> <!--random quote string-->
<img src="icons/favicon.png">
</div>
`;
```
*I added images to make it more appealing. 
*
### Query Selectors
To access an element in dom([Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)), we will use the querySelector() method.
The Document method querySelector() returns the first element within the document that matches the specified selector. The syntax is 
```javascript
element = document.querySelector(selectors);
```
 In our HTML file, we have a div element with id="quote". We will access it in the same way as this. And then we will add the HTML template we created earlier to this div element.

### Element.innerHTML
Each HTML element has an innerHTML property that defines both the HTML code and the text that occurs between that element's opening and closing tag. By changing an element's innerHTML after some user interaction, we can make much more interactive pages.


```javascript
let div=document.querySelector('#quote');
div.innerHTML=quote;
```
The code we wrote till now will work only once. And we want to execute this every time we want to display a quote. We can do this using functions.

### Functions 

> 
A function is a block of code that performs an action or returns a value. Functions are custom code defined by programmers that are reusable, and can, therefore, make your programs more modular and efficient.

### Defining a Function
Functions are defined, or declared, with the function keyword. Below is the syntax for a function in JavaScript.
```javascript
function nameOfFunction() {
    // Code to be executed
}
```
We will create the displayQuote function add all this code in the function.
```javascript
function displayQuote(){
let index=Math.floor(Math.random()*quotes.length);

//display the quote of that index
let div=document.querySelector('#quote');
let quote=`<div class="card">
<img src="icons/favicon.png">
<p>${quotes[index]}</p>
<img src="icons/favicon.png">
</div>
`;
div.innerHTML=quote;
}
```
We are almost done. Just need to invoke this displayQuote function whenever we click the generate button.

### Events in javaScript
Events are actions that take place in the browser that can be initiated by either the user or the browser itself. 
Like in our case it's when the user clicks the generate button.

### Event listeners
An event listener watches for an event on an element. We will use the addEventListener() method to listen for the event. addEventListener() takes two mandatory parameters . 
- the event it is listening for 
- and the listener callback function.

```javascript
target.addEventListener(type, listener [, options]);
```
We have a button element with class="btn". The click event will call the displayQuote function every time we click on the button and display a random quote.

```javascript
let btn=document.querySelector('.btn');
btn.addEventListener('click', displayQuote);

```
![Screenshot (248).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1585072651093/2_UBWoiXG.png)

And we are done. congratulations. We built a random quote generator while learning some JavaScript concepts.

## Conclusion
So the quote generator is ready. Also if you wish, you can add some more features of your own like tweeting the quote or something like that.

You can find the complete repository of the code on [Github](https://github.com/rutikwankhade/Random-Quote).                                    
Also, you can see it [live](https://random-quotesforu.netlify.com/) here.
I hope you had fun while doing this and learned a few things along the way.
Well for me this process of building things helps me a lot while learning.


%[https://twitter.com/WankhadeRutik/status/1228373769980432384]


You can connect with me on [Twitter](https://twitter.com/WankhadeRutik), [Github](https://github.com/rutikwankhade)  or [Linkedin](https://www.linkedin.com/in/rutik-wankhade).

⚡ Happy learning !