---
title: Python Class Method Decorator- A Comprehensive Guide
date: 2021-11-12
published: true
Tags: ["programming","python"]
keywords: python class method decorators,python class method decorator,python class decorator,python classmethod decorator,python class method decorator args
description: Learn how to use decorators to modify and enhance the functionality of your Python class methods. This guide covers everything from the basics to advanced techniques, with practical examples and code snippets to help you get started.
image: /images/Python-@classmethod-decorator.jpg
---

# Python Class Method Decorator: A Comprehensive Guide

Python is a powerful programming language that supports many features that make programming easier and more efficient. One of these features is the class method decorator. In this article, we will explore what class method decorators are, how to use them, and some practical examples.

## Table of Contents
* Introduction
* What is a Class Method?
* What is a Decorator?
* What is a Class Method Decorator?
* When should you use Python Decorators?
    * Characteristics of Decorators
    * classmethods() Syntax
    * classmethod() Parameters
    * classmethod() Return Value
* Practical Examples of Class Method Decorators
* Conclusion
* FAQs

## Introduction

In Python, decorators are a simple and elegant way to add functionality to functions and methods. The use of decorators can be done in a variety of ways. Decorators can be used with methods declared in a class, which is a handy use-case. The functionality of the defined method can be extended by decorating methods in the classes we design. We could, for example, do a data integrity check or save the method call's result to a file. What we choose to do is entirely up to us. Method decorators merely give us the ability to enhance functionality in a stylish manner.

## What is Class Method ?

A class method is one that is attached to a class rather than its object. It, like staticmethod, does not necessitate the construction of a class instance.

The following is the distinction between a static method and a class method:

1. The static method has no knowledge of the class and only deals with the parameters.

2. Because the class method's parameter is always the class itself, it works with it.

## What is a Decorator?

In Python, a decorator is a function that takes another function as input and returns a modified version of the input function. A decorator is denoted by the @decorator_name syntax, where decorator_name is the name of the decorator function.

Decorators can be used to modify the behavior of functions or classes without changing their code directly. This is a powerful feature of Python that allows for code reuse and simplification.

## What is a Class Method Decorator?
A class method decorator is a decorator that is used to modify the behavior of a class method. Class method decorators are defined using the @classmethod and @decorator_name syntax.

A class method decorator can be used to modify the behavior of a class method by adding functionality before or after the method is called, or by modifying the arguments passed to the method. Class method decorators can also be used to create alternative constructors, which allow creating instances of the class using different parameters or inputs.

## When Should You Use a Python Decorator?

When you need to change the behaviour of a function without changing the function itself, you'll use a decorator.
When you want to add logging, test performance, do caching, validate rights, and so on, here are some nice examples.

When you need to run the same code on many functions, you can utilise one. This prevents you from creating redundant code.

### Characteristics of Decorators

- Declares a method for a class.

- The first parameter must be `cls`, which is a class attribute accessor.

- Only the class attributes, not the instance attributes, are accessible via the class method.

- ClassName can be used to invoke the class method.

- It has the ability to return a class object.

The `@classmethod` decorator is used to declare a class method that may be called using `ClassName.MethodName()`.
A class object can also be used to call the class method.

The `classmethod()` function can be replaced with the `@classmethod()` function. Because the `@classmethod` decorator is only a syntactic sugar, it is advised to use it instead of the function.

### classmethods() Syntax

Syntax of `classmethod` methods is:

```python

classmethod(func) ## un-Pythonic way

#or

@classmethod
def func(cls,args...)

```

### classmethod() Parameters

`classmethod()` method takes one argument:

- **function** - Function that need to be converted into class method.

### classmethod() Return Value

It returns a class method for a giver function.

### Example

Let's have a look at an example of a class that deals with dates (this will be our boilerplate):

```python
class Date(object):

    def __init__(self, day=0, month=0, year=0):
        self.day = day
        self.month = month
        self.year = year
```

This class might certainly be used to hold information about specific dates.

Here we have `__init__`, a typical initializer of Python class instances, which receives arguments as a typical `instancemethod`, having the first non-optional argument (`self`) that holds a reference to a newly created instance.

Let's say we want to construct a lot of Date class instances with date information encoded as a string with the format 'dd-mm-yyyy' from an external source.
Assume we need to perform this in several locations across our project's source code.

So here's what we need to do:

1. Parse a string to get the day, month, and year as three integer variables or a three-item tuple that includes those variables.

2. Pass those variables to the initialization method to create Date.

which look's something like this:

```python
day, month, year = map(int, string_date.split('-'))
date1 = Date(day, month, year)
```

C++ can implement such a functionality with overloading for this reason, but Python lacks this overloading. We can instead use classmethod. Let's create another "constructor".

```python
    @classmethod
    def from_string(cls, date_as_string):
        day, month, year = map(int, date_as_string.split('-'))
        date1 = cls(day, month, year)
        return date1

date_obj = Date.from_str("2021-11-12")
```

Let's take a closer look at the above implementation and see what benefits we have:

- We've made date string parsing reusable by putting it all in one place.

- Encapsulation works well in this case (if you think that you could implement string parsing as a single function elsewhere, this solution fits the OOP paradigm far better).

**`cls` is not a class instance, but rather an object that holds the class itself. It's cool because if we inherit our Date class, all of our children will inherit `from_string() method.**

## Practical Examples of Class Method Decorators

### Example 1: Alternative Constructor

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_birth_year(cls, name, birth_year):
        age = datetime.date.today().year - birth_year

```
In this example, we define a class `Person` with an `__init__` method that initializes the `name` and `age` attributes of the class. We also define an alternative constructor `from_birth_year`, which takes the `name` and `birth_year` as arguments and calculates the age of the person based on the current year.

### Example 2: Logging Decorator

```python
import logging

def log_class_method(func):
    def wrapper(*args, **kwargs):
        logging.info(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

class MyClass:
    @classmethod
    @log_class_method
    def my_class_method(cls, arg1, arg2):
        # method code here

```
In this example, we define a decorator function `log_class_method` that logs the name of the decorated method before it is called. We then decorate the `my_class_method` with this decorator, which adds logging functionality to the method.

### Example 3: Caching Decorator

```python
def memoize_class_method(func):
    cache = {}
    def wrapper(cls, arg):
        if arg not in cache:
            cache[arg] = func(cls, arg)
        return cache[arg]
    return wrapper

class MyClass:
    @classmethod
    @memoize_class_method
    def my_class_method(cls, arg):
        # method code here


```
In this example, we define a decorator function `memoize_class_method` that caches the results of the decorated method for future use. We then decorate the my_class_method with this decorator, which adds caching functionality to the method.

## Conclusion

In this article, we explored what class method decorators are, how to use them, and some practical examples. Class method decorators are a powerful tool in Python programming that allows modifying the behavior of a class method without changing its code directly. They can be used to add functionality before or after the method is called, or to modify the arguments passed to the method. Class method decorators can also be used to create alternative constructors or to add caching or logging functionality to a method.

## FAQs
1. What is a decorator in Python?
A decorator is a function that takes another function as input and returns a modified version of the input function. It is a powerful tool for modifying or enhancing the behavior of functions and classes without explicitly modifying their code.

2. What is a class method in Python?
A class method is a method that is bound to the class and not the instance of the class. It can be called on the class itself, not just on an instance of the class. Class methods are defined using the `@classmethod` decorator.

3. What is a class method decorator in Python?
A class method decorator is a decorator that is used to modify the behavior of a class method. Class method decorators are defined using the `@classmethod` and `@decorator_name` syntax.

4. How to use a class method decorator in Python?
To use a class method decorator, you need to define the decorator function and use it with the `@classmethod` syntax. The decorator function modifies the behavior of the class method by adding functionality before or after the method is called, or by modifying the arguments passed to the method.

5. What are some practical examples of using class method decorators in Python?
Some practical examples of using class method decorators in Python are alternative constructors, logging decorators, and caching decorators. These examples demonstrate how class method decorators can be used to modify the behavior of a class method and add functionality to it.

## Refrences

- https://www.educba.com/python-classmethod-decorator/
- https://stackoverflow.com/questions/12179271/meaning-of-classmethod-and-staticmethod-for-beginner
