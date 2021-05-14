# Capter 2: Flow Control

*Flow Control Statements* decide which lines of code to execute, under which conditions

## Boolean Values

* name after mathematician George Boole

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

* these evaluate to True or False

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

* **not** operator

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


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
