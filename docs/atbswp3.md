# Chapter 3: Functions

A *function* is like a miniprogram within a program
```python
def hello():
    print("hi!")
    print("hello there.")
    print("helloHello?")

hello()
```

Consist of:

* The `def` statement -- defines a function in the example called `hello`

* The *body* of the statement -- the block of code following the `def` statement

* A **Function Call** -- the name of the function with `()` appended to the end, possibly with some arguments

Remember: functions are run when they are called, **not** when they are defined


## def Statements with Parameters

**Arguments** -- values you can pass in the `()` of functions
```python
def hello(name):
    print('Hey there, ' + name)

hello('Bob')
hello('Alice')
```

**Parameters** -- variables that contain arguments -- `name` in the above example

* when a function is called with arguments, the arguments get stored in the parameters

* important to note that the values stored in parameters are lost/reset when the function returns

### Define, Call, Pass, Argument, Parameter

To Clarify any Confusion:
```python
def sayHello(name):
    print('Hello, ' + name)
sayHello('Al')
```

To **define** a function is to create it -- the `def sayHello(name):` line

To **call** a function is to send the execution to the top of the function's code -- the `sayHello('Al')` line

**Passing** is when the string value `'Al'`, is sent to the function -- the `sayHello('Al')` line sending code execution back to line 1

A value being passed to a function in a function call is an **Argument** -- the argument `Al` being assigned to the `name` variable

Variables with arguments are called **Parameters** -- the `name` variable after getting assigned the string `Al`


## Return Values and Return Statements

**Return Value** --  the value that a *function call* evaluates to

When creating a function using a `def` statement, you can specify what the return value should be with a **Return Statement**

**Return Statements** consist of:
* the `return` keyword
* the value/expression that the function should return

```python
import random

def getAnswer(answerNumber):
    if answerNumber == 1:
        return 'It is certain'
    elif answerNumber == 2:
        return 'Yes'
    elif answerNumber == 3:
        return 'Ask again later'
    elif answerNumber == 4:
        return 'My reply is no'
    elif answerNumber == 5:
        return 'Outlook is not good'

r = random.randint(1, 5)
fortune = getAnswer(r)
print(fortune)
```

Note that you can pass return values as an argument to another function call, meaning you can rewrite the last 3 lines as:
```python
print(getAnswer(random.randint(1, 5)))
```

Remember that *expressions* are composed of values and operators,
meaning a function call can be used in an expression because the call evaluates to its return value


## The None Value

In Python, the value `None` represents the absence of a value

* the `None` value is the only value of the *NoneType* data type

* other programming languages might call it `null`, `nil`, or `undefined`

* just like the Boolean data types (`True` and `False`), `None` must be typed with a capital `N`

```
>>> spam = print('Hello!')

Hello!
```

```
>>> None == spam

True
```

* helpful when you need to store something that won't be confused for a real value in a variable

* ie: the return value for `print()`

    + the `print()` function displays text on the screen, but doesn't need a return value like `len()` or `input()` do

    + but since all functions need to evaluate to a return value, `print()` returns `None`

Python automatically adds `return None` to to end of any function definition with no return statement

This is similar to how a `while` or `for` loop implicitly ends with a `continue` statement, even if one isn't supplied

Also important to note that a `return` statement without a value, will return `None`


## Keyword Arguments and the print() Function

Most arguments are identified by their position in the function call

* Ex: `random.randint(1, 10)` -- the `1` is the low-end of the range, the `10` is the high-end

    + `random.randint(10, 1)` -- would return an error

**Keyword Arguents** however, are identified by the *keyword* put before them in the function call

* often used for *Optional Parameters*

    - the `print()` function has:

        + the `end` parameter, which specifies what should be printed at the end of the arguments

        + the `sep` parameter, which specifies what should be printed in between the arguments

```
>>> print('Hello', end='')
    print('World')

HelloWorld
```

```
>>> print('cats', 'dogs', 'mice', sep=',')

cats,dogs,mice
```


## The Call Stack

Think of function calls like a meandering conversation...

New topics are added on top of a *stack*, while the original topic gets *pushed* to the bottom

Python will remember which line of code called the function and return to it after encountering a `return` statement

**The Call Stack** is how Python remembers *where* to return to
* This is handled *behind-the-scenes*, meaning there's nothing stored in a variable
* Python creates a *frame object*, and places it on top of the *Stack*
* **Frame Objects** store the line number of the original function call -- a place to return to
* When a function call returns, Python removes the *frame object*, and moves execution to the line stored in it

Note that frame objects are **always** added/removed from the *top* of the stack, nowhere else


## Local and Global Scopes

Parameters/Variables that are assigned inside a function exist *only* in that function's **Local Scope**: -- termed *local variables*

Variables that are assigned outside of *all* functions exist in the **Global Scope** -- termed *global variables*

Think of a **Scope** like a *container* for variables:
* when a scope is destroyed, all the values stored in its variables are forgotten
* there is **only 1** global scope, and it is created when the program begins
* a local scope is created whenever a function is called
    - when the function returns, the local scope is destroyed, and all variables are forgotten
    - the next time you call the function, the variables are reset, as if you never called it
* local variables are also stored in frame objects on the call stack

Why Scopes Matter:
* code in the global scope, **can't** access any local variables
* however, code in a local scope **can** access global variables
* code in a specific function's local scope, **cannot** access variables in any other local scope
* you can use the same name for different variables if they are in different scopes
    - ie: a *local* variable named `spam` and a *global* variable named `spam` is ok

Python has different scopes to limit the amount of code modified by any particular function

This makes debugging easier -- if a bug is caused by a local variable, you can infer the function is written incorectly

Using global variables in a small program is fine, but relying on too many is a bad habit as projects get larger

### Examples
Local Variables **Cannot** be Used in the Global Scope:
```python
def spam()
    eggs = 324423
spam()
print(eggs)
```
this returns an **error**

Local Scopes **Cannot** use Variables in Other Local Scopes:
```python
def spam():
    eggs = 3469
    bacon()
    print(eggs)


def bacon():
    ham = 32131
    eggs = 0


spam()
```
this returns an **error**

Global Variables **can** be Read from a Local Scope:
```python
def spam():
    print(eggs)
eggs = 42
spam()
print(eggs)
```
this is **fine**

Local and Global Variables with the Same Name:
```python
def spam():
    eggs = 'spam local'
    print(eggs) # prints 'spam local'


def bacon():
    eggs = 'bacon local'
    print(eggs) # prints 'bacon local'
    spam()
    print(eggs) # prints 'bacon local'


eggs = 'global'
bacon()
print(eggs) # prints 'global'
```
this is **fine**


## The Global Statement

**Global Statement** -- used to modify a global variable from within a function
```python
def spam():
    global eggs
    eggs = 'spam'

eggs = 'global'
spam()
print(eggs)
```
This final `print()` call will output: `spam` instead of `global`

Rules for Determining Local/Global Scope:
* if a variable is used in the global scope (outside of all functions), then it is **always** a global variable
* if there is a `global` statement for that variable in a function, it is a global variable
* otherwise, if the variable is used in an *assignment statement* in the function, it is a local variable
* but if the variable is not used in an *assignment statement*, it is a global variable

In a function, a variable will either **always** be global, or **always** be local

also note: if you ever want to modify the value stored in a global variable from in a function, 
you **must** use a `global` statement on that variable

Don't forget to assign values to local variables before trying to use them:
```python
def spam():
    print(eggs) # ERROR!
    eggs = 'spam local'

eggs = 'global'
spam()
```
this causes an error because the local variable `eggs` appears in the `spam` function, which makes it
appear local, but because `print(eggs)` is executed before `eggs` is assigned anything, the local 
variable `eggs` doesn't exist yet.

Python will **not** fall back to using the global `eggs` variable in the above example


## Exception Handling

Getting an error, or **exception**, in Python usually means your entire program will crash

This program will attempt to divide by 0 and crash:
```python
def spam(divideBy):
    return 42 / divideBy

print(spam(2))
print(spam(12))
print(spam(0))
print(spam(1))
```

Errors can be handled with `try` and `except` statements:
* code that could potentially have an error is put in a `try` clause
* program execution moves to the start of a following `except` clause if an error happens

The same program using `try` and `except` to handle any errors:
```python
def spam(divideBy):
    try:
        return 42 / divideBy
    except ZeroDivisionError:
        print('Error: Invalid argument.')

print(spam(2))
print(spam(12))
print(spam(0))
print(spam(1))
```
this will handle any `ZeroDivisionErrors`, and continue on to run like normal


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
