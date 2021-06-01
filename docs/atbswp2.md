# Chapter 2: Flow Control

**Flow Control Statements** decide which lines of code to execute, under which conditions

## Boolean Values

* named after mathematician George Boole

* data type with only 2 possible values: `True` or `False` -- case sensitive

* just like any other value:

    - can be used in expressions

    - can be stored in variables


## Comparison Operators

aka **Relational Operators** -- compare 2 values and evaluates them down to a single Boolean value:

```
== -- Equal to
!= -- Not Equal to
<  -- Less than
>  -- Greater than
<= -- Less than or Equal to
>= -- Greater than or Equal to
```

* these evaluate to `True` or `False`

* Equal to and Not Equal to work with values of any data type

* integers and floating-point numbers will always `!=` strings

* important to remember that `==` and `=` are different:
```
== -- Equal to
=  -- Assigns values to Variables
```


## Boolean Operators

`and`, `or`, and `not` -- used to compare Boolean values

Binary Boolean Operators:

* `and` and `or` operators always take 2 Boolean values, so they are *Binary Operators*

* `and` -- evaluates to `True` if **both** given values are True

* `or` -- evaluates to `True` if **either** given value is True

```
>>> True and True
True

>>> True and False
False
```

```
>>> False or True
True

>>> False or False
False
```

The `not` operator:

* only works on 1 Boolean value at a time, making it a *unary* operator

* simply evaluates to opposite Boolean value

* can be nested, just like double negatives in speech

```
>>> not True
False

>>> not not not not True
True
```

## Mixing Boolean & Comparison Operators

Since comparison operators evalutate to Boolean values, they can be used with Boolean operators:
```
>>> (4 < 5) and (5 < 6)
True

>>> (4 < 5) and (9 < 6)
False

>>> (1 == 2) or (2 == 2)
True
```

can also be used multiple times in an expression:
```
>>> 2 + 2 == 4 and not 2 + 2 == 5 and 2 * 2 == 2 + 2
True
```

Follow Order of Operations too, in order:
1. `not`
2. `and`
3. `or`


## Elements of Flow Control

start with a part called the **Condition** and always followed by a block of code called the **Clause**

**Conditions** -- same thing as expressions

* condition is just the specific name in the context of flow control statements

* always evaluate down to a single Boolean value -- **True** or **False**

**Blocks of Code** -- lines of code grouped together

* indicated by an indentation of code

* Rules for Blocks of Code:
    
    - **begin** when the indentation increases

    - can contain other blocks

    - **end** when indentation decreases to 0, or to a containg block's indentation


## Program Execution

or simply **Execution** -- term for the current instructions being executed

* not always straight down, flow control statements make execution jump all over the code


## Flow Control Statements

`if` statements:

* most common type of flow control statement

* will execute if statement's condition is `True`; skipped if statement's condition is `False`

* basically: "if this condition is true, execute the code in the clause"

* consist of:

    - the `if` keyword

    - a condition -- an expression that evaluates to `True` or `False`

    - a colon `:`

    - starting on the next line, an indented block of code -- aka the *if clause*

```python
if name == 'Alice':
    print('Hi, Alice.')
```

`else` statements:

* optionally follow `if` statement
    
* only executed when the `if` statement's condition is `False`
    
* basically: "if this condition is true, execute this code. Or else, execute that code"

* consist of:

    + the `else` keyword

    + a colon `:`

    + starting on the next line, an indented block of code -- aka the *else clause*

```python
if name == 'Alice':
    print('Hi, Alice.')
else:
    print('Hello, stranger.')
```

`elif` statements:

* for when you need one of many possible clauses to execute

* "else if" statements always follow an `if` or another `elif` statement

* provides another condition to check, only when all previous statements were `False`

* consist of:

    - the `elif` keyword

    - a condition -- a `True` or `False`

    - a colon `:`
    
    - starting on the next line, an indented block of code -- aka the *elif clause*

* in a chain of `elif` statements, only 1 will be executed, the rest are skipped

if the condition of every `if` and `elif` statement are false, the the `else` clause is executed:
```python
name = 'Carol'
age = 3000

if name == 'Alice':
   print('Hi, Alice.')
elif age < 12:
    print('You are not Alice, kiddo.')
else:
    print('You are neither Alice nor a little kid.')

```

basically: "if the first condition is true, do this. Else, if the second condition is true, do that. Otherwise, do something else"

`while` loop statements:

* a `while` clause will execute as long as the statement is `True`

* consist of:

    - the `while` keyword

    - a condition -- a `True` or `False`

    - a colon `:`

    - starting on the next line, an indented block of code -- aka the *while clause*

* similar to an `if` statement but 'loops' back to the `while` statement at the end of the clause

* in while loops, the condition is always checked at the start of each *iteration* -- each time the loop is executed

* the first time that the condition `== False`, the while clause is skipped

```python
spam = 0 
while spam < 5;
    print('Hello, world.')
    spam = spam + 1
```

* Infinite `while` loops:

    - written poorly, *while statements* can get stuck in infinite loops; a common programming bug

    - in the example below, the code will loop back to the beginning if the literal string `your name` is not entered

```python
name = ''
while name != 'your name':
    print('Please type your name.')
    name = input()
print('Thank you!')
```

* `break` statements

    - shortcut to break out of a while loop

    - when the execution hits a `break` statement, it simply exits the `while` loop

    - simply contains the `break` keyword

```python
while True:
    print('Please type your name.')
    name = input()
    if name == 'your name':
        break
print('Thank you!')
```

* `continue` statements
    
    - used inside `while` loops, similar to `break` statements

    - when execution hits a `continue` statement, it jumps back to the start of the loop and reevaluates the condition

```python
while True:
    print('Who are you?')
    name = input()
    if name != 'Joe':
        continue
    print('Hello, Joe. What is the password?')
    password = input()
    if password == 'swordfish':
        break
print('Access Granted.')
```

### for loops and the range() function

Similar to `while` loops, but only execute a *certain* number of times

Consist of:
* the `for` keyword
* a variable name
* the `in` keyword
* a call to the `range()` function, with up to 3 integers passed to it
* a colon `:`
* starting on the next line, an indented block of code -- aka the *for clause*

```python
print('My name is')

for i in range(5):
    print('Jimmy Five Times (' + str(i) + ')')
```

and an equivalent program written as a `while` loop instead:
```python
print('My name is')

i = 0
while i < 5:
    print('Jimmy Five Times (' + str(i) + ')')
    i = i + 1
```

The 'Carl Friedrich Gauss' math problem as a Python program:
```python
total = 0
for num in range(101):
    total = total + 1
print(total)
```

The Starting, Stopping, and Stopping Arguments to `range()`:
* some functions, like `range()`, can be called with multiple arguments
* the 1st argument is the *Start* value -- where the range starts
* the 2nd argument is the *Stop* value -- up to, but not including the number
* the 3rd argument is the *Step* value -- the amount variable is increased with each iteration

```python
for i in range(20, 300, 10):
    print(i)
```

The `range()` function also works with negative numbers to count down:
```python
for i in range(10, -5, -1):
    print(i)
```


## Importing Modules

Python has *built-in* functions like `print()`, `input()`, and `len()`, but more can be *Imported* from the **Standard Library**

Each **Module** from the Standard Library is a Python program itself, containing a group of functions that you can call in your own program

* ie: the `math` module has mathematics related functions
* ie: the `random` module has random-number related functions

An **Import** statements consists of:

* the `import` keyword
* the name of the module
* optionally, more module names, separated by commas

```python
import random

for i in range(5):
    print(random.randint(1, 10))
```

Some example modules:
```python
import random, sys, os, math
```

### from import Statements

An alternative way to call modules with the `for` keyword:
```python
from random import *

for i in range(5):
    print(randint(1, 10))
```

This saves the trouble of having to type `random.randint` each time, but is less readable overall

### Ending a Program Early with the sys.exit() function

```python
import sys

while True:
    print("Type exit to Exit.")
    response = input()
    if response == 'exit':
        sys.exit()
    print('You typed ' + response + '.')
```


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
