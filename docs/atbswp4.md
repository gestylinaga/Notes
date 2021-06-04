# Lists

## The List Data Type

A **List** is a value that contains multiple values in an ordered sequence

A *list value* refers to a list itself, not the values inside the list value:
```python
['cat', 'bat', 'rat', 'elephant']
```
* enclosed in `[`brackets`]`
* values inside the list are called *items*
* items are separated with `,` commas -- aka *comma-delimited*
* lists can be empty `[]`, just like strings can be empty `''`, or `""`

### Getting Individual Values in a List with Indexes

an **Index** refers to the number corresponding to an item in a list:
```python
spam = ['cat', 'bat', 'rat', 'elephant']
```
So:
* `spam[0]` == `'cat'`
* `spam[1]` == `'bat'`
* `spam[2]` == `'rat'`
* `spam[3]` == `'elephant'`

Note: the first value starts at 0, meaning the last index is always 1 less than the size of the list

also Since lists can contain other list values:
```python
bacon = [['cat', 'bat'], [10, 20, 30, 40, 50]]
```
You can acces multiple indexes:
* `bacon[0]` == `['cat', 'bat']`
* `bacon[0][1]` == `'bat'`
* `bacon[1][4]` == `50`

The first index dictates which *list value* to use, and the second index is for the value within the list value

### Negative Indexes

negative integers work for indexes too:
```python
spam = ['cat', 'bat', 'rat', 'elephant']
```
* `spam[-1]` == `'elephant'`
* `spam[-2]` == `'rat'`
* `spam[-3]` == `'bat'`
* `spam[-4]` == `'cat'`

### Getting a List from Another List with Slices

just like an index gets a *single* value from a list, a **slice** gets *several* values from a list, 
in the form of a new list:
* an index: `spam[2]`
* a slice: `spam[1:4]`

The first integer is index where the slice starts, and the second is where the slice ends

**Important to Note: a slice goes up to, but will not include the value at the second index**
```python
spam = ['cat', 'bat', 'rat', 'elephant']
```
* `spam[0:4]` == `['cat', 'bat', 'rat', 'elephant']`
* `spam[1:3]` == `['bat', 'rat']`
* `spam[0:-1]` == `['cat', 'bat', 'rat']`

You can also leave out either side of the colon as a shortcut:
* `spam[:2]` == `['cat', 'bat']` -- same as using `spam[0:2]`
* `spam[1:]` == `['bat', 'rat', 'elephant']` -- same as using `spam[1:3]` (or length of list)
* `spam[:]` == `['cat', 'bat', 'rat', 'elephant']`

### Getting a List's Length with the len() Function

the `len()` function works just like it does with strings:
```python
spam = ['cat', 'dog', 'moose']
len(spam)
```
would return `3`

### Changing Values in a List with Indexes

### List Concatenation and List Replication

### Removing Values from Lists with del Statements


## Working with Lists


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
