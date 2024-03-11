---
title: React JS - useReducer hook in react
date: 2022-07-17
author: Hatim
published: true
Tags: ["programming","react"]
description: In article we will dive into what is useReducer hook and how to use useReducer hook to write complex logic of the react component
keywords: useReducer,hook,react,reducer,state,dispatch,function
image: /images/usereducer.png
---

# ReactJS - useReducer() hook in react

Hooks in React introduced a new method of building and thinking about React apps. So far, one of the most popular hooks among developers is **useReducer**, which allows us to manage certain complex state manipulations and updates, and this is what we'll learn about in this post.

We are all familiar with the two basic hooks used for state management in React.
They are as follows:

- useReducer and
- useState

You may have heard of or used the **useState** hook; if not, you can read React's official hooks documentation here.

Have you ever struggled to select a state management library to maintain and handle a global state in a React app? What if you need to manage more complex data structures or run any side effects? Thinking about these ideas is difficult and time-consuming.

## What is a Reducer ?

Well to understand useReducer hook first let's try to understand what is a reducer. As the name suggest a **reducer** is something which reduces something to some form. Ringing some bell ??

Well first thing that come to my mind when I hear term **reducer** is Javascript `Array.reducer()`. Which reduces the array to certain form based on the function passed to it.

**For Example:**

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 9];

const sum_of_array = arr.reduce((acc, num) => {
  return acc + num;
}, 0);

console.log(sum_of_array);
```

As you can see in the code above we have created array `arr` and we want to get total sum of each element in the array. For this we are using `reduce` function which take a function as an argument. In the function we apply logic of our reducer which in our case is the sum of element. After function is passed it take an initial value which in our case is zero.

Our reducer function get two argument:

- `acc`: Accumulator which hold the value of previous state,
- `num`: Each value in the array.

Now that you have understand the basic function of reducer let us now under useReducer hook.

## What is useReducer hook in react ?

**useReducer** hook pretty much work similar way as Javascript **reducer** works. useReducer hook takes two thing a **reducer function** and initial value similar to our Javascript reducer.

A reducer function receives two argument current `state` and `action` (triggered by some event such as button click) and return the new State.

So if you want to sum the element which is in your current state you will be using following logic:

```jsx

useReducer((state,action)={
  return state+action
},0)

```

One question may arise that how does this useReducer hook get triggered?

The useReducer hook just like **useState** hook return two element. The first is **current state** and the second is **dispatch** function. This dispatch function is what triggers our useReducer hook.

Following is how you will normally declare a useReducer hook:

```jsx
const [state, dispatch] = useReducer((state, action) => {
  return sum + action;
}, 0);
```

Now let's look at some real life example on how useReducer hook works and how it reduces complexity which occur if we use useState hook.

### useReducer hook example

```jsx
import { useReducer, useRef } from "react";
function App() {
  const inputRef = useRef();
  const [items, dispatch] = useReducer((state, action) => {
    switch (action.type) {
      case "add":
        return [...state, action.item];
      case "remove":
        return state.slice(1);
      default:
        return state;
    }
  }, []);
  return (
    <div>
      <div>
        <h2> Items </h2>
      </div>
      <input ref={inputRef} />
      <ul>
        {items.map((item, index) => (
          <li key={index}>
            <span>{item}</span>
          </li>
        ))}
      </ul>
      <button
        onClick={() => {
          dispatch({ type: "add", item: inputRef.current.value });
        }}
      >
        {" "}
        Add{" "}
      </button>
      <button
        onClick={() => {
          dispatch({ type: "remove" });
        }}
      >
        {" "}
        Remove{" "}
      </button>
    </div>
  );
}

export default App;
```

In the above exampel we have simple _todo_ app which add the item in the list and remove the last item form the list by clicking on **Add** and **Remove** button respectively.

Inside the **App** component we created our **useReducer** hook which gives us two thing:

1. **items(crrent state)** which is our list of item.(when the component mounts this list is empty)

2. dispatch function

We have also passed the logic of what is reducer function do when it gets triggered which is simply add or remove the item from the list based on the type which get provided.

Also to make things simpler I have also used the **useRef** hook which will directly give use the value from the input field.

Next we have declared two button **Add** and **Remove**. Whenever user clicks on the button our `dispatch` function get called and calls our `useReducer` logic.

- **The reducer returns a new array that contains all the old elements in addition to the new one at the end when it receives the "add" action.**

- **But when the "Remove" actiion is triggered the reducer remove the first item fom our current state(or item) and return new state**

  The `actions` we do in our app are objects with a type property and some related data, but you can make them out of anything (plain strings, numbers, more complex objects, etc).

## When to use the `useReducer` hook

You'll most likely deal with more complicated state transitions when your application gets bigger, at which case useReducer will be more advantageous.

When state changes grow so complex that you want to have one place to manage state, like the render function, useReducer becomes more crucial because it offers more predictable state transitions than useState.

A reasonable rule of thumb is that useReducer is usually preferable whenever you need to handle a complicated object, such as with arrays and additional primitives, as opposed to managing primitive data, such as a text, integer, or Boolean.

If you learn better visually, the video below provides a thorough explanation and real-world examples of when to utilise the usage.

## Conclusion

The useReducer hook is a fantastic addition to the React framework that makes updating our component's state simpler, predictable, and organised and facilitates data sharing between components.

Because you can now easily transmit dispatch down instead of conventional callbacks, it enables you to enhance the efficiency of the components that initiate deep updates.

And even if you only remember one thing from this post, it should be that useReducer gives us the ability to specify how we update our state value.
