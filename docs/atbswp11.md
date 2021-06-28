# Debugging

"Writing code accounts for 90 percent of programming. Debugging code accounts for the 
other 90 percent."

Computers only do what you tell them to do, **not** what you *intended* them to do

## Raising Exceptions

As seen in chapter 3, `try` and `except` statements can handle Python's exceptions to errors, but 
you can also raise your own exceptions

Raising an exception is a way of saying "Stop running the code in this function and move the 
program execution to the `except` statement."

A `raise` statement consists of:
* the `raise` keyword
* a call to the `Exception()` function
* a string with a helpful error message passed to the `Exception()` function

For Example:
```python
raise Exception('This is the error message.')
```
this returns:
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
Exception: This is the error message.
```
Note that if there are no `try` and `except` statements covering the `raise` statement that raised 
the exception, the program simply crashes and displays the error message

Usually a `raise` statement is inside a function, and the `try`/`except` statements in the code 
calling the function, like so:
```python
# boxPrint.py

# notice the `raise` statements inside this function
def boxPrint(symbol, width, height):
    if len(symbol) != 1:
        raise Exception('Symbol must be a single character string.')
    if width <= 2:
        raise Exception('Width must be greater than 2.')
    if height <= 2:
        raise Exception('Height must be greater than 2.')

    print(symbol * width)
    for i in range(height - 2):
        print(symbol + (' ' * (width - 2)) + symbol)
    print(symbol * width)


# notice the `try`/`except` statements here, where the function is called
for sym, w, h in (('*', 4, 4), ('O', 20, 5), ('x', 1, 3), ('ZZ', 3, 3)):
    try:
        boxPrint(sym, w, h)
    except Exception as err:
        print('An exception happened: ' + str(err))
```
this returns:
```
****
*  *
*  *
****
OOOOOOOOOOOOOOOOOOOO
O                  O
O                  O
O                  O
OOOOOOOOOOOOOOOOOOOO
An exception happened: Width must be greater than 2.
An exception happened: Symbol must be a single character string.
```
Notice how the first two examples work out fine, but the combination of `raise` and `try`/`except` 
statements return the error instead of crashing


## Getting the Traceback as a String

When Python encounters an error, it produces a **traceback**

A traceback includes:
* the error message
* the line number of the line that caused the error
* the sequence of the function calls that led to the error (aka the *call stack*)


## Assertions

### Using an Assertion in a Traffic Light Simulation


## Logging

### Using the logging Module

### Don't Debug with the print() Function

### Logging Levels

### Disabling Logging

### Logging to a File


## Mu's Debugger

### Debugging a Number Adding Program

### Breakpoints


## Summary


## Practice Questions

1. Write an assert statement that triggers an AssertionError if the variable spam is an integer 
less than 10.
2. Write an assert statement that triggers an AssertionError if the variables eggs and bacon 
contain strings that are the same as each other, even if their cases are different (that is, 
'hello' and 'hello' are considered the same, and 'goodbye' and 'GOODbye' are also considered the 
same).
3. Write an assert statement that always triggers an AssertionError.
4. What are the two lines that your program must have in order to be able to call logging.debug()?
5. What are the two lines that your program must have in order to have logging.debug() send a 
logging message to a file named programLog.txt?
6. What are the five logging levels?
7. What line of code can you add to disable all logging messages in your program?
8. Why is using logging messages better than using print() to display the same message?
9. What are the differences between the Step Over, Step In, and Step Out buttons in the debugger?
10. After you click Continue, when will the debugger stop?
11. What is a breakpoint?
12. How do you set a breakpoint on a line of code in Mu?


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
