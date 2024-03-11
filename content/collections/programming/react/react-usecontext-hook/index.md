---
title: React useContext Hook- Simplifying State Management in React
published: true
author: Hatim
Tags: ["programming","react"]
image: /images/emre-turkan-KULAXcZZ22U-unsplash.jpg
description: Learn how to use the React useContext hook for simplified state management in your React applications. Our tutorial covers everything you need to know to get started.
date: 2022-06-30
keywords: React useContext Hook,React Hooks,React Context API,React State Management,React Tutorial
---

# React useContext Hook: Simplifying State Management in React

In a typical React application, data is passed top-down (from parent to child) by props, however this can be challenging for some prop types (such locale preference and UI theme), which are needed by numerous components that are nested at different levels within an application.

**Without having to manually provide props down via each nested component, context offers a means to pass data or state through the component tree.** For a tree of React components, it is intended to share information that can be regarded as global information, such as the currently authenticated user or theme (e.g. color, paddings, margins, font-sizes).

Context is used by Context API. **Context and Provider Consumer Components** transmit the data, however writing the lengthy functional code to leverage this Context API is quite time-consuming. Therefore, using the useContext hook eliminates the requirement to use the Consumer Component and makes the code easier to read and less verbose. React 16.8 has a new hook called useContext.

## Problem with useState hook in ReactJS

The topmost parent component in the stack that needs access to the state should hold it.

We have numerous nested components as an example.
The stack's top and bottom components both require access to the state.

Without Context, we must transmit the state as "props" via each nested component in order to accomplish this. **Prop drilling** is the term for this.

**Example:**

```jsx
import { useState } from "react";


const ParentComponent = () => {
  const [data, setData] = useState("Another Techs");
  const [user, setUser] = useState("Alex");
  return (
    <div>
      <h1> Hello, {user} </h1>
      <ChildComponent1 data={data} />
    </div>
  );
};


const ChildComponent2 = ({data}) => {
	return (
	<div>
	   <ChildComponent3 data={data}>
	</div>
	)
}

const ChildComponent3 = ({data}) => {
	return (
	<div>
	   <ChildComponent4 data={data}>
	</div>
	)
}

const ChildComponent4 = ({data}) => {
	return (
	<div>
	   <ChildComponent5 data={data}>
	</div>
	)
}

const ChildComponent5 = ({data}) => {
	return (
	<div>
	   <h2> Welcome to {data} !! </h2>
	</div>
	)
}

```

Despite the fact that components 2-4 did not require the state, they had to send it on so that component 5 could receive it.

## React useContext to the rescue

The context, the provider extrapolated from the context, and the consumer are the three players required to apply the React context.

**Syntax:**

```jsx
const contextName = useContext(initialValue);
```

The value that React provides is accepted by useContext. When its value changes, you must first createContext and then re-render the component, although memorising can still improve performance.

The example application would seem as follows when the context is applied to it:

```jsx

import { useState,createContext,useContext } from "react";

const DataContext = createContext();


const ParentComponent = () => {
  const [data, setData] = useState("Another Techs");
  const [user, setUser] = useState("Alex");
  return (
    <div>
	<UserContext.Provider value={data}>
	   <h1> Hello, {user} </h1>
	   <ChildComponent1 />
	</UserContext.Provider>
    </div>
  );
};


const ChildComponent2 = () => {
	return (
	<div>
	   <ChildComponent3 >
	</div>
	)
}

const ChildComponent3 = () => {
	return (
	<div>
	   <ChildComponent4 >
	</div>
	)
}

const ChildComponent4 = () => {
	return (
	<div>
	   <ChildComponent5 >
	</div>
	)
}

const ChildComponent5 = () => {
	const data = useContext(DataContext);
	return (
	<div>
	   <h2> Welcome to {data} !! </h2>
	</div>
	)
}

```

Let's look into more detail what has been done.

- First, const DataContext = createContext() creates the context that's going to hold the data.

- Second, inside the `<ParentComponent />` component, the application's child components are wrapped inside the user context provider: `<UserContext.Provider value={data}>`.

**Note that the value prop of the provider component is important: this is how you set the value of the context.**

- Finally, `<ChildComponent5 />` becomes the consumer of the context by using the built-in useContext(DataContext) hook. The hook is called with the context as an argument and returns the user name value.

- `<ChildComponent2/>` to `<ChildComponent4/>` components don't have to pass down the `data` prop. That is the great benefit of the context: it removes the burden of passing down data through the intermediate components.

## What happens if context value is changed ?

All of the context provider's consumers are alerted and re-rendered when the context value is updated by changing the context provider's value prop `(<Context.Provider value=value />)`.

For example, if I change the user data from 'Another Techs' to 'ReactJS Context Hook', then <ChildComponent5 /> consumer immediately re-renders to display the latest context value:

```jsx

import { useState,useEffect,createContext,useContext } from "react";

const DataContext = createContext();


const ParentComponent = () => {
  const [data, setData] = useState("Another Techs");
  const [user, setUser] = useState("Alex");
	useEffect(()=>{
	   setTimeout(()=>{
		    setData("ReactJS Context Hook");
		 },2000);
	},[]);

  return (
    <div>
	<UserContext.Provider value={data}>
	   <h1> Hello, {user} </h1>
	   <ChildComponent1 />
	</UserContext.Provider>
    </div>
  );
};


const ChildComponent2 = () => {
	return (
	<div>
	   <ChildComponent3 >
	</div>
	)
}

const ChildComponent3 = () => {
	return (
	<div>
	   <ChildComponent4 >
	</div>
	)
}

const ChildComponent4 = () => {
	return (
	<div>
	   <ChildComponent5 >
	</div>
	)
}

const ChildComponent5 = () => {
	const data = useContext(DataContext);
	return (
	<div>
	   <h2> Welcome to {data} !! </h2>
	</div>
	)
}

```

On the screen, "Another Techs" (context value) would be visible. The context value switches to "ReactJS Context Hook" after two seconds, and the screen updates to reflect the new value.

### Real world example where useContext Hook might come handy
Suppose you have a React app that displays a list of products. You want to be able to add and remove products from the list, and you also want to be able to display the total number of products in the list. One way to do this is to use the useContext hook to manage the state of the products list and the total number of products.

First, you need to create a context object that will hold the state of the products list and the total number of products. Here's how you can do it:

```jsx
import React, { createContext, useContext, useState } from 'react';

const ProductContext = createContext();

export const useProduct = () => useContext(ProductContext);

export const ProductProvider = ({ children }) => {
  const [products, setProducts] = useState([]);
  const [totalProducts, setTotalProducts] = useState(0);

  const addProduct = (product) => {
    setProducts([...products, product]);
    setTotalProducts(totalProducts + 1);
  };

  const removeProduct = (product) => {
    const newProducts = products.filter((p) => p.id !== product.id);
    setProducts(newProducts);
    setTotalProducts(totalProducts - 1);
  };

  return (
    <ProductContext.Provider value={{ products, totalProducts, addProduct, removeProduct }}>
      {children}
    </ProductContext.Provider>
  );
};


```
In the above code, we create a ProductContext object using the createContext method. We also define a custom hook called useProduct that will be used to retrieve the state values from the context. Inside the ProductProvider component, we define the state values using the useState hook, and we define two functions called addProduct and removeProduct to add and remove products from the list. Finally, we pass the state values and functions to the context using the Provider component.

Now, in any component that needs to access the products list or the total number of products, you can use the useProduct hook to retrieve the values from the context. Here's an example:

```jsx
import React from 'react';
import { useProduct } from './ProductContext';

const ProductList = () => {
  const { products, totalProducts, removeProduct } = useProduct();

  return (
    <>
      <h2>Products ({totalProducts})</h2>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            {product.name} - {product.price}
            <button onClick={() => removeProduct(product)}>Remove</button>
          </li>
        ))}
      </ul>
    </>
  );
};

export default ProductList;


```
In the above code, we import the useProduct hook from the ProductContext file. We then use the useProduct hook to retrieve the products list, total number of products, and the removeProduct function from the context. We render the products list as a list of items, and we use the removeProduct function to remove a product from the list when the user clicks the "Remove" button.

Using the useContext hook in this way can make your code cleaner and easier to maintain. By centralizing the state management in the context, you can avoid having to pass props down the component tree, which can make your code more efficient as well.

## When to use useContext hook ?

Utilizing the context is primarily intended to give your components access to certain global data and to re-render when that global data is modified.
When you have to pass down props from parents to kids, context solves the props drilling problem.

Holding within the context:

- global state
- a theme
- an application's settings
- an authenticated user name
- a user's settings
- their preferred language
- a group of services.

On the other hand, you ought to give the decision to use context in your application significant thought.

Integrating the context hook firstly increases complexity. Complexity is increased by creating the context, encapsulating everything in the provider, and using `useContext()` in each consumer.

Second, introducing context hook makes unit testing the components more challenging. You would need to encase the consumer components in a context provider for unit testing. Including the elements that the context indirectly influences — the forerunners of context consumers!

## Conclusion

No matter where in the components tree a child component is located, React's concept of useContext hook enables you to supply it with global data. The context must be created, provided, and consumed before it can be used.

Remember that the useContext hook adds a significant degree of complexity when incorporating it into your application. It's not always a big deal to drill the props through two or three layers of the hierarchy.


## References

- [Context](https://en.wikipedia.org/wiki/Context_(computing))
- [useContext Hooks React Docs](https://reactjs.org/docs/hooks-reference.html#usecontext)
- [Medium](https://medium.com/technofunnel/usecontext-in-react-hooks-aa9a60b8a461)
- [React Hooks](https://amzn.to/3TM9f76)
