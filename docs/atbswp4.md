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

Just like other operators, `in` and `not in` are used in expressions and connect 2 values:
* a value to look for in a list
* the list where it may be found

These expressions will evaluate too a boolean value:
```python
'howdy' in ['hello', 'hi', 'howdy', 'heyas']
```
this will return `True`

```python
spam = ['cat', 'bat', 'rat', 'elephant']

'cat' not in spam
```
this will return `False`

Sample Program: myPets.py
```python
myPets = ['Cody', 'Mookie', 'ChaCha', 'Nollie']
print('Enter a pet name:')
name = input()
if name not in myPets:
    print('I do not have a pet named ' + name)
else:
    print(name + ' is my pet.')
```

### The Multiple Assignment Trick

aka **tuple unpacking**, is a shortcut that lets you assign multiple variables with the values
in a list in one line of code

So instead of doing:
```python
cat = ['fat', 'gray', 'loud']

size = cat[0]
color = cat[1]
disposition = cat[2]
```

You can do:
```python
cat = ['fat', 'gray', 'loud']

size, color, disposition = cat
```
Note that the number of variables and the length of the list **must be exactly equal**, or Python
will return a `ValueError`

### Using the enumerate() Function with Lists

The `enumerate()` function can be used instead of `range(len(someList))` when using a `for` loop
to obtain the integer index of the items on the list

The same program from "Using for Loops with Lists" section using `enumerate()`:
```python
supplies = ['pens', 'staplers', 'flamethrowers', 'binders']
for index, item in enumerate(supplies):
    print('Index ' + str(index) + ' in supplies is: ' + item)
```

Just like as before, this will return:
```
Index 0 in supplies is: pens
Index 1 in supplies is: staplers
Index 2 in supplies is: flamethrowers
Index 3 in supplies is: binders
```

`enumerate()` functions are useful when you need **both** the item and the item's index in
the loop's block

### Using the random.choice() and random.shuffle() Functions with Lists

The `random.choice()` function will return a randomly selected item from the list:
```python
import random
pets = ['Dog', 'Cat', 'Mouse']
random.choice(pets)
```
This will return `'Dog'`, `'Cat'`, or `'Mouse'` picked at random

You can consider `random.choice(someList)` to be a shorter form of `someList[random.randint(0, len(someList) - 1]`

The `random.shuffle()` function reorders the items in a list:
```python
import random
people = ['Alice', 'Bob', 'Carol', 'David']
random.shuffle(people)
```
This function modifies the list *in place*, rather than returning a new list


## Augmented Assignment Operators

Recall that working with variables is usually done like:
```python
spam = 42
spam = spam + 1
spam
```

**Augmented Assignment Operators** are a shortcut to do the same thing:
```python
spam = 42
spam += 1
spam
```

**Equivalent Assignment Statements:**
| Augmented | Assignment | Operators |
| --- | :---: | --- |
| `spam += 1` | == | `spam = spam + 1` |
| `spam -= 1` | == | `spam = spam - 1` |
| `spam *= 1` | == | `spam = spam * 1` |
| `spam /= 1` | == | `spam = spam / 1` |
| `spam %= 1` | == | `spam = spam % 1` |

Note that the `+=` operator can also do string/list concatenation:
```python
spam = 'Hello,'
spam += ' world!'
spam
```
this returns `'Hello, world!'`

Also note that the `*=` operator can do string/list replication:
```python
bacon = ['lol']
bacon *= 3
bacon
```
this returns `['lol', 'lol', 'lol']`


## Methods

a **method** is the same thing as a function, except it is *called on* a value

note that each data type has its own set of methods

### Finding a Value in a List with the index() Method

List value have an `index()` method that can be passed a value, and if that value exists in the
list, the index of the value is returned:
```python
spam = ['hello', 'hi', 'howdy', 'heyas']
spam.index('hello')
```
this returns a `0` because `'hello'` is item 0 in the index 

If the value isn't in the list, then it produces a `ValueError`:
```python
spam.index('hey there')
```
run on the list above, this returns `ValueError` becauase `'hey there'` is not in list `spam`

Note that when there are duplicates of a value in a list, the index of the **first** appearance
is returned

### Adding Values to Lists with the append() and insert() Methods

The `append()` method is used to add new values to a list: (at the end of the list)
```python
spam = ['cat', 'dog', 'bat']
spam.append('moose')
spam
```
this returns a new list: `['cat', 'dog', 'bat', 'moose']`

Similarly, the `insert()` method can insert a value at any index in the list:
```python
spam = ['cat', 'dog', 'bat']
spam.insert(1, 'chicken')
spam
```
* this will return a new list: `['cat', 'chicken', 'dog', 'bat']`
* the first argument, `1`, is the index for the new value
* the second argument, `'chicken'`, is the new value to be inserted

Notice that the code is `spam.append('moose')` and `spam.insert(1, 'chicken')`, and **NOT**
`spam = spam.append('moose')` or `spam = spam.insert(1, 'chicken')`

This is because `append()` and `insert()` return the value `None`, and only modify the list
*in place*

Note that `append()` and `insert()` only work on lists, no other values

### Removing Values from Lists with the remove() Method

The `remove()` method is passed the value to be removed from the list it is called on:
```python
spam = ['cat', 'bat', 'rat', 'elephant']
spam.remove('bat')
spam
```
* this returns: `['cat', 'rat', 'elephant']`
* attempting to delete a value that does not exist results in a `ValueError`
* if a value appears multiple times, only the **first** instance is removed

Note that the `del` statement is good to use when you know the **index** of the value you want to
remove. In contrast, the `remove()` method is useful when you know tha **value** you want to remove

### Sorting the Values in a List with the sort() Method

The `sort()` method can be used to sort lists of number values or lists of strings:
```python
spam = [2, 5, 3.14, 1, -7]
spam.sort()
spam
```
this returns: `[-7, 1, 2, 3.14, 5]`

```python
spam = ['ants', 'cats', 'dogs', 'badgers', 'elephants']
spam.sort()
spam
```
this returns: `['ants', 'badgers', 'cats', 'dogs', 'elephants']`

You can also pass `True` for the `reverse` keyword to sort the values in reverse order:
```python
spam = ['ants', 'cats', 'dogs', 'badgers', 'elephants']
spam.sort(reverse=True)
spam
```
this returns: `['elephants', 'dogs', 'cats', 'badgers', 'ants']`

Things to note about `sort()`:
* sorts lists *in place*, **do not** try to capture the return with `spam = spam.sort()`, it won't work
* you **cannot** sort lists with both number values *and* string values in them
* uses "ASCIIbetical order" rather than actual alphabetical order
    - upper case letters come before lowercase letters
    - for normal alphabetical order: `spam.sort(key=str.lower)`

### Reversing the Values in a List with the reverse() Method


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
