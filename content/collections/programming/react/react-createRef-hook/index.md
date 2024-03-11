---
title: React JS - A complete guide to React refs
date: 2022-07-04
author: Hatim
published: true
Tags: ["programming","react"]
keywords: react,reactjs,refs,dom,component,React,Refs
description: Learn how to use React refs, and why it's important to use them only when React can't handle a function call through its own methods.
image: /images/lautaro-andreani-UYsBCu9RP3Y-unsplash.jpg
---

# ReactJS - A complete guide to refs and useRef() in React

We will talk about how to directly manipulate DOM elements in React in this tutorial.

Although the React Framework constructs your components and abstracts your code from DOM manipulation, developers can still access it. There are only a few situations where it might be required. React offers a refs escape route as a result.

refs is a function used by components to access the DOM. To enable access to the element from wherever within your component without using properties and everything, you merely need to attach a ref to it in your application.

refs can be used to gain direct access to React elements and to interact with them via callbacks. refs should only be used when state and props are unable to deliver the desired interaction.

## React refs

In React, references are denoted by the abbreviation refs. It is comparable to React's keys. It is an attribute that enables the storage of a reference to certain React elements or DOM nodes. It gives instructions on how to interact with React elements and DOM nodes. It is used when we don't want to use props but still want to update the value of a child component.

Similar to many other UI technologies, React provides a means to reconsider a view as the outcome of a component's state. This is a significant departure from how we typically create applications.

We find out how simple frontend problems that used to be challenging to us can be solved if we become familiar with some of these new ideas. This gain is partially attained by building views using the abstraction techniques that React and JSX expose rather than the DOM standard methods.

These escape routes are called refs, and they give us direct access to DOM properties. React often re-renders the component for us in order to refresh the data on the screen using state. However, there are some circumstances where dealing with the DOM properties directly is necessary, and that's where refs come in handy.

This might be demonstrated by automatically focusing a text box as a component renders. We can use refs to access the DOM directly and focus the text box for us whenever the component renders on the screen because React doesn't offer a simple mechanism to do this.

We'll look into why React, a framework designed to keep your code away from DOM manipulation, leaves the door open for developers to access it in this post.

## Creating React refs

Since React recommends functional components, and general practice is to follow the Hooks way of doing things we will be using `useRef(null)` to create refs intead of `createRef()` which were used in class-based component in the past.

Let's start with the simple example of grabing a node element using refs.

```jsx
import React, { useRef } from "react";

const App = () => {
  const buttonRef = useRef(null);
	return(
	<div>
	  <button onClick={()=> console.log("Hello")} ref={buttonRef}>
		  Click Here
		</button>
	<div>
	)
}

export default App;

```

Here, the `<button>` statement is actually how JSX calls `React.createElement("button")` does not truly represent an HTML button element; rather, it represents a React element.

By generating a React reference and sending it to the element itself, you may access the real HTML element.By using `buttonRef.current`, we may access the actual HTML element at any point in the component's lifecycle.

At this point, we are aware of how to access DOM nodes within a React component. Let's look at some of the circumstances in which this can be helpful.

## Using React refs

By invoking focus() on the node instance, you can programmatically gain focus in an element. The simplest approach to do this with React is to build a ref and manually perform it when we think it's appropriate because the DOM exposes this as a function call.

```jsx
import { React, useRef, useEffect } from "react";

const App = () => {
  const inputRef = useRef(null);
  useEffect(() => {
    console.log(inputRef.current); //Logs "HTMLInputElement"
    inputRef.current.focus();
  }, []);
  console.log(inputRef.current); //Logs undefined

  return (
    <div>
      <input ref={inputRef} type="text" />
    </div>
  );
};
```

During initial rendering, React still determines what the component's output is, therefore no DOM structure is produced. As a result, during initial rendering, `inputRef.current` evaluates to undefined.

When the input element has already been established in DOM, the `useEffect(callback, [])` hook performs the callback immediately after mounting. Because the DOM is guaranteed to be built, the callback function of the `useEffect(callback, [])` is the correct place to access inputRef.current.

## When to Use React's Refs

Refs are applicable in the following situations:

- when handling focus, text selection, or media playing requires DOM measurements.

- while incorporating DOM libraries from outside sources.

- In order to start imperative animations, it is used.

- In callbacks, it can also be used.

## When not to use React's Refs

- For anything that can be done declaratively, it should not be used. For instance, you should supply an isOpen prop to a Dialog component rather than calling the open() and close() methods on it.

- You must refrain from using the Refs excessively.
