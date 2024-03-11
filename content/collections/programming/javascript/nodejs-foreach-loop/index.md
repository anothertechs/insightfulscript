---
title: Nodejs- forEach loop cheatsheet
date: 2021-09-26
published: true
author: Hatim
Tags: ["programming","javascript"]
keywords: nodejs,forEach,javascript,loop,cheatsheet,examples,array
description: Node.js forEach executes the supplied function for each element using Node.js forEach.  With the help of examples, we will learn how to use the forEach statement in this article.
image: /images/nodejs-forEach.jpg
---

# Nodejs- forEach loop cheatsheet

You can use looping to run through each item in an array and customise and output each one as you see fit.
Loops are a crucial tool for rendering arrays in JavaScript, just as they are in any other programming language.

Let's dive deeper into the many ways you can use foreach loops in JavaScript/Nodejs with the help of some practical examples.

## forEach Loops in Nodejs/Javascript

- It's a sophisticated looping structure for traversing elements in a collection. It runs till the collection set is finished.

- The difference between a for loop and a foreach loop is that a for loop works with variables, whereas a foreach loop works with an object.

- In most cases, foreach loops do not have an explicit counter.

Although forEach in Nodejs/JavaScript cannot decrement, it is typically less verbose than the raw for loop.
It operates by selecting items one by one without remembering the previous one.

The general syntax of JavaScript forEach is as follows:

```javascript
...

array.forEach((element) => {
  action;
});

...
```

For Example:

```javascript
...

let array = [1, 3, 5, 6];
array.forEach(elem => {
    console.log(elem)
});

...
Output:
1
3
5
6

```

## Applying External function supplied as parameter to forEach on an array of items

In this example, we'll use forEach to apply to each element of the array.
We also define the function separately and pass it as an input to forEach.

```javascript
...

let elements = [1,2,3,4,5];

let myFunc = function (elem) {
  console.log(elem * 2);
};

elements.forEach(myFunc);

...

Output:
1
4
6
8
10
```

## Using Lambda fucntion in forEach loop

In the below example we will show how to use Nodejs/Javascript Lambda function in forEach loop.

```javascript
...
let elements = [1,2,3,4,5,6]

elements.forEach(elem => (console.log(elem*2)))

...

Output:
1
4
6
8
10

```

## Using forEach on Array with access to Element, Index and Array

In each iteration of this example, we will access index, array, and element.

```javascript
...

let elements = ["dog","cat","fish","horse"]


let myFunc = function(elem, index, array) {
  console.log(index + ' : ' + elem + ' - ' + array[index])
}

elements.forEach(myFunc)
...

Output:
0 : dog - dog
1 : cat - cat
2 : fish - fish
3 : horse - horse

```

Although we've covered the JavaScript/Nodejs forEach looping methods here, understanding the fundamentals of iteration in programming allows you to employ them in your applications with confidence and flexibility.
However, the majority of these JavaScript/Nodejs loops operate in the same way, with just minor changes in their overall structure and syntax.

Most client-side array rendering, on the other hand, is based on loops.
So feel free to experiment with various looping strategies.
Using them with more complex arrays, for example, will help you comprehend JavaScript/Nodejs loops better.
