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

* A *function call* -- the name of the function with `()` appended to the end, possibly with some arguments

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

* just like the Boolean data types (`True` and `False`), `None` must be typed with a capital `P`

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


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
