# All the ways to define functions in JavaScript

## Introduction

Function is a set of statements or block of code to perform a specific task and return a value.They are reusuable and make your program modular and efficient.

Below are few of the ways by which you can define a function in JS.

### Defining a Function

#### 1. Function Statements / Function Decalaration / Function Definition

This is the most common way to define a function in JS. The definition starts with the keyword **function**, followed by the **name** of the function where the naming convention is similar the variables - they can contain letters, digits, underscores and dollarsigns and are mostly written in **camelCase**. The name is followed by a set of parenthesis which is used to pass **arguments**. After this comes the curly brackets which contains the **body** of the function.

![Function Statements](https://res.cloudinary.com/dyyr6kwla/image/upload/v1586085463/define-functions/define-function-statement_akc1qj.svg)

A function always has to return a value. If nothing is returned explicitly, it will return **undefined**. A function defined this way has access to the global and the local variables. These types of functions are always **hoisted** to the top of the enclosing function or global scope, which is the reason why they can be invoked before their declaration.

#### 2. Function Expression

This is a way by which you can define function as an expression. A function expression has almost similar syntax as function definition. The difference in the syntax comes with that the **function name** can be omitted and it can be created as an **anonymous function**. A function expression is never hoisted, so it cannot be invoked before it is defined. It can also be used as an **IIFE (Immediately Invoked Function Expression)**, a **closure**, and **function as an argument**.

![Function Expression](https://res.cloudinary.com/dyyr6kwla/image/upload/v1586105772/define-functions/function-expression_mskfpa.svg)

#### 3. Arrow Functions

Arrow Functions are the most latest way of defining Functions. They are one of the features of ES6 (EcmaScript- 6). These are always anonymous functions.They do not create their own **this** value. They are also known as **fat arrow** functions.

![Arrow function](https://res.cloudinary.com/dyyr6kwla/image/upload/v1587207495/define-functions/arrow-functions_hcwk94.png)

They make the code more concise, simplify the scope of the function and the **this** keyword. These function do not have any binding for **this**.In a classic function expressions, the this keyword is bound to different values based on the context in which it is called. With arrow functions however, this is lexically bound. It means that it uses this from the code that contains the arrow function.

For example, look at the setTimeout function below:

![Arrow Function Scope](https://res.cloudinary.com/dyyr6kwla/image/upload/v1587207743/define-functions/arrow-function-scope_bhj4yc.png)

----

That's all for the article. Thanks for reading it. Please comment your feedback and suggestions.
