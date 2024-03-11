---
title: React 18 is out !
date: 2021-06-15
image: /../images/images-react.jpg
published: true
Tags: ["programming","react"]
author: Hatim
description: react core team recently released an alpha version of react18. This version pays more attention to user experience and internal architecture changes, including adaptive concurrency functions. It gives you more control over dom rendering events.
keywords: react,react18,reactjs,new,feature,alpha,architecture,dom,document,API,root,suspense,transition,effects,strict,javascript,mode
---

# React 18 is Out!

react core team recently released an alpha version of react18. this version pays more attention to user experience and internal architecture changes, including adaptive concurrency functions,it gives you more control over dom rendering events.

## Installation

```bash
npm install react@alpha
npm install react-dom@alpha
```

## What's new in React 18

### 1. New Root API

You may be accustomed to seeing something like this at the top level of the application:

```javascript
import React from "react";
import ReactDOM from "react-dom";

const container = document.getElementById("root");

ReactDOM.render(<App />, container);
```

Isn't it normal? correct. This ReactDOM.render() is now called Legacy Root API. It works in exactly the same way as React 17. You can still keep it, but it will eventually be deprecated.

**The new root API looks a bit different:**

```javascript
import React from "react";
import ReactDOM from "react-dom";
import App from "App";

const somecontainer = document.getEleementById("root");

const root = ReactDOM.createRoot(somecontainer);

root.render(<App />);
```

It is very similar! Use `ReactDOM.createRoot` instead of the **legacy** method.

**With this change, a few things happened:-**

The hydrate method is gone, now it is an option in `createRoot`-The render callback is gone (now anything can be passed to `<App/>`)

If you don't use these two functions, you don't have to worry about their changes. If you'd like to learn more about them, here are some sample code changes from the React core team.

By switching to the new root API, you will automatically get the new out-of-the-box enhancements that React 18 offers.

### Suspense

Suspense updates are all to improve server-side rendering. One of the main problems we face in the server-side rendering process is that not all data is sent to the user at once. Send HTML first, then CSS, while JS is still rendered on the server. This is also called hydration time. Buttons are great, but until event handlers are attached to them, they are just visual effects.

**React 18 solves this problem!**

For those elements that rely heavily on JS, we can send alternative components for a period of time instead of sending HTML and CSS. Once the component is ready for shipment, the main component will automatically change it.

For using `Suspense` all you have to do is warp your components in an `<Suspense>` component:

```javascript
<Suspense fallback={<Loading />}>
  <Component />
</Suspense>
```

In the above snippet, React will show `<Loading/>` component at first and then replace it with `<Component>` when the data gets resolved.

### Transition API

This is a new API introduced in this version, which helps to keep the current web page responsive and allows a large number of non-blocking UI updates at the same time.

An important use case for `startTransition` can be when the user starts typing in the search box. The input value should be updated immediately and the search results can wait a few milliseconds (as expected by the user).

This API provides a way to distinguish between fast updates and delayed updates.
Delayed update (that is, transition from one user interface view to another user interface view) is called transition update.

For urgent updates such as typing, hovering, clicking, etc., we usually call props/functions like this:

```javascript
setText(input);
```

For non-urgent or heavy UI updates, we can wrap it in a startTransition API as :

```javascript
startTransition(() => {
  setText(input);
});
```

### Server Side Rendering Imporvements

The server-side rendering has undergone an architectural overhaul in this release, including improvements to the first loading screen time.
In the normal version (up to React 17), SSR must load the entire page to start reloading the page.

**This has changed !**

This is now called selective hydration. Assuming we have 5-8 different components on the screen, once the code loads and does not block the rest of the page, packaging a component will now start to hydrate a very specific component. By adopting this strategy, the most important part/component of the page can first become interactive (under extremely slow connections), while other components continue to remain hydrated to provide a good user experience.

### Strict Effects coming to Strict Mode

React 18 will now be released with strict effects mode. Like strict mode, it will be used for developing builds and improving DX.

When components are included in Strict Effects, React will make sure the side effects are run twice "on purpose" to detect abnormal behaviors / patterns, which is often a problem when using the useEffect mount and cleanup feature.

To know more about feature and improvement in React 18 [here](https://reactjs.org/blog/20/the-plan-for-react-18.html)
