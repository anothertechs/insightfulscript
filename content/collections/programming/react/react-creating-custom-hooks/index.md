---
title: React JS - Creating custom hooks in React
date: 2022-07-11
author: Hatim
published: True
Tags: ["programming","react"]
description: We provide you with simple-to-understand React custom hook code recipes so you can understand how they function and get more at ease creating your own.
keywords: react,create,custom,hook,hooks,reactjs,use,hooks
image: /images/christopher-gower-m_HRfLhgABo-unsplash.jpg
---

# ReactJS - Creating Custom hooks in React

**With the help of custom React hooks, you may provide your React applications additional, distinctive functionality.**

Installing a third-party library designed to address your issue is frequently the simplest way to add a certain functionality to your application. What do you do, though, if such a library or hook doesn't exist?

Learning how to create custom hooks is crucial if you want to fix issues or add features that are lacking in your own React projects.

In this step-by-step tutorial, I'll walk you through the process of making your own custom React hooks and explaining the issues they were designed to address.

## What is react hooks?

To the delight of the developer community, the React team just unveiled hooks. What is the big deal? By enabling us to incorporate elements that are only available to class components, such stateful logic, hooks actually opens up a completely new method to design functional components.

You can basically accomplish this using State and Effect hooks in React. You can define a state object and a function that updates it using the State(useState) hook. You can execute side effects in a functional component using the Effect(useEffect) hook. Consider it to be similar to class component lifecycle events.

A function that begins with the word "use" and may invoke other hooks is referred to as a custom hook. The "useWhatever" naming style is primarily used to enable the linter to detect errors in the usage of certain hooks, such as instances when usage violates the hooks requirements.

## Need of react custom hooks

In order to keep the DRY (Don't Repeat Yourself) principle in your React projects, you should use custom hooks. Consider the situation when you need to employ some logic that uses some built-in hooks in various functional components. You may either write the same logic in each component individually (which goes against the DRY principle), or you can construct a new function, encapsulate the logic inside of it, and call it from the other components. Since you only need to write the reasoning once, the second alternative is unquestionably the preferable option. The unique hook in this case is the independent function you defined.

In order to apply your logic in different functional components (hooks are ineffective in class components), simply construct a separate custom hook and use it.

## Rules for creating react custom hooks

- Only use hooks at the highest level. Never call hooks while inside of a loop, a condition, or nested procedures.
- hook calls must only come from React function components.
- Regular JavaScript functions shouldn't call hooks. (Your own custom hooks are the only other location where calling hooks is appropriate. They'll be revealed to us shortly.)

If you're wondering why these rules exist, it's because React uses the order that hooks are invoked to associate each hook with a certain local state. Placing a hook inside of a condition can alter this order, preventing the subsequent hooks from being called and, most likely, leading to bugs.

## Example on creating react custom hooks

Now let us see how we can create and use custom hooks in our react application. For our example we are going to create custom hooks name `useCopytoClipboard()`.

Since the hooks return two thing our custom hook will also give us two values :

1. `isCopied`: this state will tell us weather the content is copied or not.
2. `handleCopy`: this function will be use to set text to our system clipboard.

Also to make `useCopytoClipboard` hook little bit real. I have used `useEffect` hook which will clear our system clipboard after some amount of time which we decide

```jsx
//useCopytoClipboard.js

import { useEffect, useState } from "react";
import copy from "copy-to-clipboard";

export default function useCopyToClipboard(resetInterval = null) {
  const [isCopied, setCopied] = useState(false);

  const handleCopy = (text) => {
    if (typeof text == "string" || typeof text == "number") {
      copy(text.toString());
      setCopied(true);
    } else {
      console.error("Error\n Cannot Copy");
    }
  };

  useEffect(() => {
    let timeout;
    if (isCopied && resetInterval) {
      timeout = setTimeout(() => {
        copy(" ");
        setCopied(false);
      }, resetInterval);
    }
    return () => {
      clearTimeout(timeout);
    };
  }, [isCopied, resetInterval]);

  return [isCopied, handleCopy];
}
```

We must first check that the function only accepts data of the types string or numeric. To ensure that the type is either a string or an integer, we will create an if-else statement. If not, we will record a console error informing the user that they are unable to copy any further types.

Next, we turn the text into a string so that it can be passed to the `copy` method. The `handleCopy `method from the hook is then returned for use wherever in the application we see fit.

The `handleCopy` function will typically be attached to a button's onClick event.

We also need a state that indicates whether or not the text was copied. `useState` will be called at the beginning of our hook to construct that, and we'll make a new state variable called `isCopied` with the setter setCopy.

This value will initially be false. If the copying of the text is successful, copy will be set to true. Otherwise, we'll make it false.

Finally, we will return `handleCopy` and `isCopied` from the hook in an array.

Now, we can use `useCopyToClipboard` inside of any component.

In my situation, I'll utilise it in conjunction with a copy button that already has the code for our code sample.

All we have to do to make this work is to give the button a on click. Additionally, a function called `handlecopy` returns the text form of the code that was sent to it.

```jsx
// App.js

import { useState } from "react";
import useCopyToClipboard from "./utils/copyToClipboard";

function App() {
  const [isCopied, handleCopy] = useCopyToClipboard(3000);
  const [value, setValue] = useState("Type Anything...");
  return (
    <div>
      <input
        value={value}
        onChange={(e) => {
          setValue(e.target.value);
        }}
      />
      <button onClick={() => handleCopy(value)}>Copy to ClipBoard</button>
      {isCopied ? <div> Text Copied </div> : <div> Nothing to Clipboard </div>}
    </div>
  );
}

export default App;
```

## Why should you use react custom hooks ?

Consider a scenario where you have to use useEffect and useState during development.

After some time, you become aware that another component also requires the useEffect and useState logic. You can copy code, but you probably think there must be a better approach. What will you do then? Personalized hooks to the rescue.

- Reusability: We don't have to write the same hook twice because we can use it repeatedly.

- Clean Code: A cleaner codebase can be achieved by isolating all component logic into a hook.

- Easy maintenance — maintainability. The logic of the hook only needs to be altered once, if at all.
- Great Community – there is a significant probability that the hook you had in mind has already been developed. There are a tonne of Custom hooks on the web! You can locate a hook that fits your needs, utilise it as is, or even better, use it as a springboard to create something great!

## Conclusion

We discussed custom hooks, clarified the advantages of utilising custom hooks, and provided examples from actual applications along with an explanation of when we utilised particular hooks.

We've shown how easy it is to create custom hooks and how many (open) resources are available for finding inspiration and using custom hooks that already exist (I attached more sources below).
I sincerely hope you enjoyed and gained knowledge from the post. Regards from the reader.

It's now your turn to design a unique hook of your own!
