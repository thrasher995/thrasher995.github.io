---
layout: post
title: Exception Handling in Python
subtitle: try, catch, except, and finally
categories: Python
tags: [python, errors, handling, exceptions]
---

## Why is Exception Handling necessary?
- Python raises (throws) one of its many built-in Exceptions when the program encouters an error.
- When an Exception is raised, the interpreter stops the current process and passes it to the calling process until it's handled. 
- If the Exception is not handled, the program crashes.

### Example 1.1: Printing a variable that's not been defined
```Python
print(x)
```
Output:

<pre>
NameError: name 'x' is not defined</pre>

## `try` & `except` blocks:
- Instead of having the program crash, the Exception is handled in the **`except`** block.

### Example 2.1: Introducing `try` & `except` blocks
- Handling `Exception` with `print` statement:

```Python
try:
    print(x)
except:
    print("Variable not defined")
```

Output:
<pre>
Variable not defined</pre>


### Example 2.2: Excepting a specific Exception
- In this case, if a different Exception is raised, the program crashes (if not handled).

```Python
from math import sqrt
try:
    print(sqrt(-1))
    print(x)
except NameError:
    print("Variable not defined")
```

Output:
<pre>
ValueError: math domain error</pre>

### Example 2.3: Multiple `except` blocks
- Multiple `except` blocks can be used to handle different Exceptions differently:

1. `except` ValueError:

    ```Python
    from math import sqrt
    try:
        print(sqrt(-1))
    except NameError:
        print("Variable not defined")
    except ValueError:
        print("Can't find square root of negative value")
    ```

    Output:
    <pre>
    Can't find square root of negative value</pre>

2. `except` NameError:

    ```Python
    from math import sqrt
    try:
        print(x)
    except NameError:
        print("Variable not defined")
    except ValueError:
        print("Can't find square root of negative value")

    ```

    Output:
    <pre>
    Variable not defined</pre>


## `finally` block:
- The finally block is executed regardless of whether the try block raises an error or not.
### Example 3.1: Finally block with an Exception raised in try block

```Python
try:
    print(x)    # Throws NameError Exception
    print(1)    # This line is not executed because the previous line throws an Exception
except:
    print("Variable not defined")
finally:
    print("Hello World!")
```

Output:
<pre>
Variable not defined
Hello world!</pre>


### Example 3.2: Finally block with no Exceptions raised in try block

```Python
try:
    print(123)
except:
    print("Variable not defined")
finally:
    print("Hello World!")
```

Output:
<pre>
123
Hello world!</pre>

## Throwing/raising Exceptions:
`raise` Exception: throws an Exception
### Example 4.1: Throwing an Exception:

```Python
try:
    raise Exception("Exception Raised !")
except Exception as e:
    print(str(e))
    print("Exception Handled !!")
```

Output:
<pre>
Exception Raised !
Exception Handled !!</pre>

## Some Exceptions:
- `IndexError`: raised when a sequence subscript is out of range. (If an index is not an integer, TypeError is raised.)
- `TypeError`: raised when passing arguments of the wrong type (e.g. passing a list when an int is expected).
- `ValueError`: raised when an operation or function receives an argument that has the right type but an inappropriate value, and the situation is not described by a more precise Exception such as *IndexError*.
- `NameError`: raised when a local or global name is not found. 
<br/>This applies only to unqualified names. 
<br/>The associated value is an error message that includes the name that could not be found.
- `ZeroDivisionError`: raised when the second argument of a division or modulo operation is zero. 
<br/>The associated value is a string indicating the type of the operands and the operation.



