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

Usually, variables are assigned like this: `spam = 42`

However, you can use an index of a list to change the value at that index:
```python
spam = ['cat', 'bat', 'rat', 'elephant']
```
so the command: `spam[2] = 'aardvark'` would overwrite `'rat'` with `'aardvark'`

or the command: `spam[0] = spam[3]` would overwrite `'elephant'` with `'cat'`

### List Concatenation and List Replication

Lists can be concatenated and replicated just like strings
* the `+` operator combines 2 lists to create a new list value
* the `*` operator with a list and an integer replicate the list

so `[1, 2, 3] + ['A', 'B', 'C']` would return `[1, 2, 3, 'A', 'B', 'C']`

and `['X', 'Y', 'Z'] * 3` would return `['X', 'Y', 'Z', 'X', 'Y', 'Z', 'X', 'Y', 'Z']`

### Removing Values from Lists with del Statements

the `del` statement is used to delete values at an index in a list
```python
spam = ['cat', 'bat', 'rat', 'elephant']

del spam[1]
```
this deletes the item `'bat'` and moves everything in list after it up 1 index

so running the command `del spam[1]` again, would delete `'rat'`, because it is **now** at index 1

note that the `del` keyword can be used to delete stand-alone variables too, but in practice this 
is rarely used


## Working with Lists

Lists alleviate the need to store multiple, similar values into multiple, similar variables

so while it might be tempting to write code like this:
```python
catName1 = 'Nollie'
catName2 = 'Killua'
catName3 = 'Tony'
```
it would require *messy* duplicate code like this to work:
```python
print('Enter the name of cat 1:')
canName1 = input()
print('Enter the name of cat 2:')
canName2 = input()
print('Enter the name of cat 3:')
canName3 = input()

print('The cat names are:')
print(catName1 + ' ' + catName2 + ' ' + catName3)
```
this also limits the maximum number of variables you can store

Instead, with lists you can store everything into a single empty list value:
```python
catNames = []                    # empty list to hold cat names

while True:
    # User Prompt; converts the length of the list 'catNames' into a string; exit instructions
    print('Enter the name of cat ' + str(len(catNames) + 1) + ' (Or enter nothing to stop.):')
    name = input()               # stores individual cat names as variable 'name'
    if name == '':               # breaks out of loop of input is left empty
        break
    catNames = catNames + [name] # list concatenation happens here

print('The cat names are:')
for name in catNames:            # for loop to run through each individual list item
    print(' ' + name)            # adds fake 'indent', and prints each item
```
the benefit of lists is that your data is now in a structure, so your program is much more flexible
in processing the data than it would be with several repetitive variables

### Using for Loops with Lists

recall that a `for` loop repeats the code block once for each item in a list value:
```python
for i in range(4):
    print(i)
```
would return:
```
0
1
2
3
```
this is because the return value for `range(4)` is considered by Python to be similar to `[0, 1, 2, 3]`

so an equivalent way to write the previous program is:
```python
for i in [0, 1, 2, 3]:
    print(i)
```

A common Python technique is to use `range(len(someList))` with a `for` loop to iterate over
the indexes of a list:
```python
supplies = ['pens', 'staplers', 'flamethrowers', 'binders']

for i in range(len(supplies)):
    print('Index ' + str(i) + ' in supplies is: ' + supplies[i])
```
would return:
```
Index 0 in supplies is: pens
Index 1 in supplies is: staplers
Index 2 in supplies is: flamethrowers
Index 3 in supplies is: binders
```
Handy because the code in the loop can access:
* the index -- through the variable `i`
* the value at the index -- as `supplies[i]`

Best of all, `range(len(listName))` will iterate through all indexes, no matter how many items it 
contains

### The in and not in Operators

The `in` and `not in` operators are used to determine whether a value is or isn't in a list


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
