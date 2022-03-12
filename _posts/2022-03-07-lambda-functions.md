---
layout: post
title: Lambda Functions in Python
subtitle: map(), filter(), reduce()
categories: Python
tags: [python, lambda, functions]
mermaid: false

---

## What is a Lambda function?
- A lambda function is a small anonymous function.
- A lambda function can take any number of arguments, but can only have one expression.
- Syntax:

<pre>
<i> lambda arguments : expression </i>
</pre>

### Example (1):
```
x = lambda argument : 2 ** argument
print(x(3))
```
Output:
```
8
````
### Example (2): **Nested Functions**
```
def raise_to_power(n):              # Defining raise_to_power function with one argument: n
    """ Returns lambda function """
    return lambda base: base ** n 

cube = raise_to_power(3)    # Sets n=3 for cube
# type(cube) -> function that takes one argument: base

print(cube(2))  # Prints 2^3
```
Output:
```
8
```

## `map` function:
- Returns a map object (which is an iterator) of the results after applying the given function to each item of a given iterable (list, tuple,...).
- Syntax:

<pre>
<i> map(function, iterable_object) </i>
</pre>

### Example 1: Squaring values in a Tuple using map()
- Casting map object to list, then printing:
```
my_tuple = (1,2,3)
squaring_map = map(lambda x: x**2, my_tuple)
print(list(squaring_map))
```
Output:
```
[1, 4, 9]
```
- Printing twice:
```
my_tuple = (1,2,3)
squaring_map = map(lambda x: x**2, my_tuple)
print(list(squaring_map))
print(list(squaring_map))
```
Output:
```
[1, 4, 9]
[]
```
- As noticed here, the second print statement printed an empty `list` even though no modifications were done to the **squaring_map** object.
- This is because iterating over the map object "consumed" it, and all values it held were lost.
- To fix this issue, cast the **squaring_map** object to list or tuple.

### Example 2: Fixing the previous example
```
my_tuple = (1,2,3)
squared_tuple = tuple(map(lambda x: x**2, my_tuple))
print(list(squared_list))
print(list(squared_list))
print(tuple(squared_list))
```
Output:
```
[1, 4, 9]
[1, 4, 9]
(1, 4, 9)
```

## `filter` function:
- Returns a filter object (which is an iterator) of the results after testing each element in a given iterable (list, tuple,...) to be true or not.
- Similar to map objects, cast the filter object to list or tuple to keep values.
 
- Syntax:
<pre>
<i> filter(function, iterable_object) </i>
</pre>

### Example: Filter values greater than or equal to 7
```
my_tuple = (11,2,5,7,10,119)
filtered_tuple = tuple(filter(lambda x: x>=7,my_tuple))
print(filtered_tuple)
```
Output:
```
(11, 7, 10, 119)
```

## `reduce` function:
- Used to apply a particular function passed in its argument to all of the iterable's elements mentioned in the sequence passed along, reducing the elements to a single element.
- Type of returned object depends on the type of elements in the iterable.
- Defined in the **functools** module.
 
- Syntax:
<pre>
<i> reduce (function, iterable) </i>
</pre>

### Example:
```
from functools import reduce
string_tuple = ("Hello"," ","World","!")
integers_tuple = (20,30,37)
floats_tuple = (20.0,30,37)
reduced_string = reduce((lambda x,y: x+y),string_tuple)
reduced_integers = reduce((lambda x,y:x+y),integers_tuple)
reduced_floats = reduce((lambda x,y:x+y),floats_tuple)
print(reduced_string,":", type(reduced_string))
print(reduced_integers,":", type(reduced_integers))
print(reduced_floats,":", type(reduced_floats)) 
```
Output:
```
Hello World! : <class 'str'>
87 : <class 'int'>
87.0 : <class 'float'>
```

