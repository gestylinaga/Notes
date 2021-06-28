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

*Logging* is a great way to understand what's happening in your program and in what order it's
happening. Python's `logging` module makes it easy to create a record of custom messages that you 
write

### Using the logging Module

To enable the `logging` module to display log messages on your screen as your program runs:
```python
#!/usr/bin/env python3
import logging
logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s -  %(levelname)
s -  %(message)s')
```
Note:
* the code is at the top of the program, but still beneath the hashbang `#!` line
* when Python logs an event, it creates a *LogRecord* object
* the `logging` module's `basicConfig()` function lets you specify what details about the *LogRecord*
object you want to see

Example program *factorialLog.py*:(for finding factorials)
```python
import logging
logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s -  %(levelname)s -  %(message)s')
logging.debug('Start of program')

def factorial(n):
    logging.debug('Start of factorial(%s%%)' % (n))
    total = 1
    for i in range(n + 1): # intentional error here
        total *= i
        logging.debug('i is ' + str(i) + ', total is ' + str(total))
    logging.debug('End of factorial(%s%%)' % (n))
    return total

print(factorial(5))
logging.debug('End of program')
```
this returns:
```
 2021-06-27 21:19:08,632 -  DEBUG -  Start of program
 2021-06-27 21:19:08,632 -  DEBUG -  Start of factorial(5%)
 2021-06-27 21:19:08,632 -  DEBUG -  i is 0, total is 0
 2021-06-27 21:19:08,632 -  DEBUG -  i is 1, total is 0
 2021-06-27 21:19:08,632 -  DEBUG -  i is 2, total is 0
 2021-06-27 21:19:08,632 -  DEBUG -  i is 3, total is 0
 2021-06-27 21:19:08,632 -  DEBUG -  i is 4, total is 0
 2021-06-27 21:19:08,632 -  DEBUG -  i is 5, total is 0
 2021-06-27 21:19:08,632 -  DEBUG -  End of factorial(5%)
0
 2021-06-27 21:19:08,632 -  DEBUG -  End of program
```
Notice how the total is `0` which is incorrect

This happens because the `for` loop is starting at `0`, which multiplied by anything is also `0`

so changing the `for` loop line to: `for i in range(1, n + 1)` (to change the starting range to 1) 
and running the program again returns:
```
 2021-06-27 21:21:16,631 -  DEBUG -  Start of program
 2021-06-27 21:21:16,631 -  DEBUG -  Start of factorial(5%)
 2021-06-27 21:21:16,631 -  DEBUG -  i is 1, total is 1
 2021-06-27 21:21:16,631 -  DEBUG -  i is 2, total is 2
 2021-06-27 21:21:16,631 -  DEBUG -  i is 3, total is 6
 2021-06-27 21:21:16,631 -  DEBUG -  i is 4, total is 24
 2021-06-27 21:21:16,632 -  DEBUG -  i is 5, total is 120
 2021-06-27 21:21:16,632 -  DEBUG -  End of factorial(5%)
120
 2021-06-27 21:21:16,632 -  DEBUG -  End of program
```
which shows the correct value of `120`

### Don't Debug with the print() Function

Typing:
```python
import logging
logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s -  %(levelname)s -  %(message)s')
```
every time might be annoying, but using `print()` calls instead is **not** a shortcut:
* you'll have to remove all the `print()` statements after debugging
    - possible to accidentaly delete *non-log* print statements
* can disable logging with 1 line
    - `logging.disable(logging.CRITICAL)`

Note that log messages are intended for the programmer, not the user

Users don't care about the contents of some dictionary value you need to help with debugging; This 
is where you would use logging

For messages that the user will want to see, like `'File not found'` or `'Invalid input, please 
enter a number'`, you wan't to use a `print()` call

### Logging Levels

*Logging Levels* provide a way to categorize your log messages by importance:

| Level | Logging function | Description |
| --- | --- | --- |
| DEBUG | `logging.debug()` | Lowest level. Used for small details. |
| INFO | `logging.info()` | Used to record information on general events in your program or confirm that things are working at their point in the program. |
| WARNING | `logging.warning()` | Used to indicate a potential problem that doesn't prevent the program from working but might do so in the future. |
| ERROR | `logging.error()` | Used to record an error that caused the program to fail to do something. |
| CRITICAL | `logging.critical()` | Highest level. Used to indicate a fatal error that has caused or is about to cause the program to stop running entirely. |

Note that logging levels are suggestions, and ultimately, it is up to you to decide which category 
your log message falls into

Examples:
```python
import logging
logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s -  %(levelname)s -  %(message)s')

logging.debug('Some debugging details.')
# this returns: 2021-06-27 23:22:46,797 -  DEBUG -  Some debugging details.

logging.info('The logging module is working.')
# this returns: 2021-06-27 23:23:03,507 -  INFO -  The logging module is working.

logging.warning('An error message is about to be logged.')
# this returns: 2021-06-27 23:23:23,828 -  WARNING -  An error message is about to be logged.

logging.error('An error has occured.')
# this returns: 2021-06-27 23:23:45,824 -  ERROR -  An error has occured. 

logging.critical('The program is unable to recover!')
# this returns: 2021-06-27 23:24:01,959 -  CRITICAL -  The program is unable to recover!
```
The benefits of using logging levels is that you can change what priority of logging message you 
want to see:
* passing `logging.DEBUG` to the `basicConfig()` function's `level` keyword (the lowest level), 
will show messages from **all** logging levels
* similarly, passing `logging.ERROR`, will only show ERROR and CRITICAL messages (skipping the 
lower levels DEBUG, INFO, and WARNING)

### Disabling Logging

The `logging.disable()` function disables logging messages, saving you from removing all logging 
calls by hand

You simply pass `logging.disable()` a logging level, and it will suppress all log messages at that 
level or lower

For example, adding `logging.disable(logging.CRITICAL)` will disable logging entirely:
```python
import logging
logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s -  %(levelname)s -  %(message)s')

logging.critical('Critical error! Critical error!')
# this returns: 2021-06-27 23:31:54,908 -  CRITICAL -  Critical error! Critical error!

logging.disable(logging.CRITICAL) # No logging after this point
logging.critical('Critical error! Critical error!')
logging.error('Error! Error!')
```
Note that since `logging.disable()` will disable all messages **after** it, it is wise to put it 
near the `import logging` line. This way, you can easily find it to comment/uncomment the call as 
needed.

### Logging to a File

Instead of displaying the log messages to the screen, you can write them to a text file

The `logging.basicConfig()` function takes a `filename` keyword argument like so:
```python
import logging
logging.basicConfig(filename='myProgramLog.txt', level=logging.DEBUG, format=' %(asctime)s -  %(levelname)s -  %(message)s')
```
In this example, the log messages will be saved to a file named: `myProgramLog.txt`


## Mu's Debugger

The *debugger* is a feature of the Mu editor, IDLE, and other editor software that allows you to 
execute your program **one line at a time**

The debugger will run a single line of code, and then wait for you to tell it to continue

To run the debugger in Mu, click the `Debug` button in the top row of buttons

Other Buttons:
* `Continue` will cause the program to execute normally until it terminates or reaches a *breakpoint*
* `Step In` will cause the debugger to execute the next line of code and then pause again
    - if the next line is a function call, the debugger will "step into" that function, and jump to the first line of that function
* `Step Over` will execute the next line of code, similar to `Step In`, but will execute functions at normal speed before pausing again
* `Step Out` will cause the debugger to execute lines of code at full speed until it returns from the current function
    - used if you have "stepped into" a function, and want to quickly get out
* `Stop` will stop debugging entirely, immediately terminating the program without executing the rest of the program

### Debugging a Number Adding Program

### Breakpoints

A *breakpoint* can be set on a specific line of code and forces the debugger to pause whenever it 
reaches that line


## Summary

Assertions, exceptions, logging, and the debugger are all valuable tools to find and prevent bugs in 
your program:
* Assertions with `assert` statements are a good way to implement "Sanity Checks"
    - only for errors that the program shouldn't try to recover from
* An exception can be caught with the `try`/`except` statements
* The `loggging` module is a good way to look into your code while it's running
    - more convenient than using `print()` calls to debug
* The debugger lets you step through your program one line at a time
    - alternatively, you can run it at regular speed, but stop at a *breakpoint*


## Practice Questions

1. Write an assert statement that triggers an AssertionError if the variable spam is an integer 
less than 10.
    - `assert (spam.isdecimal()) and (spam < 10)`
2. Write an assert statement that triggers an AssertionError if the variables eggs and bacon 
contain strings that are the same as each other, even if their cases are different (that is, 
'hello' and 'hello' are considered the same, and 'goodbye' and 'GOODbye' are also considered the 
same).
    - `assert eggs.lower() != bacon.lower()`
3. Write an assert statement that always triggers an AssertionError.
    - `assert True`
4. What are the two lines that your program must have in order to be able to call logging.debug()?
    - `import logging`
    - `logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s -  %(levelname)s -  %(message)s')`
5. What are the two lines that your program must have in order to have logging.debug() send a 
logging message to a file named programLog.txt?
    - `import logging`
    - `logging.basicConfig(filename='programLog.txt', level=logging.DEBUG, format=' %(asctime)s -  %(levelname)s -  %(message)s')`
6. What are the five logging levels?
    - DEBUG (lowest)
    - INFO
    - WARNING
    - ERROR
    - CRITICAL (highest)
7. What line of code can you add to disable all logging messages in your program?
    - `logging.disable(logging.CRITICAL)`
8. Why is using logging messages better than using print() to display the same message?
    - `different logging levels`
    - `one line cleanup`
9. What are the differences between the Step Over, Step In, and Step Out buttons in the debugger?
    - `'Step Over' runs functions at full speed, then pauses`
    - `'Step In' jumps to first line of funtion, then pauses`
    - `'Step Out' is used after 'Step In' to run full speed until it exits the function`
10. After you click Continue, when will the debugger stop?
    - `program terminates, or hits a breakpoint`
11. What is a breakpoint?
    - `a line that forces your debugger to pause there`
12. How do you set a breakpoint on a line of code in Mu?
    - `click the line number, leaving a red dot`


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
