---
title: ReactJS - Understanding Higher Order Components in React
date: 2022-06-16
Tags: ["programming","react"]
author: Hatim
published: true
description: In this course, we will learn about higher-order components, including their syntax and applications. We will create a higher-order component from an existing React component in the process. You will learn the fundamentals of higher-order components and how to construct them at the end of this lesson.
keywords: react,component,higher,order,higher-order,higher order,function,HOC
image: /images/lautaro-andreani-UYsBCu9RP3Y-unsplash.jpg
---

# ReactJS - Understanding Higher-Order Components in React

**A function that takes a component and returns a new component is known as a higher-order component.**React's higher-order components (HOCs) were inspired by JavaScript's higher-order functions. A HOC is a sophisticated approach to reuse logic in React components. It's a pattern derived from the compositional nature of React. Another function is passed as an argument to a higher-order component function. The greatest example to understand this is the map function. The basic purpose is to break down the component logic into smaller, more manageable functions that may be reused as needed.

These functions are **pure** in the sense that they accept data and return values based on that input. Higher order functions are re-run with different data input if the data changes. We don't need to edit the HOC if we wish to update our returning component. All we have to do now is update the data our function is working with.

In React.js, a higher-order component (HOC) is an advanced mechanism for reusing component logic. The React API does not include Higher-Order Components. They're the pattern that React's compositional nature produces. A higher-order component translates a component into another component, while the component converts props into UI.

**Reason for using Higher Order Component:**

- Simple to use

- Get rid of the need to copy the same logic across all components.

- It improves the readability of the code.

## Higher-Order Functions in JavaScript

Let's take a quick look at higher-order functions in JavaScript before diving into HOCs in React. Understanding them is crucial to comprehending our main topic.

In JavaScript, higher-order functions take one or more functions as arguments and return another function. They give us the ability to abstract over actions rather than just values. They come in a variety of shapes and sizes, and they assist us in writing less code when working with functions and even arrays.

Composition is the most intriguing aspect of employing higher-order functions. Small functions that handle a single piece of logic can be written. Then, by combining the various tiny functions we've constructed, we may create large ones. This decreases the number of defects in our code and makes it much easier to read and understand.

Some of these functions are already included in JavaScript. The following are some instances of higher-order functions:

- `forEach()`: This code iterates over every element in an array, but it does not update or mutate the array, and it returns undefined.

- `filter()`: This function examines each element in an array to see if it matches the criteria set in the filter method, and then returns a new array with the elements that do.

- `map()`: This method modifies an array by applying a function to all of its elements and then constructing a new array from the values returned.

- `reduce()`: For each value of the array, this method runs the specified function (from left to right).

##### An Example of Higher-Order Functions

```js
function add(x, y) {
  return x + y;
}

function sub(x, y) {
  return x - y;
}

//Define a function that take function as an argument
function operation(x, y, op) {
  return op(x, y);
}

operation(5, 3, add); // 8
operation(5, 3, sub); // 2
```

In the above example, we have to define a higher-order component `operation` which takes values and operation to be performed on that value as an argument which in our case are two `add` and `sub`.

## Higher Order Component (HOC) in React

A higher-order component (HOC) is a React component that allows you to reuse logic.
Components accept one or more parameters and return a new, updated component.
Is this anything you've heard before? They are analogous to higher-order functions, which accept as an argument several functions and return a new function.

HOCs are often used to create components with shared behavior in a way that connects them in a way that differs from the standard state-to-props paradigm.

The React API does not include Higher-Order Components. They're the pattern that React's compositional nature produces. A higher-order component translates a component into another component, while the component converts props into UI. Redux's connect and Relay's createContainer are two examples of HOCs.

### Structure Of Higher Order Component (HOC)

The structure of a HOC is similar to that of a higher-order function:

- It's a Component

- As an argument, it uses another component.

- Then a new component is returned. It can render the original component that was supplied to it with the component it returns.

```jsx
import React from "react";

const withHOC = (WrappedComponent) => {
  return <div>{<WrappedComponent />}</div>;
};
```

**Note: the name of the higher-order component (HOC) should always start with the prefix "with".**

### Example

The simplest example to learn how higher-order component works are showing a loader while the component is waiting for data.

When creating a web application, we almost always need to employ a loader of some kind that is displayed while a component waits for data to be supplied to its props. We could render the loader with an in-component solution, which would work, but it wouldn't be the most elegant option. Better would be to write a common HOC that can track those props; and while those props haven’t been injected or are in an empty state, it can show a loading state.

First, let's see how we will normally write this function without HOC

```jsx

const ListData = ({data}) => {
	return(
		<ul>
			{
				data.map((item) => (
				<li>
					<h1> item </h1>
				</li>
				))
			}
		</ul>
	)
}

const App = () => {

	const useState{data,setData} = useState(null);
	const useState{loading,setLoading} = useState(true);

	useEffect = (() => {
			fetch("https://example.com/dummydata")
			.then((json) => json.json())
			.then((repos) => {
				setData(repos)
				setLoading(false);
			)

	})

	if(loading) return <div> Loading Data Please Wait </div>;
	if(!data) return <div> No data </div>;
	if(!data.length) return <div> Data is Empty </div>

	return <ListData data={data} />
}

export default App;

```

In the above example, we first fetch the data from a given URL and this display the data in the form of a list. But Before displaying the data we first check:

- weather the data fetched or not?
- weather the website returned any data or not? and
- if data is returned is it empty or not?.

If all of the above condition is satisfied then only we display the `ListData` component.

Now suppose instead of listing data we want to display images. The process here will be the same, we will check:

- weather the data fetched or not?
- weather the website returned any data or not? and
- if data is returned is it empty or not?.

After all these conditions get satisfied we display component `ListImages`

```jsx


const ListImages = ({data}) => {
	return(
		<ul>
			{
				data.map((url) => (
				<li>
					<img src={url} />
				</li>
				))
			}
		</ul>
	)
}

const App = () => {

	const useState{data,setData} = useState(null);
	const useState{loading,setLoading} = useState(true);

	useEffect = (() => {
			fetch("https://example.com/dummyimages")
			.then((json) => json.json())
			.then((repos) => {
				setData(repos)
				setLoading(false);
			)

	})

	if(loading) return <div> Loading Data Please Wait </div>;
	if(!data) return <div> No data </div>;
	if(!data.length) return <div> Data is Empty </div>

	return <ListImages data={data} />
}

export default App;

```

Now if you look closely at both the code snippets above you will notice that in both the cases the validation part is common
and the only thing which changes is the displaying component. Therefore to avoid this duplication of code and make the code more readable we can use High Order React Component (HOC).

Now let's see how the Higher-Order React Component (HOC) will help use avoid duplication of code:

```jsx

//Higher Order Component
const withLoading = (Component) => ({url}) => {

	const useState{data,setData} = useState(null);
	const useState{loading,setLoading} = useState(true);

	//Fetching url
	useEffect = (() => {
			fetch(url)
			.then((json) => json.json())
			.then((repos) => {
				setData(repos)
				setLoading(false);
			)

	})
}

//Checking the required Component
	if(loading) return <div> Loading Data Please Wait </div>;
	if(!data) return <div> No data </div>;
	if(!data.length) return <div> Data is Empty </div>

	//displaying data
	return <Component {data}/>
}

const ListImages = ({data}) => {
	return(
		<ul>
			{
				data.map((url) => (
				<li>
					<img src={url} />
				</li>
				))
			}
		</ul>
	)
}

const ListData = ({data}) => {
	return(
		<ul>
			{
				data.map((item) => (
				<li>
					<h1> item </h1>
				</li>
				))
			}
		</ul>
	)
}

const DisplayData = withLoading(ListData);
const DisplayImages = withLoading(ListImages);

const App = () => {
	return (
	<div>
		<DisplayData url="https://examples.com/dummydata">
		<DisplayImages url="https://examples.com/dummyimages">
	</div>
	)
}



```

Now if you look at the code we have created a Higher Order Component `withLoading` which takes another component as an argument. The job of this component is to fetch the URL and check our validation condition. If all goes well it just displays the component which is passed to it as an argument. It does not care how the component is rendering the data which is exactly what we wanted.

Then we have created two-component `ListData` and `ListImages` which we display the data and images respectively. We then pass this component to `withLoading` component. Now if we call `DisplayData` or `DisplayImages` component both will first fetch the URL, then check our validation condition, and then it will render the component.

You can see how we as developers were able to adhere to the principles of functional programming here by employing the composition of functions as well as an additional wrapper function for the configuration.
This composition would still work if one of the higher-order components refused to accept a configuration (just by not calling it like the other ones that take a configuration).
