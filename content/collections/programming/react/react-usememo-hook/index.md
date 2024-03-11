---
title: React JS - useMemo hook in React
date: 2022-08-10
Tags: ["programming","react"]
author: Hatim
published: true
keywords: useMemo,memoized,cache,state,react,hook,component
description: In this article we will be convering useMemo Hook which is a great hook for reducing overhead of an react component
image: /images/useMemoHook.jpg
---

# ReactJS - useMemo hook in React

In software development, we're typically fixated on performance improvements and ways to speed up our products so that users have a better experience.

One strategy for improving performance is memoization. We'll examine how React implements it in this article.

## What is Memoized ?

In computer science memoization is a concept used in general when we don't need to recompute value again and again. That is we some how store the current value in the form of cache and when we want some value we simply look from cache instead of recomputing the function again.

**Memoization is a process where it remebers the output for the given sets of input**

If memoized function is called again with the same parameter, it does not re-execute the function. Rather cahce value is return from the function,reducing overhead of executing function.

## Why do we need useMemo Hook?

When an update is made throughout a component's lifespan, React re-renders the component. Due to the way JavaScript handles equality and shallow comparisons, React may notice an unwanted or unexpected change while checking for changes in a component. The React application will needlessly re-render as a result of this update.

## useMemo Hook

The useMemo hook in react takes two parameter :-

1. A function that returns a value.
2. Dependency value.

format:

```js
const memoizedValue = useMemo(functionThatReturnsValue, arrayDepencies);
```

Here the function will only run when the dependency changes

Let's understand useMemo Hook with an example:

```jsx
import React, { useMemo, useState } from "react";
function App() {
  const [todo, setTodo] = useState([]);
  const [count, setCount] = useState(0);
  const someCalculation = expensiveCalculation();

  function expensiveCalculation() {
    let num = Math.floor(Math.random() * 10000);
    for (let i = 0; i < 100000000; ++i) num += i;

    return num;
  }

  return (
    <div>
      <h1> Another Techs </h1>
      <h2> useMemo </h2>
      <div>
        <button
          onClick={() => {
            console.log(todo);
            setTodo((t) => [...t, "new Todo"]);
          }}
        >
          {" "}
          New Todo{" "}
        </button>
        <h3> Todo List:</h3>
        <ul>
          {todo.map((item) => (
            <li>{item}</li>
          ))}
        </ul>

        <div>
          <button onClick={() => setCount((c) => ++c)}>
            Increment Counter
          </button>
          <h2>Expensive Calculation Value </h2>
          <p>{count}</p>
        </div>
      </div>
    </div>
  );
}

export default App;
```

1. In the above example we have two states `count` and `todo`. Since we know that whenever any of the state changes the whole component get's re-renders.

2. The problem here comes if suppose we only change the value of `todo`, then according to the react life cycle the whole component will render.

3. This will also run over `expensiveCalculation` function. This causes overhead in our component. Since whenever our `todo` state changes it will by default run `expensiveCalculation` function even if the `count` state is changed or not.

Here we only want `expensiveCalculation` function to run when the `count` state is changed. For this we some how want to store value some where so that we can access it without running the whole function.

This is where useMemo comes to rescue !!

Let us now understand how this component will run when we use useMemo hook:

```jsx
import React, { useMemo, useState } from "react";
function App() {
  const [todo, setTodo] = useState([]);
  const [count, setCount] = useState(0);
  const someCalculation = useMemo(() => expensiveCalculation(), [count]);

  function expensiveCalculation() {
    let num = Math.floor(Math.random() * 10000);
    for (let i = 0; i < 100000000; ++i) num += i;

    return num;
  }

  return (
    <div>
      <h1> Another Techs </h1>
      <h2> useMemo </h2>
      <div>
        <button
          onClick={() => {
            console.log(todo);
            setTodo((t) => [...t, "new Todo"]);
          }}
        >
          {" "}
          New Todo{" "}
        </button>
        <h3> Todo List:</h3>
        <ul>
          {todo.map((item) => (
            <li>{item}</li>
          ))}
        </ul>

        <div>
          <button onClick={() => setCount((c) => ++c)}>
            Increment Counter
          </button>
          <h2>Expensive Calculation Value </h2>
          <p>{count}</p>
        </div>
      </div>
    </div>
  );
}

export default App;
```

In the above code we have used useMemo hook which takes a **function** and a **dependency value** as an argument.

Now if we change the `todo` state this will cause the component to re-render but this time instead of running `expensiveCalculation` function again here **useMemo** will use the previous value store in cache and hence it will reduce overhead of the overall component.

The `expensiveCalculation` function will only run when the state of `count` changes else it will always use previous whenever the component gets re-renders

## Conclusion

useMemo is the hook which will memoize expensive computation. Once memoized, the hook will return the memoized value without triggering computation given that the **dependency value** is same.

## Reference
- [React Docs](https://reactjs.org/docs/hooks-reference.html#usememo)
- [Shallow Comparison](https://stackoverflow.com/questions/36084515/how-does-shallow-compare-work-in-react)
- [memoization](https://en.wikipedia.org/wiki/Memoization) 
- [Road to React](https://amzn.to/3wFXiFZ)
- [React.js Essentials](https://amzn.to/3TkzxND)
