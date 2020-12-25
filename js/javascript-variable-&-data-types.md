In this Blog we'll learn about: 
- What is a JavaScript 
- What can you do with JavaScript
- What is a Variable
- Different Data Types in JavaScript

 ## What is a JavaScript
JavaScript is the most popular & widely-used programming language in the world. It adds logic and interactivity to a web page. Like:
1. Do some Math
2. Manipulate the data according to user's need
3. Validate data

## What can you do with JavaScript
1. Build Web/Mobile Apps/ Web Apps
2. Real-time Networking Applications(like chats & video streaming services)
3. Command-line Tools
4. Games

**Basically Everything**

## What is a Variable
In programming languages, we use a variable to store data temporarily in a computer's memory.

Here is a metaphor, Think of the boxes you use to organize your stuff, you put everything inside and label them so
that they are easy to find. So,


-**The Boxes** here indicates **The Variables**


-**Stuff** that we put inside indicates **data/value of those Variable**


-**Labels** on the boxes are **the name of Variables**


### Let's see how we can declare variables...
```
let variableName = yourValue;
```

There are two ways to declare a variable :


### 1. Let: 
The value of these variables can be reassigned. Such as a counter variable in a Loop. 
```
for (let i = 0; i < 5; i++) {
  // some statements
}
// Some statements will be printed 5 times.
```

### 2. Const: 
The value of these variables can't be reassigned.
```
const PI = 3.14159265359;
```


>**Camel case naming convention** is used to name a variable, in this:
>first letter is always lower case and the words followed after that have their first letter as uppercase

>```var myFirstName = 'Shradha' ```


## Data Types In JavaScript
There are 2 main categories of Data Type in JS:

### 1. Primitive Data Types: 
**Primitives** are known as being immutable data types because there is no way to change a primitive value once it gets created.
```
let string = 'This is a string';
string[1] = 'S';
console.log(string);
//Result: This is a string
```


They are Sub Divided Into 5 categories:

- **Strings:**  We can have a number or any character inside strings Only important thing is they should be declared inside of quotes.
```
let myDogName = 'Rusty';
let value = '1234';
```

- **Numbers:** Category for whole, Fractional and Negative numbers.
```
let age = 8;
```

- **Boolean:** They only have 2 options either true or false, used for building logic.
```
let isAdorable = true;
```

- **Undefined:** Variables that are declared but not initialized.
```
let firstName;
console.log(firstName);
```

- **Null:** Null is "simply nothing". We use null where we explicitly want to clear the value of a variable.

```
/* Suppose we are making a game and we have a currentPlayer variable,
which holds the name of the player, if that player dies, then we could set 
currentPlayer to be null */

let currentPlayer = "Charlie";

currentPlayer = null; //when Charlie dies
```


> JavaScript is a dynamically-typed language, which means a variable's value can change along with its type without an error. The type of variables will be defined at run time based on the values that are assigned to them


```
let num = 50
console.log(num);
//Result: 50

//Reassign num
num = 'fifty'
console.log(num);
//Result: fifty

```


### 2. Non-Primitive Data Types: 
**Non-primitive** values are mutable data types. The value of an object can be changed after it gets created.
```
var arr = [ 'one', 'two', 'three', 'four', 'five' ];
arr[1] = 'twelve';
console.log(arr) 
//Result:  [ 'one', 'twelve', 'three', 'four', 'five' ];
```

They are subdivided into 3 categories:
- **Arrays:** Lets us group data in a list. Used to store multiple values in a single variable.

Suppose I want to model a group of Friends:

let friend1 = 'Monica';

let friend2 = 'Rachel';

let friend3 = 'Joe';

let friend4 = 'Ross';

let friend5 = 'Pheobe';

let friend6 = 'Chandler';


This is a lot of code So rather than having 6 separate variables I can write one variable and inside of it, I can store 6 different values.
```
let friends = ['Monica', 'Rachel', 'Joe', 'Ross', 'Pheobe', 'Chandler'];
```
- **Functions:** lets us wrap functionality into REUSABLE packages. 
> Functions are sort of variables for the line of code. If a normal variable can store a value, a function can store 20 lines of code.

```
//Declare a Function first
function greetings() {
console.log("Hello World!!!");
}
//then call it
greetings();
//Result: Hello World!!!
```

- **Objects:** lets us store various keyed collections and more complex entities. 
Objects always have a key-value pair. Keys are the different properties and values are their respective value.

```
const person = {
name: 'Shradha',
age: 21,
address: 'Lucknow',
};
```

## Conclusion
In this blog, we learned about variables and different data types in JavaScript

Winding up now!

Will be back soon. Hope you liked it. Please share your valuable suggestions in the comments.


Thank you for your valuable time & stay tuned!!
