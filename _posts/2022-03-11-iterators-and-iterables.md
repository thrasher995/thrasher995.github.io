---
layout: post
title: Introduction to Iterators & Iterables
subtitle: Iterators vs Iterables
categories: Python
tags: [iterators, iterables, python]
mermaid: false
---

## Iterables
- An iterable is a Python object with an associated `iter()` method.
- Examples on iterables: Lists, Tuples, Strings, Sets, Dictionaries, and File Connections.

## Iterators
- An iterator is an object that contains a countable number of values that can be iterated upon.
- Applying `iter()` to an iterable returns an iterator object.
- Applying `next()` to an iterator iterates over the iterable.
- The `StopIteration` Exception is raised to signal that there are no further items produced by the iterator.
- The Star/Splat ( `*` ) operator is used to unpack all elements of an **iterator** or an **iterable** at once.
- Iterating over an iterator object "consumes" the elements inside the iterator object.
- If values in an iterator are to be kept, the iterator is cast to an iterable (List, Tuple,etc.).

### Example 1: Iterating using `next()`
```
string_obj = 'no'                   # Creating an iterable object
iterator_obj = iter(string_obj)     # Creating Iterator object
print(next(iterator_obj))           # Applying next() method to Iterator obj.
print(next(iterator_obj))           # Applying next() method to Iterator obj.
```
Output:
```
n
o
```

### Example 2: `StopIteration` Exception

```
string_obj = 'no'                   # Creating an iterable object
iterator_obj = iter(string_obj)     # Creating Iterator object
print(next(iterator_obj))           # Applying next() method to Iterator obj.
print(next(iterator_obj))           # Applying next() method to Iterator obj.
print(next(iterator_obj))           # Applying next() method to Iterator obj.
```
Output:
```
Traceback (most recent call last):
  File "path.../file.py", line 5, in <module>
    print(next(iterator_obj))
StopIteration
n
o
```

### Example 3: Star/Splat (`*`) Operator

```
string_obj = 'no'                   # Iterable object
iterator_obj = iter(string_obj)     # Iterator object
print(*iterator_obj)                # * operator used on an Iterator
print(*string_obj)                  # * operator used on an iterable

```
Output:
```
n o
n o
```

### Example 4-a: Consuming elements in an Iterator - `*` Operator twice

```
string_obj = 'Hello World !'                # Iterable object
iterator_obj = iter(string_obj)             # Iterator object
print(*iterator_obj)                        # * operator used on an iterator
print(*iterator_obj)                        # * operator used on an iterator

```
Output: (notice `new line` in the end of the Output window)
```
Hello World !

```

### Example 4-b: Consuming elements in an Iterator - Mixing `*` & `next()`

```
string_obj = 'Hello World !'            # Creating iterable object
iterator_obj = iter(string_obj)         # Creating iterator object
print(next(iterator_obj))               # Applying next() method to iterator obj.
print(next(iterator_obj))               # Applying next() method to iterator obj.
print(*iterator_obj)                    # * operator used on an iterator
print(*iterator_obj)                    # * operator used on an iterator

```
Output: (notice `new line` in the end of the Output window)
```
H
e
l l o   W o r l d   !

```

## Iterating Over Dictionaries
- Key & Value pairs in a dictionary are unpacked using `items()` method.

### Example: Using `items()` method

```
engines_displacement_dict = {'4A': '1.6L', 'SR20':'2.0L', '1JZ':'2.5L', '2JZ':'3.0L','3S':'2.0L'}
for k,v in engines_displacement_dict.items():
    print(k,v)
```
Output:
```
4A 1.6L
SR20 2.0L
1JZ 2.5L
2JZ 3.0L
3S 2.0L
```

## Iterating Over File Connections
- `iter()` & `next()` methods are used.

### Example 1-a: Using `next()`

```
my_file = open('file.txt')
file_iterator = iter(my_file)

print(next(file_iterator))   
print(next(file_iterator))     

```

Output: (New Lines are at end of rows in .txt file as `\n` as seen in 1-b)
```
FIRST LINE

SECOND LINE

```

### Example 1-b: Casting Iterator object to Tuple & printing it

```
my_file = open('file.txt')
file_iterator_tup = tuple(iter(my_file))
print(file_iterator_tup)     

```

Output: (New Lines are at end of rows in .txt file as `\n`)
```
('FIRST LINE\n', 'SECOND LINE\n', 'THIRD LINE\n', 'FOURTH LINE')
```

### Example 1-c: Using `next()`, casting to String, and `strip()` method
- Removing New Line

```
my_file = open('file.txt')
file_iterator = iter(my_file)

print(str(next(file_iterator)).strip())     # strip() method is used to ignore \n at end of line
print(str(next(file_iterator)).strip())     # strip() method is used to ignore \n at end of line

```

Output:
```
FIRST LINE
SECOND LINE
```
### Example 2: Using `*`

```
my_file = open('file.txt')
file_iterator = iter(my_file)

print(*file_iterator)

```

Output: (Space is present at beginning of each line due to \n from before)
```
FIRST LINE
 SECOND LINE
 THIRD LINE
 FOURTH LINE
```

## `enumerate()` Method:
- Returns an enumerate object, which is an iterable.

- Syntax:

<pre>
<i> enumerate(iterable, start=0) </i>

Iterable: any object that supports iteration
Start:  the index value from which the counter is 
        to be started, by default it is 0
</pre>


### Example 1: Creating an enumerate object using `enumerate()`

```
string_obj = 'Hello'                        # Creating an iterable object
enumerate_object = enumerate(string_obj)    # Creating an enumerate object
print(type(enumerate_object))               
enumerate_list = list(enumerate_object)     # Casting enumerate object to list
print(enumerate_list)
```
Output:
```
<class 'enumerate'>
[(0, 'H'), (1, 'e'), (2, 'l'), (3, 'l'), (4, 'o')]
```

### Example 2: Looping over an enumerate object
```
string_obj = 'Hello'                        # Creating an iterable object
enumerate_object = enumerate(string_obj)    # Creating an enumerate object
for index, value in enumerate_object:       # Looping over enumerate object
    print(index,value)
```
Output:
```
0 H
1 e
2 l
3 l
4 o
```

### Example 3: Changing `start` argument
```
string_obj = 'Hello'                            # Creating an iterable object
enumerate_object = enumerate(string_obj, 2)     # Creating an enumerate object
for index, value in enumerate_object:           # Looping over enumerate object
    print(index,value)
```
Output:
```
2 H
3 e
4 l
5 l
6 o
```

## `zip()` method
- Returns a zip object.
- Syntax:

<pre>
Pre-Python 3.10:
 <i> zip(*iterables) </i>
Python 3.10+:
 <i> zip(*iterables, strict=False) </i>

</pre>
* Note: with strict=False(default option), zip() stops when the shortest iterable is exhausted. It will ignore the remaining items in the longer iterables

### Example 1-a: Creating a zip object (iterables in arguments of equal lengths)
```
list1 = ['Toyota','Mitsubishi', 'Mazda', 'BMW','Nissan','Golf']         # len(list1) = 6
list2= ['Supra', 'Lancer Evolution', 'RX-7','M1','Skyline GT-R','R32']  # len(list2) = 6
zip_object = zip(list1,list2)
print(list(zip_object))
```
Output:
```
[('Toyota', 'Supra'), ('Mitsubishi', 'Lancer Evolution'), ('Mazda', 'RX-7'), ('BMW', 'M1'), ('Nissan', 'Skyline GT-R'), ('Golf', 'R32')]
```

### Example 1-b: Creating a zip object (iterables in arguments of unequal lengths)
```
list1 = ['Toyota','Mitsubishi', 'Mazda', 
         'BMW','Nissan','Golf','Audi','Ferrari','Mercedes Benz']            # len(list1) = 9
list2= ['Supra', 'Lancer Evolution', 'RX-7','M1','Skyline GT-R','R32']      # len(list2) = 6
zip_object = zip(list1,list2)
print(list(zip_object))
```
Output:
```
[('Toyota', 'Supra'), ('Mitsubishi', 'Lancer Evolution'), ('Mazda', 'RX-7'), ('BMW', 'M1'), ('Nissan', 'Skyline GT-R'), ('Golf', 'R32')]
```


