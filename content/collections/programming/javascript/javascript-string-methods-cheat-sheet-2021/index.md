---
title: Javascript String Methods Cheat Sheet 2021
Tags: ["programming","javascript"]
author: Hatim
date: 2021-06-28
published: true
image: /images/max-chen-lud4OaUCP4Q-unsplash.jpg
description: When programming in JavaScript, you often come across scenarios that require string manipulation. For example, when retrieving email , you may need to convert all characters to lowercase or use regular expressions to check if the entered password meets conditions.
keywords: javascript,methods,functions,string,cheatsheat, Cheat,Sheet,2021,methods
---

# Javascript String Methods Cheat Sheet 2021

Use these JavaScript string methods to easily perform character manipulation.

When programming in JavaScript, you often come across scenarios that require string manipulation. For example, when retrieving email , you may need to convert all characters to lowercase or use regular expressions to check if the entered password meets conditions.

JavaScript string methods will help you easily perform all these operations on the string according to your requirements. Here are some string methods and examples to help you understand them better.

## JavaScript String Methods

A string is a basic data structure consisting of characters. This data structure is part of all the major programming languages, including Python, JavaScript, Java, etc.

String methods are pre-built JavaScript methods that can help developers perform common operations on strings without having to write code manually. They are executed using dot notation attached to the string variable.

Because they are just JavaScript functions, they always end with square brackets and can contain optional parameters. Understanding is essential before proceeding. Let's get started and understand these methods in more detail.

First, let's declare a string with value "Hello, Welcome to Another Techs.":

```javascript
let str = "Hello, Welcome to Another Techs.";
```

## String.toUppercase() and String.ToLowerCase() methods

The string method ** toLowerCase () ** converts all characters in a given string to lowercase format. Similarly, the ** toUpperCase () ** method converts all characters to the uppercase format. These functions do not modify the original string.

Let's use a simple example to see these two methods:

```javascript
console.log(str);
console.log(str.toUpperCase());
console.log(str.toLowerCase());
```

When you run the above code in the console, you will receive the following output
:

```
Hello, Welcome to Another Techs.
HELLO, WELCOME TO ANOTHER TECHS.
hello, welcome to another techs.
```

## String.replace() method

As the name suggests, the **replace()** method can help you replace the part of the string with another part. This method has two parameters: The first is the substring to be replaced, and the second is the substring to be replaced. This method does not modify the original string in any way.

For example, if you want to replace **Another Techs** with string **javascript cheatsheat**, you can use the **replace()** method like this:

```javascript
let new_str = str.replace("Another Techs", "javascript cheatsheat");
console.log(new_str);
```

```
Hello, Welcome to javascript cheatsheat.
```

## String.trim() method

The method **trim()** removes all spaces in the string, spaces before the first character and after the last character. This method does not require you to pass any parameters, nor does modify the original string. It is very useful for validating user input on forms.

Let's explore this string method with a new example:

```javascript
let untrimmedString = "   Welcome to Another Techs      ";
let trimmedString = untrimmedString.trim();
console.log(untrimmedString);
console.log(trimmedString);
```

```
"   Welcome to Another Techs     "
"Welcome to Another Techs"
```

## String.concat() method

**concat()** method is used to concatenate two or more strings. You can add one or more parameters to this method to concatenate them into a single string. It will not make any modifications to the original string.
This is an example that shows concatenating two strings to form a new string:

```javascript
let s2 = " How are you?";
let new_str = str.concat(s2);
console.log(new_str);
```

```
Hello, Welcome to Another Techs. How are you?

```

## String.charAt() method

**charAt()** string method returns the character at index specified in the string. It only accepts one parameter, the index of the character to be retrieved. The index value ranges from 0 to and the length is -1.
This is an example of the **charAt()** method:

```javascript
console.log(str.charAt(11));
console.log(str.charAt(2));
```

```
o
l
```

## String.substring() method

**substring()** method is used to obtain a substring or part of the original string. This method takes two parameters: start index and end index. The output substring starts from the specified start index and is printed to the end index -1.

This is a quick example of the ** substring () ** method:

```javascript
console.log(str.substring(4, 8));
```

```
"o, W"
```

## String.search() method

The **search ()** method helps to find a specific substring or characters in the original string. This method accepts a set of characters or substrings as parameters and keeps track of the entire string. When a match is found, the starting index of the matching part is returned. Otherwise, this method returns 1.

You can use the **search()** method in the following ways:

```javascript
console.log(str.search("Techs"));
console.log(str.search("6"));
```

```
26

-1
```

## String.indexOf() and String.lastIndexOf() methods

The ** indexOf () ** method can help you find the first index where the specified character or substring appears in . It starts from the left of and traces the string to check if the given parameter matches.

Let's take as an example to find the index where **Another** appears in the string:

```javascript
console.log(str.indexOf("Another"));
```

```
18
```

If the given parameter does not exist in the string, the method returns with a value of 1.

Similarly, the **lastIndexOf()** method returns the index of the last occurrences of a given character or string. This is an example:

```javascript
console.log(str.lastIndexOf("l"));
```

```
9
```

## String.split() method

**split()** method is used to split all words or characters into a string according to the separator parameter passed to the method. The method's return type is an array. The array consists of characters or substrings, divided according to the given separator. The method does not modify the original string.

For example, if you pass a space ("") as the separator parameter to the divide method, the output will look like this:

```javascript
let splitString = str.split(" ");
console.log(splitString);
```

```
Array(5) [ "Hello,", "Welcome", "to", "Another", "Techs." ]
```

If you don't pass the parameter to the ** split() ** method, it will return a
array containing a single element composed of the value of a string variable.

## String.charCodeAt() method

Similar to the charAt method, the **charCodeAt()** method returns [ASCII value](https://en.wikipedia.org/wiki/ASCII)of the character at the specified index. This string method only takes as a parameter, which is the index from which characters will be retrieved.

```javascript
str.charCodeAt(9);
str.charCodeAt(str.length - 1);
```

```
108
46
```

Similarly, the index value ranges from 0 to length-1. If you try to pass an index
that exceeds the allowable limit, this method will return -1.
