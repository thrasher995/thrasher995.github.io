---
layout: post
title: Python Generator Objects
subtitle: Generator functions & Generator expressions
categories: Python
tags: [generators, python, data engineering, data science]
mermaid: false
---

## What are Python Generators?
- Generator objects are objects that implement the iterator protocol (`next()` & `iter()` methods).
- Generator objects are **iterators**.
- Generators are useful when dealing with large sequences; as storing the sequence entirely is expensive.

## Creating Python Generators
1. Using Generator functions:
    - Functions that contain a `yield` statement, and return generators.
    
    ### Example 1: Creating a Generator object using a Generator function 

    ```
    def generator_function(stop_index):
    for n in range(stop_index):
        yield n

    generator_object = generator_function(5)
    print(type(generator_object))
    print(next(generator_object))
    print(next(generator_object))
    print(*generator_object)
    ```

    Output:

    ```
    <class 'generator'>
    0
    1
    2 3 4
    ```

2. Using Generator expressions:
    - An expression, similar to a list comprehension, that returns a generator object.
    - The syntax of a generator expression differs than that of a list comprehension by using `()` rather than `[]`.
    - Syntax:
    <pre>
    <i> identifier_name = (expression for item in iterable) </i>
    </pre>

    ### Example 2: Creating a Generator object using a Generator expression 

    ```
    generator_object = (i for i in range (0,5))
    print(type(generator_object))
    print(next(generator_object))
    print(next(generator_object))
    print(*generator_object)
    ```

    Output:

    ```
    <class 'generator'>
    0
    1
    2 3 4
    ```


