---
layout: post
title: Comprehensions
subtitle: Shorter syntax, same results
categories: Python
tags: [python, list comprehensions]
mermaid: false
---
## Why use Comprehensions?
- Easier to create new lists/dictionaries from existing lists/dictionaries using shorter syntax.
- Applicable to all iterables and is not exlusive to lists/dictionaries.
- Faster than `for` loops when creating lists:
    - This is because the `append()` method is being called in each iteration in `for` loops.


## Creating New Lists from Existing Lists
 - Syntax (without if condition):
<pre>
<i> list_name = [expression for item in iterable] </i>
</pre>
- Syntax (with if condition):
<pre>
<i> list_name = [expression for item in iterable if condition] </i>
                    or
<i> list_name = [expression if condition else else_expression for item in iterable] </i>
</pre>


- Components:
    - an iterable
    - an iterator variable
    - output expression

### Example 1: Multiplying Elements in a List by 10
```
old_list = [7,15,140,21,135,174,61,13]
new_list_for = []
new_list_comp = []

# Populating list using traditional for loop
for element in old_list:
    new_list_for.append(element*10)

# Populating list using list comprehension
new_list_comp = [(element*10 )for element in old_list]

# Printing all lists
print(old_list)
print(new_list_for)
print(new_list_comp)
```
Output: (Notice that printing new_list_for & new_list_comp gives the same result)
```
[7, 15, 140, 21, 135, 174, 61, 13]
[70, 150, 1400, 210, 1350, 1740, 610, 130]
[70, 150, 1400, 210, 1350, 1740, 610, 130]
```

### Example 2: List Comprehension + if statement (appending elements less than or equal to 100)
```
old_list = [7,15,140,21,135,174,61,13]
new_list_for = []
new_list_comp = []

# Populating list using traditional for loop
for element in old_list:
    if element <= 100:              # If statement
        new_list_for.append(element)

# Populating list using list comprehension + if statement
new_list_comp = [(element)for element in old_list if element <= 100]

# Printing all lists
print(old_list)
print(new_list_for)
print(new_list_comp)
```
Output: (Notice that printing new_list_for & new_list_comp gives the same result)
```
[7, 15, 140, 21, 135, 174, 61, 13]
[7, 15, 21, 61, 13]
[7, 15, 21, 61, 13]
```
### Example 3: List Comprehension + if & else statements
```
old_list = [7,15,140,21,135,174,61,13]
new_list_for = []
new_list_comp = []

# Populating list using traditional for loop
for element in old_list:
    if element <= 100:              # If statement
        new_list_for.append(element)
    else:                           # Else: add (element-100) to list
        new_list_for.append(element-100)
# Populating list using list comprehension + if statement + else expression
new_list_comp = [element if element <= 100 else (element-100) for element in old_list ]

# Printing all lists
print(old_list)
print(new_list_for)
print(new_list_comp)
```
Output: (Notice that printing new_list_for & new_list_comp gives the same result)
```
[7, 15, 140, 21, 135, 174, 61, 13]
[7, 15, 40, 21, 35, 74, 61, 13]
[7, 15, 40, 21, 35, 74, 61, 13]
```


## Replacing Nested `for` Loops
- Readibility is worse when using list comprehension here.

### Example 1: (element, element ** i) <--> Raised to Powers (1,2,3)
```
old_list = [2,3,4]
new_list_for = []
new_list_comp = []

# Populating list using traditional nested for loops
for element in old_list:
    for i in range(1,4):
        new_list_for.append((element,element**i))

# Populating list using list comprehension with 2 for clauses
new_list_comp = [(element,element**i)for element in old_list for i in range(1,4)]

# Printing all lists
print(old_list)
print(new_list_for)
print(new_list_comp)
```
Output: 
```
[2, 3, 4]
[(2, 2), (2, 4), (2, 8), (3, 3), (3, 9), (3, 27), (4, 4), (4, 16), (4, 64)]
[(2, 2), (2, 4), (2, 8), (3, 3), (3, 9), (3, 27), (4, 4), (4, 16), (4, 64)]
```

### Example 2: Same as Example 1 + if statement (only add even numbers to list)
```
old_list = [2,3,4]
new_list_for = []
new_list_comp = []

# Populating list using traditional nested for loops
for element in old_list:
    if element % 2 ==0:
        for i in range(1,4):
            new_list_for.append((element, element ** i))

# Populating list using list comprehension with 2 for clauses
new_list_comp = [(element,element**i)for element in old_list for i in range(1,4) if element % 2==0]

# Printing all lists
print(old_list)
print(new_list_for)
print(new_list_comp)
```
Output: 
```
[2, 3, 4]
[(2, 2), (2, 4), (2, 8), (4, 4), (4, 16), (4, 64)]
[(2, 2), (2, 4), (2, 8), (4, 4), (4, 16), (4, 64)]
```
## Creating Dictionaries
 - Curly braces `{}` are used instead of square-brackets `[]`.

- Syntax (without if condition):
<pre>
<i> dict_name = {key: value for key in iterable} </i>
</pre>

- Syntax (with if condition):
<pre>
<i> dict_name = {key: value for key in iterable if condition} </i>
                    or
<i> dict_name = {key: (value if condition) for key in iterable} </i>                    
</pre>

- Syntax (with if-else):
<pre>
<i> dict_name = {key: value for key in iterable if condition} </i>
                    or
<i> dict_name = {key: (value if condition else else_statement) for key in iterable} </i>                  
</pre>

### Example: Dictionary Comprehension with if-else
```
engines_displacement_dict = {'4A': 1.6, 'SR20':2.0, '1JZ':2.5, '2JZ':3.0,'3S':2.0}
eng_dict_for = {}

for k,v in engines_displacement_dict.items():
    if v > 2:
        eng_dict_for[k] = v
    else:
        eng_dict_for[k] = "Less than 2.0"
eng_dict_comp = {k: (v if v>2 else "Less than 2.0") for k,v in engines_displacement_dict.items()}
print(engines_displacement_dict)
print(eng_dict_for)
print(eng_dict_comp)
```
Output:
```
{'4A': 1.6, 'SR20': 2.0, '1JZ': 2.5, '2JZ': 3.0, '3S': 2.0}
{'4A': 'Less than 2.0', 'SR20': 'Less than 2.0', '1JZ': 2.5, '2JZ': 3.0, '3S': 'Less than 2.0'}
{'4A': 'Less than 2.0', 'SR20': 'Less than 2.0', '1JZ': 2.5, '2JZ': 3.0, '3S': 'Less than 2.0'}
```



