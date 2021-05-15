# Chapter 2: Flow Control

*Flow Control Statements* decide which lines of code to execute, under which conditions

## Boolean Values

* named after mathematician George Boole

* data type with only 2 possible values: **True** or **False** -- case sensitive

* just like any other value:

    - can be used in expressions

    - can be stored in variables


## Comparison Operators

aka *Relational Operators* -- compare 2 values and evaluates them down to a single Boolean value

```
== -- Equal to
!= -- Not Equal to
<  -- Less than
>  -- Greater than
<= -- Less than or Equal to
>= -- Greater than or Equal to
```

* these evaluate to **True** or **False**

* Equal to and Not Equal to work with values of any data type

* integers and floating-point numbers will always != strings

* important to remember that == and = are different
```
== -- Equal to
=  -- Assigns values to Variables
```


## Boolean Operators

*and*, *or*, and *not* -- used to compare Boolean values

* Binary Boolean Operators

    - *and* and *or* operators always take 2 Boolean values, so they are *Binary Operators*

    - **and** -- evaluates to **True** if *both* given values are True

    - **or** -- evaluates to **True** if *either* given value is True

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

* the **not** operator

    - only works on 1 Boolean value at a time, making it a *unary* operator

    - simply evaluates to opposite Boolean value

    - can be nested, just like double negatives in speech

```
>>> not True
False

>>> not not not not True
True
```

## Mixing Boolean & Comparison Operators

* since comparison operators evalutate to Boolean values, they can be used with Boolean operators
```
>>> (4 < 5) and (5 < 6)
True

>>> (4 < 5) and (9 < 6)
False

>>> (1 == 2) or (2 == 2)
True
```

* can be used multiple times in an expression
```
>>> 2 + 2 == 4 and not 2 + 2 == 5 and 2 * 2 == 2 + 2
True
```

* follow Order of Operations too, in order:

    1. not

    2. and

    3. or


## Elements of Flow Control

* start with a part called the *condition* and always followed by a block of code called the *clause*

* **Conditions** -- same thing as expressions

    - condition is just the specific name in the context of flow control statements

    - always evaluate down to a single Boolean value -- **True** or **False**

* **Blocks of Code** -- lines of code grouped together

    - indicated by indentation of code

    - Rules for Blocks of Code:
    
        + begin when the indentation increases

        + can contain other blocks

        + end when indentation decreases to 0, or to a containg block's indentation


## Program Execution

* or simply *execution* -- term for the current instructions being executed

* no always straight down, flow control statements make execution jump all over the code


## Flow Control Statements

* **if** statements

    - most common type of flow control statement

    - will execute if statement's condition is *True*; skipped if statement's condition is *False*

    - basically: "if this condition is true, execute the code in the clause"

    - consist of:

        + the **if** keyword

        + a condition -- an expression that evaluates to *True* or *False*

        + a colon ":"

        + starting on the next line, an indented block of code -- aka the *if clause*

* **else** statements

    - optionally follow *if* statement
    
    - only executed when the *if* statement's condition is *false*
    
    - basically: "if this condition is true, execute this code. Or else, execute that code"

    - consist of:

        + the **else** keyword

        + a colon ":"

        + starting on the next line, an indented block of code -- aka the *else clause*

* **elif** statements

    - for when you need one of many possible clauses to execute

    - "else if" statements always follow an *if* or another *elif* statement

    - provides another condition to check, only when all previous statements were false

    - consist of:

        + the **elif** keyword

        + a condition -- a *True* or *False*

        + a colon ":"
        
        + starting on the next line, an indented block of code -- aka the *elif clause*

    - in a chain of elif statements, only 1 will be executed, the rest are skipped

* if the condition of every *if* and *elif* statement are false, the the *else* clause is executed

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

* basically: "if the first condition is true, do this. Else, if the second condition is true, do that. Otherwise, do something else"


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
