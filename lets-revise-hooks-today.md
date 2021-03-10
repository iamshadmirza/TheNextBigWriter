Hello Everyone

I'm am Minhaj Ahmad Khan and I'm a Front-End developer. After a good response to my first blog. Thanks for your like and support so here I am back with a new blog I am sure you like it.

## Why Hooks?

Until now if you started writing a functional component and ran into a situation where you needed to add a state you would have to convert the component to a class component that is simply because the state could only be used in class components That where Hooks comes into the picture.

## What is Hooks?

A Hook is a special function that lets you “hook into” React features. For example, useState is a Hook that lets you add React state to function components.

So In this blog, we cover all major Hooks where we cover everything about these Hooks in depth.

I am assuming readers have intermediate knowledge of React.

So what we are going to cover

## Rules of Hooks

- Only call Hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions.

- Only call Hooks from React function components. Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks — your own custom Hooks. We’ll learn about them in a moment.)

## Basic Hooks

- useState

- useEffect

- useContext

## Additional Hooks

- useReducer

- useCallback

- useMemo

### State Hook (useState)

State Hook(useState) is a hook that let you add react state to functional components.

To understand State Hooks(useState) we are going to create a Simple Counter

Step 1 Create a Function Component called `Counter.js`

```
import React from 'react';


const Counter = () =>{
 }
  return (<div>  </div>)

}
export default Counter
```

Step 2 We Need a State Property and initialize To 0

```
import React,{useState} from 'react';


const Counter = () =>{
  const [count,setCount] =useState(0)
  }
  return (<div></div>)

}
export default Counter
```

Step 3 We need a Function that will Increment, Decrement the State.

```
import React,{useState} from 'react';
const Counter = () =>{
  const [count,setCount] =useState(0)

  const handleIncrement=()=>{
   setCount(count + 1)
  }
  const handleDecrement=()=>{
    setCount(count - 1 )
   }
  return ( <div>
    <h1>{count}</h1>
    <button onClick = {handleIncrement}>Increment</button>
    <button onClick = {handleDecrement}>Decrement</button>
    </div>)
}
export default Counter
```

We import useState Hook from react.
Inside Counter Component We declare a variable by calling useState.
Which returns a pair of value `count,setCount` we are calling count because it holds Number.

The second returned item is itself a function. It lets us update the count so we’ll name it setCount.

When the user clicks on buttons, we call setCount with a new value. React will then re-render the Counter component, passing the new count value to it.

### Effect Hook (useEffect)

If you have been working with the class components we would have performed side effects, for example updating dom, fetching data from API.
Since the render method is too early to perform side effects you have to make use of the life cycle method.

- The Effect Hook lets you perform side effects in function components.

- It is able to handle what `ComponentDidMount`, `ComponentDidUpdate`, `ComponentWillUnmount` are able to do the in class component.
- `useEffect` run after every render

- The second argument of `useEffect` is the array of values that the array depends on. if the value does not change between rendering the effect simply not run this is called dependency array.

Now let's see how to use

So basically we are going to fetch quotes from API using useEffect hooks and display the first element of the array as simple as that.

Step 1 Create a functional component called `Quotes.js`

```
import React,{useState,useEffect} from 'react'
import axios from 'axios'


const Quotes = () => {
    const [quotes ,setQuotes] =useState([])
    useEffect(() => {
        const data =axios.get('https://type.fit/api/quotes').then((res)=>{
         setQuotes(res.data)
        }).catch((e)=>{
         console.log(e)
        })
    },[])
    const  random = Math.floor(Math.random() * quotes.length)
    return (
        <div style={{ height: '200px', width: '600px', border: '1px solid red', background:'#e1f5fe'}}>
            <h1>{quotes[0] && quotes[random].text}</h1>
            <h1>By {quotes[0] && quotes[random].author}</h1>
        </div>
    )
}

export default Quotes

```

We are basically copy the `componentDidMount` with `useEffect` hooks by simple passing in empty array [] as a second argument to `useEffect`

We are imported `useEffect` from the React library and we have added my effect under the useState line.

`useEffect` accepts a function as it’s the first argument. The function will handle side effects.

By passing `[]` as a second argument we are telling react that out `useEffect` function does not depend on any values `props` or `state`.

### useContext

Context provides a way to pass data through the component tree without having to pass it down manually at every level

![useEffect.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609762643281/Yq3P_r__z.png)

In this example we pass data from `App Component` to `ComponentE` use useContext

Let's see how

```
import React,{useState,createContext} from 'react'
import ComponenetA from './ComponenetA'
export const NameContext = createContext()

const AppComponent = () => {
    const [name,setName]=useState("Minhaj ahmad khan")
    return (
        <div>
            <NameContext.Provider value={'Minhaj ahmad khan'}>
                <ComponenetA />
            </NameContext.Provider>
        </div>
    )
}

export default AppComponent


```

So here we are export and creating a context `export const NameContext = createContext()` after that we need to provide the context with value.
The provider must wrap with the children component for the value to be available.

```
import React,{useContext} from 'react'
import {NameContext} from './App-Component';

const ComponentE = () => {
    const userName = useContext(NameContext)
    return (<div style={{ height: '200px', width: '600px', border: '1px solid red', background: '#e1f5fe' ,margin:'20px'}}>
        <h1>useContext Example</h1>
        <h3> hello My Name is  {userName} </h3>
    </div> )
}

export default ComponentE

```

Here we are importing the required context after that we are calling `useContext` function and pass in context as its argument which returns the context value

### useReducer

useReducer is a hook that is used for state management. It is an alternative to `useState`.

Similar to useState but gives you more control to manage the state.
It takes a reducer function and initial state as arguments and returns the state and dispatch method.

Let's see in code which makes more sense

```
import React, { useReducer } from 'react'
const initialState = 0;
const reducer = (state, action) => {
    switch (action) {
        case 'increment':
            return state + 1;
        case 'decrement':
            return state - 1;
        case 'reset':
            return state = 0;
        default:
            return state
    }
}

const CounterReducer = () => {

    const [count, dispatch] = useReducer(reducer, initialState)
    return (
        <div style={{ height: '200px', width: '600px', border: '1px solid red', background: '#e1f5fe', margin: '20px' }}>
            <p>Reducer Example</p>
            <h3>{count}</h3>
            <button onClick={() => dispatch('increment')}>Increment</button>
            <button onClick={() => dispatch('decrement')}>Decrement</button>
            <button onClick={() => dispatch('reset')}>Reset</button>

        </div>
    )
}

export default CounterReducer;

```

When you are dealing with multiple state transition it is good to useReducer it makes so easy to maintain state.

It's always a good practice to use `useReducer`when the state depends on the previous one.
It will give you a more predictable state transition.

### useCallback

To underStand `useCallBack` we need to understand a little bit of performance optimization.

Let's see in code

```
import React,{useState} from 'react'
import Button from './Button'
import Number from './Number'
import Title from './Title'

const App = () => {
    const [number,setNumber] =useState(0)
    const [numberTwo,setNumberTwo] =useState(0)

   const    handleIncrement = ()=>{
       setNumber(Number + 1 )
    }
   const    handleDecrement = () => {
        setNumberTwo(NumberTwo - 1)
    }
    return (
        <div style={{ height: '300px', width: '600px', border: '1px solid red', background: '#e1f5fe', margin: '20px' }}>
            <Title/>
            <Number number={number} />
            <Button handleClick={handleIncrement}>Increment</Button>
             <Number number={numberTwo}/>
            <Button handleClick={handleDecrement}>Decrement</Button>
        </div>
    )
}
export default App

```

App Component is basically a container for other components.

If you see the `JSX` we have a total of 5 components where 2 of the component is reused with different props.

Let's just quickly see all the component code and move forward.

```
import React from 'react'

const Title = () => {
    console.log('title compoent')
    return (
        <div>
            <h1>useCallback Hooks</h1>
        </div>
    )
}

export default Title
```

In the Title component we simply return title in `h1` tags.

```
import React from 'react'

const Number = (props) => {
    console.log('counter compoent')
    return (
        <div>
           <h3>{props.count}</h3>
        </div>
    )
}
export default Number

```

Here we have a Number component to show the current number.

```
import React from 'react'

const Button = (props) => {
   console.log(`button component  -- ${props.children} `)
    return (
        <div style={{display:'block'}}>
           <button onClick={props.handleClick}>{props.children}</button>
        </div>
    )
}

export default Button

```

Last, Here we have Button Component to increment and decrement the number.

Let's Run our code and see what happens.

![usecallback.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609934658848/YUGsjz53T.png)

UI is pretty terrible but that's not our concern here. So you can see on logs every component is rendered as expected.

Now let's increment the number and see what happens.

![increment.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609934671483/VQrzMhXS5.png)

As we can see in logs every component is re-rendered. This is really not a problem with a few components that has a simple logic.

Consider a scenario where lots of components and updating a single component is going to rerender all the components. You would then start facing performance issues.

So here we have to figure out any way to rerender only those components who need to re-render.

In our example, the number and button component for increment should be rerendered, and the rest component doesn't need to rerender.

Here `React.memo` comes into the picture.

`React.memo` is a higher-order component that will prevent a functional component from being rerendered if its props and state do not change.

`React.memo` has nothing to do with hooks. It has been a feature since React version 16.6.0.

Now let's see how we can use `React.memo`

To use `React.memo` we only need to exporting wrap our component `React.memo` as simple as that

Let's wrap all three components.

```
import React from 'react'

const Title = () => {
    console.log('title compoent')
    return (
        <div>
            <h1>useCallback Hooks</h1>
        </div>
    )
}

export default React.memo(Title)
```

`Title` component

```
import React from 'react'

const Button = (props) => {
   console.log(`button component  -- ${props.children} `)
    return (
        <div style={{display:'block'}}>
           <button onClick={props.handleClick}>{props.children}</button>
        </div>
    )
}

export default React.memo(Button)

```

`Button` component

```
import React from 'react'

const Number = (props) => {
    console.log('counter compoent')
    return (
        <div>
           <h3>{props.number}</h3>
        </div>
    )
}

export default React.memo(Number)

```

`Number` component

Now let's run and our code and see what happen now

![usememo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609935101745/uqhRBHVOv.png)

As we can see on logs title component not rerendered but it's still not right.

Because button component for decrement still rerendered

**Why is happening **

Let's see our code and try to understand what is happening.

The first Component is the Title component it has no props and no state of its own hence does not rerender.

After that Number and Button component for increment are related.

Number component accept `number` as a props and Button component accept `handleIncrement` as a props. Which is depend on ` setNumber(number + 1 )` as you can see.

So when the number Increment both these components will rerender.

But what we see here decrement button also rerender. Now this is because a new decrement function is created each time the parent component rerender.

We know when we are dealing with function we always have to consider reference equality.

For example, the two functions have exactly the same behavior it does not mean they are equal to each other that means the function is not the same before and after rerender.

Here the function is props `React.memo` sees the props have changed will not prevent the rerender.

So How do we fix this?

How do we tell react that there is no need to create a new decrement function.

And the Answer is useCallBack hook

**What is useCallback hook**

useCallback is hook that will return memorized version of the callback function.

That will only change if the dependencies have changed.

In simple words based on our example `useCallback` hook will memorize the decrement function and return that if the number is not decremented.

If the number is decremented that the dependency has changed only then a new function will return.

Let's see how to implement `useCallback`.

First import `useCallbak` from react and then we need to call `useCallback`.

Which accepts a callback function as its first argument and then an array of dependencies as its second argument.

Now both the function, we return the memorized function which we passed as a props the child component.

```
import React,{useState,useCallback} from 'react'
import Button from './Button'
import Number from './Number'
import Title from './Title'

const ParentCompoent = () => {
    const [number,setNumber] =useState(0)
    const [numberTwo,setNumberTwo] =useState(0);

   const    handleIncrement = useCallback(()=>{
       setNumber(number + 1 )
   },[number])

   const    handleDecrement = useCallback(()=>{
            setNumberTwo(numberTwo - 1)
   },[numberTwo])


    return (
        <div style={{ height: '300px', width: '600px', border: '1px solid red', background: '#e1f5fe', margin: '20px' }}>
            <Title/>
            <Number number={number} />
            <Button handleClick={handleIncrement}>Increment</Button>
            <Number number={numberTwo} />
            <Button handleClick={handleDecrement}>Decrement</Button>
        </div>
    )
}
export default ParentCompoent

```

Now time to test this out

![result.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609935724643/hNRMNyAfW.png)

Cool here only Counter and button components for increment are rerenderd. That all about useCallback hook.

### useMemo

`useMemo` hook is also used for performance optimization.

Let's understand with Example.

Here we have a simple `handleGrade` function which is basically calculate whether the student percentage are first division or second division.

Which takes no time to execute but in real world will take some time for execution.

That is not so good with performance it could anything like fetching thousand of data or mapping that array.

So here we create some delay in `handleGrade` by using `while loop`

```
import React,{useState} from 'react'

const PersonAge = () => {
    const [studentName,setName] =useState('Urooj ahmad')
    const [percentage,setPercentage] =useState(55)
    const [studentAge,setStudentAge] =useState(20)

    const  handleIncreaseAge = ()=>{
        setStudentAge(studentAge + 1 );
    }
    const handleIncreasePercentage = () => {
       setPercentage(percentage + 1);
    }

    const handleGrade = () =>{
        let i = 0
        while(i <300000000)i++
      if(percentage >= 60){
          return <span>First Division</span>
      }
     return <span>Second Division</span>

    }
    return (
        <div style={{ height: '200px', width: '600px', border: '1px solid red', background: '#e1f5fe', margin: '20px' }}>
            <h4>Student Name {studentName}</h4>
            <h4>Student Percentage {percentage}% <button onClick={handleIncreasePercentage}>Increase percentage</button> <span>{handleGrade()}</span></h4>
            <h4>Student Age {studentAge} <button onClick={handleIncreaseAge}>Increase Age</button></h4>
        </div>
    )
}

export default PersonAge

```

Becasue of the `handleGrade` function there are now considerable amount of delay before the UI update.

Which is expected if the number is change react need to check whether the student percentage are first division or second division.

But if you click the `Increase Age` button there still there is a delay with UI update.

Why is Increase Age slow as well

That is because every time state updates the compoent rerenders and when the compoent rerender the function `handleGrade` is called again which takes time to execute. Even we are updating the Increase age the UI update is slow.

What we need is a way to tell react not to recalculate the value which we don't need especially which takes some time to execute.

This is the ideal situation to `useMemo` hook.

### useMemo

`useMemo` is a hook that will only recalculate the cached value when one of the dependency has changed.

Let's see how to use

```
import React,{useState,useMemo} from 'react'

const PersonAge = () => {
    const [studentName,setName] =useState('Urooj ahmad')
    const [percentage,setPercentage] =useState(55)
    const [studentAge,setStudentAge] =useState(20)

    const  handleIncreaseAge = ()=>{
        setStudentAge(studentAge + 1 );
    }
    const handleIncreasePercentage = () => {
       setPercentage(percentage + 1);
    }

    const handleGrade = useMemo(()=>{
        let i = 0
        while(i <300000000)i++
      if(percentage >= 60){
          return <span>First Division</span>
      }
     return <span>Second Division</span>
    },[percentage])

    return (
        <div style={{ height: '200px', width: '600px', border: '1px solid red', background: '#e1f5fe', margin: '20px' }}>
            <h4>Student Name {studentName}</h4>
            <h4>Student Percentage {percentage}% <button onClick={handleIncreasePercentage}>Increase percentage</button> <span>{handleGrade}</span></h4>
            <h4>Student Age {studentAge} <button onClick={handleIncreaseAge}>Increase Age</button></h4>
        </div>
    )
}

export default PersonAge

```

![usememo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609944597085/eMZLEig-y.png)

The way `useMemo` works is very similar to `useCallback`. First we need to import `useMemo` from react.

After that call the `useMemo` as the first argument, we pass a callback function whose return value needs to be cashed.

The second argument we need to pass dependencies our function is depend on `percentage`.

That's means whenever `percentage` changes we are telling to react recalculate the value and do not use the cached value.

`useMemo` returns the cached value which we assgin to the variable `handleGrade` now all set let's run our code.

Now there is no delay on `Increase Age ` and the UI update is very faster.

This is because React is now using cached value of `handleGrade` to display weather the student percentage is the first divison or second division.

That all about `useMemo`

That's it, I hope it was helpful to you. Thanks for reading you can follow me on Twitter

[Minhaj ahmad khan](https://twitter.com/MinhajAhmadKha7)
