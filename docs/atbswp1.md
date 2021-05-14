# Chapter 1: Python Basics

* REPL -- Read-Evaluate-Print Loop

    - the interactive shell that lets you *execute* Python code


## Expressions:
```
2 + 3
```
- 2 and 3 are considered *values*

- the '+' is the *operator*

- expressions can always *evaluate* down to a single value

    + meaning you can use expressions anywhere you can use values

    + single values with no operators are still considered values, they just evaluate to themselves

    + Order of Operations (PEMDAS), or *precedence* applies here

- Operators in order of precedence
```
** -- Exponent
%  -- Modulus/remainder
// -- Integer division/floored quotient
/  -- Division
*  -- Multiplication
-  -- Subtraction
+  -- Addition
```


## Data Types

* Data Types -- category for values, every value belongs to **exactly** 1 data type

    - **int** -- Integer

        + 53

        + 0

        + -39

    - **floats** -- Floating-Point Number

        + 3.3

        + 0.65

        + -3.693

    - **str** -- Strings -- text values

        + 'Hello'

        + 'fdsjfdskljfas'

        + 'text text text'

        + ' ' -- Can also be *blank* or *empty*


## String Concatenation and Replication

* operators change meaning depending on the data type of a value

* '+' when used on 2 strings joins them as the *string concatenation* operator
```
>>> 'Alice' + 'Bob'
'AliceBob'
```

* String Concatenation only works on 2 strings, mixing data types will result in an error
```
>>> 'Alice' + 39

TypeError: can only concatenate str (not "int") to str
```

* '*' works on strings **and** integers together as a *string replication* operator
```
>>> 'Alice' * 3
'AliceAliceAlice'
```

* '*' won't work on 2 strings or a string/float combo
```
>>> 'Alice' * 'Bob'

TypeError: can't multiply sequence by non-int of type 'str'
```
```
>>> 'Alice' * 5.0

TypeError: can't multiply sequence by non-int of type 'float'
```


## Storing Values in Variables

* Variable -- like a box in the computer's memory for storing a single value

* Assignment Statement -- variable name, *assignment operator*, value to be stored
```
>>> spam = 64
>>> spam
64

>>> eggs = 36
>>> spam + eggs
100
```

* A variable is *initialized* aka created the first time a value is stored in it

* Assigning a new value to a variable is *overwriting* it
```
>>> spam = 'hello'
>>> spam
'hello'

>>> spam = 'later'
>>> spam
'later'
```

* Variable naming rules:

    - can only be 1 word, no spaces

    - only letters, numbers, or an underscore '_'

    - can't begin with a number

    - Case-Sensitive

* Variable Name common conventions:

    - starting variable names with a lowercase letter
        + variable1
        + like_this
        + orLikeThis

    - underscores are preferred to *camelcase*
        + underscores_are_preferred
        + thisIsCamelCase


## Sample Program

```python
# This program says hello and asks for my name

print('Hello, world!')
print('What is your name?')     # asks for their name
myName = input()
print('It is good to meet you, ' + myName)
print('The length of your name is:')
print(len(myName))
print('What is your age?')      # asks for their age
myAge = input()
print('You will be ' + str(int(myAge) + 1) + ' in a year.')
```

* Comments done with hash marks '#'
```python
# this is a comment
```

* **print()** -- the print function

    - prints the string value in the parenthesis

    - called *calling* a print function when python runs it

    - the string value 'Hello, World!' is being *passed* to the function

    - values that are passed to a function are called *arguments*

    - can also be used to enter an empty line
```python
print('Hello, World!')
```

* **input()** -- waits for user to input text and press Enter

    - evalutates to a string, whatever the user typed in

    - assigns input to myName variable in example
```python
myName - input()
```

* **len()** -- returns number of characters in string
```python
print('The length of your name is:')
print(len(myName))
```

* The **str()**, **int()**, and **float()** Functions

    - convert whatever value you pass as a *string*, *integer*, or *float-point* number

```python
myAge = input()
print('You will be ' + str(int(myAge) + 1) + ' in a year.')
```


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
