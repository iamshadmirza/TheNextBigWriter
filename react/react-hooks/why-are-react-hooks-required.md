# Why Are React Hooks Required?

If you are new to Web Development or React in particular, you might have heard this buzz word "React Hooks" a lot and might be finding it overwhelming too. You may be having questions like – "Should I learn it? Is it important? Is it even required for a beginner like me?".

While I cannot straight away answer your questions, what I can do is help you understand why do React Hooks exist and what motivated their intoduction to React by the React Team, so that you can decide for yourself whether to learn React Hooks or not.

## Let's get started

Just so that we don't get overwhelmed with all the things that hooks have to offer, let's first define our goal for this article and we'll stick to it.

> In order to answer why are React Hooks required, we will need to understand one thing: What problems do React Hooks solve?

## Background

To get a little context, let's see how React has evolved over the years. Initially when React was release, there was no concept of class in JavaScript and hence it had to be handled by React. Back then, the React Components were created using `React.createClass` API as shown in the code snipped below.

```javascript
const ExampleComponent = React.createClass({
  getInitialState () {
    return {
        // ...
    }
  },
  componentDidMount () {
    // setup
    // add listener for feature 1
    // add listener for feature 2
    // and so on...
  },
  componentDidUpdate () {
    // logic to update state
  },
  componentWillUnmount () {
    // clean up
    // remove listener for feature 1
    // remove listener for feature 2
    // and so on...
  },

  render() {
    return (
      // ...
    )
  }
})
```

### Post ES6 release

With release of ES6, `class` keyword was introduced in JavaScript and it was a new way to create classes in JavaScript. Later, React deprecated the `createClass` API and moved to `React.Component` API. Now we could create React Components using JavaScript native way of creating classes, as shown in the snippet below.

```js
class ExampleComponent extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      // ...
    };

    this.exampleFunction = this.exampleFunction.bind(this);
  }
  componentDidMount() {
    // setup
    // add listener for feature 1
    // add listener for feature 2
    // and so on...
  }

  componentDidUpdate() {
    // logic to update state
  }

  componentWillUnmount () {
    // clean up
    // remove listener for feature 1
    // remove listener for feature 2
    // and so on...
  },

  exampleFunction() {
    //...

    this.setState({
      // ...
    });
  }

  render() {
    // ...
  }
}
```

With this change, React got better than earlier, but it still had some tradeoffs. Everytime while creating a component, it was compulsory to use constructor and call `super(props)` and also `.bind` every function using `.this` keyword in the constructor.

Now these weren't too big of an issue and also these weren't actually React issues because this is how classes worked in JavaScript. But still, there had to be some more efficient way to overcome this problem.

Later, something called as Class Fields were released, which allowed us to directly add properties to the class, without having to use constructor and we no longer needed to `.bind` any methods in the constructor as we could use arrow functions to create methods in class.

```js
class Example Component extends React.Component {
    state = {
        // ...
    }

    exampleFunction = () => {
        // ...
    }
}
```

### React Functional Components

Then with Functional Components, there was a simpler way to create components which did not require any state management or lifecycle methods. Initially, Functional Components were fairly simple. They would take in props and simply render a UI, no other complexity was involved.

```js
function ExampleComponent({ props }) {
  // ...
  render(){
      return(
          // ...
      );
  }
}
```

Now this was the stage, just before hooks were introduced. At this point, there was considerable scope of imporovement in the following areas:

- State Management

  - Event the simplest state management requirements made it compolsory for us to use Class Components instead of Functional Components and it just got messy with complex state management.

- Lifecycle Methods

  - With the use of lifecycle methods, the logic that is related to the component was spread across the component. For instance, in the code snippets above, the actual logic lied in the `exampleFunction`, while the logic of when to call `exampleFunction` was contained in `componentDidMount` and `componentDidUpdate` methods.
  - In addition to this, the lifecycle methods could also contain several other unrelated logic that needs to be executed at a particular lifecycle stage.

- Non Visual Logic was not Reusable

  - Due to the logic of the component being spread across the component and React Components, being a combination of logic and UI, it made reusability of non visual logic (i.e. logic without UI) very complex.

These were the exact problems that motivated the introduction of React Hooks.

## React Hooks

The React team introduced React Hooks to the world at React Conf in late October 2018. In early February 2019, they finally came in React v16.8.0.

React Hooks enables you to use state and other React features, without writing a class, in functional components. It gives combined advantage of Functional Components clean code and Class Components poweful features. And all this is possible because React Hooks are just regular JavaScript functions.

### State Management

React Hooks provide a new way to add and manage state in functional components using `useState` method. The useState method takes in the initial value of a state variable as the only argument and it returns array of two items, the first being the state variable and the second being a function to update that state variable.

```jsx
import React, { useState } from "react";

function App() {
  const [count, setCount] = useState(0);
  // count is state variable
  // setCount is method to update state variable count
  // initial value of count will be 0, as passed in useState

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### Lifecycle Methods

With Hooks, React introduces a new way to connect logic and it's trigger conditions. Instead of writing all the unrelated logic in a block of a lifecycle method which needs to be executed at a particular stage in lifecycle, we can now write any logic independently and pass in the trigger conditions with the help of `useEffect` method.

useEffect lets us perform side effects inside a functional components. It takes two arguments, first being a function and second being an optional array. The function defines which side effect is to be run and the optional array defines when should the effect be triggered or re-run. The effect is triggered whenever the value of the variables passed in the array changes.

```js
import React, { useState, useEffect } from "react";

export default function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### Reusable Non Visual Logic

When it comes to sharing non visual logic across components, there is no inbuilt hook like useState or useEffect which can directly take care of it. But there is a flexibility of creating our own custom hooks, using the different inbuilt hooks as required. This lets us extract the logic out of the component and make it reusable across components.

An example of such logic is handling Authentication State. In apps with authentication, there may be number of functionalities where you need to check for authentication and only allow logged in users to access that functionality. In this scenario, you should not be required to write logic to handle authentication state in multiple components. You can write the logic once inside custom hook and access it across components.

```js
import { useState, useEffect, useContext } from "react";

export default function useAuthListener() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    // setup – add auth state listener
    // logic to handle auth state change
    // clean up – remove auth state listener
  }, []);

  return { user };
}
```

# Conclusion

I think, by now, you would have got a fair idea of how Hooks has enabled us to have better **state management**, **concentrated effect logic** and **reusable non visual logic**.

Since the scope of this article is to understand why are React Hooks required, I've taken the simplest examples of hooks and not gone into detailed explanation of how each of them works. While there is lot more about hooks that makes it powerful and there are many different ways in which we can use hooks, the content covered in this article is enough to answer our primary question: What problems do hooks solve, and why are they required?

In upcoming posts, I'll be writing in detail about different hooks, how they work and how can they be used in our projects.

---

Thank you very much for reading this article. I hope you found it useful and if you did, please do share it with your friends or anyone who may find this interesting.

Connect with me on [Twitter](https://twitter.com/desaihetav) and [LinkedIn](https://linkedin.com/in/desaihetav) to get updates on my new blog posts.