---
layout: post
title: Introduction to Python Functions
subtitle: Creating your own functions in Python
categories: python, functions
tags: [python, functions]
mermaid: false

---

# What is a function?
- A function is a block of code which only runs when invoked (called).
- Data can be passed to functions using arguments.
- A function can return data as a result.


## Defining a function:
1. To define a function in Python, the keyword **def** is used, and followed by the function's name, its arguments in brackets, and a colon.
2. A block of code is written after the colon, and is ended with the return statement **if the function returns any value(s)**.

### Creating your first function:
 
```
def first_function():
    print("Hello World!")

first_function()
```
Output:
``` 
Hello World!
```
- This function prints "Hello World!" when invoked.
- This function does not take any arguments and does not return any values.

## Docstrings:
- Describe what a function does, serving as documentation for it.
- Placed directly after the function's header, in between triple double-quotes (""" """).
- Do not show in output.
 
```
def first_function():
    """Prints "Hello World!" """
    print("Hello World!")

first_function()    # Invoking function
```
Output:
``` 
Hello World!
```

## Return statement:
- Used if the function returns value(s):

```
def first_function():
    """returns "Hello World!" """
    return("Hello World!")

print (first_function())    # Invoking function inside the print() method
```

Output:

``` 
Hello World!
```

### Returning multiple values:
- To return multiple values, Tuples (Python Data Structure) are used.

<pre>
def multiple_return_values():
    """returns "Hello World!" """
    output_string = "Hello World!"
    return (output_string, len(output_string), type(output_string))

print (multiple_return_values())    # Invoking function inside the print() method
</pre>

Output:

<pre>
('Hello World !', 13, <class 'str'>)
</pre>

## Arguments (Function's Parameters):
- Used to pass data into functions.
- Specified in the brackets after the function's name.
- Arguments are seperated using commas.

```
def raise_to_power(value, power):
    """returns (value^power) """
    raised_output = value ** power
    return raised_output

print(raise_to_power(3,3))
```
Output:
```
27
```

### Default Arguments:
- Default values indicate that the function argument will take that value if no argument value is passed during the function call.

- Example:
```
def raise_to_power(value, power=1):
    """returns (value^power) """
    raised_output = value ** power
    return raised_output

print(raise_to_power(3), raise_to_power(3,1), raise_to_power(3,3))
```
Output:
```
3 3 27
```
### Flexible Arguments (*args, **kwargs):
- In Python, we can pass a variable number of arguments to a function using special symbols: *args, **kwargs.
- `*args:` for Non-keyword arguments.
- `**kwargs:` for Keyword arguments.
- *args Example:
```
def args_adder(*args):
    """ Sums all values in arguments """
    sum = 0         # Initializing sum variable

    for num in args:
        sum += num
    print(sum)

args_adder(1)   # Invoking args_adder with arguments 1,
args_adder(1,2)   # Invoking args_adder with arguments 1,2
args_adder(1,2,3,4,5)   # Invoking args_adder with arguments 1,2,3,4,5
```
Output:
```
1
3
15
```
- **kwargs Example:
```
# Defining report_status
def report_status(**kwargs):    
    """Print out the status of a movie character."""

    print("\nBEGIN: REPORT\n")

    # Iterate over the key-value pairs of kwargs
    for key, val in kwargs.items():
        # Print out the keys and values, separated by a colon ':'
        print(key + ": " + val)

    print("\nEND REPORT")

# First call to report_status()
report_status(name="luke", affiliation="jedi", status="missing")

# Second call to report_status()
report_status(name="anakin", affiliation="sith lord", status="deceased")

```
Output:
```
BEGIN: REPORT

name: luke
affiliation: jedi
status: missing

END REPORT

BEGIN: REPORT

name: anakin
affiliation: sith lord
status: deceased

END REPORT
```




## Nested Functions:
- A function within another.

```
def outer_function(arg1,arg2,arg3):
    """Returns whether the arguments are even or odd as a Tuple"""
    def inner_function(x):
        """Returns "Even" if argument is even and "odd" if argument is odd """
        if (x % 2 == 0):
            return "Even"
        else:
            return "Odd"

    return (inner_function(arg1),inner_function(arg2),inner_function(arg3))

print (outer_function(1,2,4))
```
Output:
```
('Odd', 'Even', 'Even')
```
- The scope of outer_function is an **enclosing scope** to inner_function.

### Another Nested Functions Example:
```
def echo(n):
    """Return the inner_echo function."""

    # Define inner_echo
    def inner_echo(word1):
        """Concatenate n copies of word1."""
        echo_word = word1 * n
        return echo_word
    
    return inner_echo


# Call echo: twice
twice = echo(2)
print(type(twice))    # Invoking type(twice) inside the print() method

# Call echo: thrice
thrice = echo(3)

# Call twice() and thrice() then print
print(twice('hello'), thrice('hello'))
```

Output:

```
<class 'function'>
hellohello hellohellohello
```

- In this example, the **echo** function returns **inner_echo** function, with 2 taken as an argument for the **echo** function. This can also be seen in the output of print(type(twice)) in the outputs block.
- This means that our call to twice('hello') is equivalent to the code below:

```
def echo(2):
    """Return the inner_echo function."""

    # Define inner_echo
    def inner_echo('hello'):
        """Concatenate n copies of word1."""
        echo_word = word1 * n
        return echo_word
    
    return inner_echo


# Call echo: twice
twice = echo(2)
print(type(twice))
# Call echo: thrice
thrice = echo(3)

# Call twice() and thrice() then print
print(twice('hello'), thrice('hello'))
```
