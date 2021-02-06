# What is props?

---

If you are beginner in react you must have heard about `props` a lot, so let's understand, how is it so important to understand.

## How is it useful?

Before starting we need to understand how react works. So React is a component based `JavaScript` Library where we can divide our project into various reusable components.

For example the below code is your main `App.js` file which you can see when we create a project using create-react-app

```JavaScript
import "./styles.css";
import Greet from "./Greet";

function App() {
  var Humans = [
    {
      id: 1,
      name: "Ashray",
      age: 22
    },
    {
      id: 2,
      name: "Aman",
      age: 25
    }
  ];

  return (
    <div className="App">
      <Greet Humans={Humans} />
    </div>
  );
}
export default App;
```

In the above code we can see that I have created one `Component`.

- Greet

There is an array of object's with key value pair of `id`, `name` and `age`

1. Now let's come to our main topic **Props** it stands for **properties** it's not mandatory to write only `props` we can name it anything we wish for.

2. It gives a way to pass data from one component to other components.

Now we understood how we have passed the **Humans** props now it's time to destructure:

Destructuring is an ES6 feature to extract multiple pieces of data from an array or object and assign them to their own variables.

Let us understand with an example consider the Object give below

```JavaScript
var Humans =
    {
      id: 1,
      name: "Ashray",
      age: 22
    }
```

Now if we want to access _Ashray_ or the age property we can do by `console.log(Humans.name)` & `console.log(Humans.age)` which will give the output **Ashray** & **22**

## Now let's try to do the same thing in another way

```JavaScript
const { id, name, age} = Humans

console.log(id);

console.log(name);

console.log(age);
```

This will also give us the same result i.e.

- 2
- Ashray
- 22

In the above example we destructured the Humans Object and accessed it without using the dot property.

The same thing we are going to do it in React for destructuring props

As you can see we have passed Humans as a props `<Greet Humans={Humans}` and now we can destructor the `Humans` props in our `<Greet>` component.

```JavaScript
import React from "react";

const Greet = ({ Humans }) => {
  return (
    <div>
      {Humans.map((human) => (
        <div>
          <h1>Hello {human.name}</h1>
          <h2>Age: {human.age}</h2>
        </div>
      ))}
    </div>
  );
};
export default Greet;
```

In the above code we have destructored Humans **props** to display in the view we are using array method `map` which is displayed as `{Human.name}` and `{Human.age}` to give us the output as shown below:

> **Hello Ashray**
> Age: 22
> **Hello Aman**
> Age: 25

![blog.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612520834858/mwxloLPvm.png)

## How is it passed?

One thing to keep in mind is Props are passed from Parent component to Child Component. In above example Parent Component is `App.js` and Child Component is `Greet.js`.

- We are passing **Humans** `props` from Parent to child component.

# Conclusion

---

- **Props** main purpose is to pass data from one component to another
- It works only one way i.e. Parent component to Child component

⚡ Happy learning!
