---
title: A Beginner's Guide to React API Calls- Learn How to Make GET Requests with React
date: 2022-07-23
Tags: ["programming","react"]
author: Hatim
published: true
keyword: React,HTTP,Fetch,Axios,REST APIs,API calls,HTTP method,HTTP request,API,Asynchronous,Rendering,RESTful
description: Learn how to make API calls in React using fetch, axios and other HTTP request methods. Our comprehensive guide will help you master the art of making API calls in React, from basic to advanced techniques.
image: /images/daduk_visa.jpg
---

# A Beginner's Guide to React API Calls: Learn How to Make GET Requests with React

If you're a developer working with React, you know how challenging it can be to keep up with all the APIs available. React APIs provide developers with all the tools they need to create user interfaces, and there are countless options to choose from.

To help you get started, we've put together this comprehensive React API cheat sheet. In this article, we'll cover the most important APIs in React.We'll also explain how to use them and provide some examples.

## React APIs

**API** or **Application Programming Interface** is a way a programmer talk between two piece software. An API is used by the programmer to make the software simpler and easy. It also facilitates the programmer with an efficient and organise way to build their software.

In React API, are mostly used in getting data from the server. Here the data can be of any type text,image,video or xml or json file which a programmer uses in different way to build a web app.

The most frequent action in any modern online application is calling APIs. The majority of the time, collecting data from an API call, managing success or error cases, and other repeated tasks are required while communicating with an API.

We constantly have to perform those time-consuming processes when making tens of hundreds of API calls. In contrast to certain small apps, where we occasionally don't even care, we can handle those situations effectively by adding a higher degree of abstraction over those basic API calls.

_The issue arises when we start layering additional features on top of the already-existing ones without properly and repeatedly managing API calls. In that instance, we end up having a lot of repeating code throughout the entire application for all of those API call-related repetitions._

Consuming [REST APIs](https://www.ibm.com/topics/rest-apis) in a React Application can be done in various ways.The most prefered ways now a days is using **[React Hooks](https://www.w3schools.com/react/react_hooks.asp)**. In this tutorial we will discuss various ways to call an API using react.

### 1. React API call using Fetch API

This is the most common way to call an API. **Fetch API** is built into most the browser and it enable use to make HTTP GET request easily.

```jsx

import { useEffect } from "react";

function App() {
  useEffect(() => {
	//Calling API
    fetch("https://jsonplaceholder.typicode.com/posts")
		//Getting API response and converting it into json format
      .then((data) => data.json())
      .then((data) =>  console.log(data) )
      .catch((errro) => console.log("Error"));
  }, []);

	return (
	....
	)
}

```

In the above code the **fetch** return a promise. We are making asynchronous request to the particular url. When the server reponse this response is passed to callback function using **then(callback)**. By chaining this **then** method we can transform the data as per we need. The return data of the **then(callback)** is passed as an argument to next **then** method. If anything goes wrong in the chainning process we catch that error using **catch(callback)**

### 2. React API call using Async/Await

Another way of working with promise is to use **async/await**

Before a function, the **async** keyword has two effects:

- Make a promise that is always kept.
- permits the usage of await in it.

JavaScript waits until a promise settles when the **await** keyword is used before:

- If there is a problem, an exception is raised.
- If not, it returns the outcome.

```jsx

import { useEffect } from "react";

function App() {
  async function fetchData(url) {
    try {
      const response = await fetch(url);
      const response_json = await response.json();
      console.log(response_json);
    } catch (error) {
      console.error(error);
    }
  }

  useEffect(() => {
    fetchData("https://jsonplaceholder.typicode.com/posts");
  }, []);


	return (
	....
	)
}
```

### 3. React API call using Axios

Your front-end application and Node.js backend can both use [Axios](https://axios-http.com/), a Promise-based HTTP client for JavaScript.
Sending asynchronous HTTP queries to REST endpoints and carrying out CRUD processes are simple when using Axios.

In this case, you must first use npm or yarn to install Axios before adding it as an import to your parent component.

```bash

npm install axios

```

An example of utilising Axios is shown in the code snippets below:

```jsx

import { useEffect } from "react";

function App() {

	useEffect(() => {
		axios
			.get("https://jsonplaceholder.typicode.com/posts")
			.then((res) => res.data)
			.then((res) => {
				console.log(res);
				setData(res);
				setLoading(false);
			})
			.catch((error) => console.log(error));
	}, []);



	return (
	....
	)
}

```

### 4. Waterfall Requests

Once you start writting react app there will be time were you will need to call different api request one after other That is if one api request is successful call next api and then next. This request which happen one at a time and one after another is called **Waterfall Requests**.

#### Using fetch()

```jsx

function App() {

  useEffect(() => {
//	Fetch Here Multiple Requests
    Promise.all([
      fetch("https://jsonplaceholder.typicode.com/posts").then((res) =>
        res.json()
      ),
      fetch("https://jsonplaceholder.typicode.com/users").then((res) =>
        res.json()
      ),
    ])
      .then(([res1, res2]) => {
			//response of each request in an array
        console.log(res1);
        console.log(res2);
      })
      .catch((error) => console.log(error));
  }, []);



	return (
	....
	)
}

```

#### Using Await/Async

```jsx

function App() {

  async function fetchData() {
    try {
      const [res1, res2] = await Promise.all([
        fetch("https://jsonplaceholder.typicode.com/posts").then((res) =>
          res.json()
        ),
        fetch("https://jsonplaceholder.typicode.com/users").then((res) =>
          res.json()
        ),
      ]);
      console.log(res1);
      console.log(res2);
    } catch (error) {
      console.error(error);
    }
  }

  useEffect(() => {
    fetchData();
  }, []);

	return (
	....
	)
}
```

### 5. Creating Custom Hook for fetching API call in React

We have seen that API call are either successful,pending or failed. We can use this logic to create a our own custom hook for fetching api call or request in our react application. We will call this hook `useFetch` and use this hook to in different component in our react application.

```jsx
// fetch.js
import React, { useState, useEffect } from "react";

export const useFetch = (url) => {
  const [data, setData] = useState();
  const [error, setError] = useState();
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    if (!url) return;
    fetch(url)
      .then((data) => data.json())
      .then((data) => {
        setData(data);
        console.log(data);
      })
      .then(() => setLoading(false))
      .catch(setError);
  }, [url]);

  return {
    loading,
    data,
    error,
  };
};
```

As you can see we have created custom hook which will fetch our data based on the `url` passed to it. Based on this it will return three things:

1. `loading`: if the request its getting fetched this will be true or false.
2. `data`: if the request is successful this variable will hold our data.
3. `error`: if any error occured during api call this vairbale will hold error.

```jsx
// App.js

import React from "react";
import { useFetch } from "./fetchHook";
function App() {
  const { loading, data, error } = useFetch(
    "https://jsonplaceholder.typicode.com/posts"
  );

  if (loading) {
    return <h1>Loading</h1>;
  }
  if (error) {
    return <pre>{JSON.stringify(error, null, 2)}</pre>;
  }

  return <div>{data}</div>;
}

export default App;
```

## Conclusion

In this article, we provided a beginner's guide to React API calls, specifically focusing on how to make GET requests with React. We explained what API calls are, why they are important, and how to make a GET request using the fetch() function. We also discussed best practices for making API calls with React and how to handle errors that may occur during the request. By following these guidelines, you can build dynamic and responsive applications that retrieve and display data in real-time.

## FAQs
1. What is the difference between GET and POST requests?
GET requests are used to retrieve data from a server, while POST requests are used to send data to a server.
2. Can I use other HTTP methods with React, such as PUT or DELETE?
Yes, React supports a variety of HTTP methods, including PUT, POST, DELETE, and more.
3. Do I need to use a third-party library to make API calls with React?
No, React has a built-in fetch() function that can be used to make API calls. However, there are third-party libraries available, such as Axios or jQuery, that can provide additional functionality.
4. What is an API endpoint?
An API endpoint is a URL that is used to access a specific resource or data from an API.
5. How can I test my API calls in React?
There are a variety of tools available for testing API calls in React, such as Postman or the Chrome DevTools network tab.