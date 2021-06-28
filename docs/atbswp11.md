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

Consider *errorExample.py*:
```python
def spam():
    bacon()

def bacon():
    raise Exception('This is the error message.')

spam()
```
this returns the traceback:
```
Traceback (most recent call last):
  File "errorExample.py", line 7, in <module>
    spam()
  File "errorExample.py", line 2, in spam
    bacon()
  File "errorExample.py", line 5, in bacon
    raise Exception('This is the error message.')
Exception: This is the error message.
```
Notice that the error occurs on `line 5`, which was called by `line 2`, which in turn was called by 
`line 7`. This is helpful in programs where functions can be called from multiple places, the call 
stack can help determine which call led to the error

Python displays the traceback whenever a raised exception goes unhandled, but you can also obtain it 
as a string by calling `traceback.format_exc()`. This is useful if you want the information from an 
exception's traceback, but also want an `except` statement to gracefully handle the exception. (Note 
that this requires importing Python's `traceback` module)

You can write the traceback information to a text file, and keep your program running:
```python
import traceback

try:
    raise Exception('This is the error message.')
except:
    errorFile = open('errorInfo.txt', 'w')
    errorFile.write(traceback.format_exc())
    errorFile.close()
    print('The traceback info was written to errorInfo.txt.')

# this returns:
# 111 (the number of characters written)
# The traceback info was written to errorInfo.txt.
```


## Assertions

An **assertion** is a sanity check to make sure your code isn't doing something obviously wrong

These 'sanity checks' are performed by `assert` statements, and if failed raise an `AssertionError` 
exception

An `assert` statement consists of:
* the `assert` keyword
* a condition (a `True`/`False`)
* a comma `,`
* a string to display when the condition is `False`

In plain english: "I assert that the condition holds true, and if not, there is a bug somewhere, so 
immediately stop the program."

```python
ages = [26, 57, 92, 54, 22, 15, 17, 80, 47, 73]
ages.sort()
ages

# this returns:
# [15, 17, 22, 26, 47, 54, 57, 73, 80, 92]

assert ages[0] <= ages[-1] # asserts that the first age is <= the last age
```
Note that the `assert` statement here, asserts that the first item in `ages` should be less than or 
equal to the last one. **This is the sanity check**. If the code in `sort()` is bug-free, then the 
assertation would be true. Because the `ages[0] <= ages[-1]` expression returns `True`, nothing 
happens.

However, if an error does occur: (like using `reverse()` instead of `sort()`)
```python
ages = [26, 57, 92, 54, 22, 15, 17, 80, 47, 73]
ages.reverse()
ages

# this returns:
# [73, 47, 80, 17, 15, 22, 54, 92, 57, 26]

assert ages[0] <= ages[-1] # asserts that the first age is <= the last age
```
this returns:
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError
```
Unlike exceptions, your code should **not** handle `assert` statements with `try`/`except`

If an `assert` fails, your program **should** crash, and shorten the time between the original cause 
of the but and when you first notice it. This reduces the amount of code you will have to check 
before finding the bug's cause

Assertions are for programmer errors, not user errors

Meaning they should **not** be used in place of exception statements

> Note that Python scripts run with the `-O` flag like this:
>> `python3 -O myScript.py`
>
> will skip `assert` statements
>
> this can be used when running in a production setting that requires peak performance

Note that assertions also aren't a replacement for comprehensive testing

### Using an Assertion in a Traffic Light Simulation

Consider building a traffic light simulation program
* the stoplights of the intersection are represented as a dictionary
    - key `'ns'` for north-south stoplights
    - key `'ew'` for east-west stoplights
    - values as strings: `'green'`, `'yellow'`, `'red'`

Example:
```python
market_2nd = {'ns': 'green', 'ew': 'red'}
mission_16th = {'ns': 'red', 'ew': 'green'}
```
so a simple function **could** be:
```python
def switchLights(stoplight):
    for key in stoplight.keys():
        if stoplight[key] == 'green':
            stoplight[key] = 'yellow'
        elif stoplight[key] == 'yellow':
            stoplight[key] = 'red'
        elif stoplight[key] == 'red':
            stoplight[key] = 'green'

switchLights(market_2nd)
```
While the program **won't** crash, the virtual cars will, unless you add this `assert` statement:
```python
assert 'red' in stoplight.values(), 'Neither light is red! ' + str(stoplight)
```
this ensures that at least 1 direction is always red, and will return this error message:
```
Traceback (most recent call last):
    File "carSim.py", line 14, in <module>
        switchLights(market_2nd)
    File "carSim.py", line 13, in switchLights
        assert 'red' in stoplight.values(), 'Neither light is red! ' +
   str(stoplight)
   AssertionError: Neither light is red! {'ns': 'yellow', 'ew': 'green'}
```
While your program crashing is not ideal, it immediately points out that a sanity check failed, and 
can save you a lot of future debugging effort


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
