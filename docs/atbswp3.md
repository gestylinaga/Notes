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

* A *function call* -- the name of the function with `()`, possibly with some arguements

Remember: functions are run when they are called, not when they are defined


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


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
