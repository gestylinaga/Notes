# Lists (cont.)

[see Chapter 4: Lists - part 1](atbswp4.md)

## Sequence Data Types

Lists aren't the only data type that represent an ordered **sequence of values**.
Strings can be considered a "list" too, in that it's a *list* of single characters.

Python Sequence Data Types include:
* lists
* strings
* range objects returned by `range()`
* tuples

This means that things you can do to lists can be done to other values of sequence types:
* indexing
* slicing
* with `for` loops
* with `len()` 
* with `in` and `not in`

```python
name = 'Zophie'
```
* `name[0]` returns `'Z'`
* `name[0:4]` returns `'Zoph'`
* `'Zo' in name` returns `True`
* `'z' in name` returns `False`

and:
```python
for i in name:
    print('***' + i + '***')
```
will return:
```
* * * Z * * *
* * * o * * *
* * * p * * *
* * * h * * *
* * * i * * *
* * * e * * *
```

### Mutable and Immutable Data Types

**Mutable** data types:
* ie. lists
* can have values added/removed/changed

**Immutable** data types:
* ie. strings
* **cannot** be changed

The proper way to *"mutate"* a string is to use *slicing* and *concatenation* and to
build a new string:
```python
name = 'Zophie a cat'
newName = name[0:7] + 'the' + name[8:12]

name
newName
```
here `name` returns `'Zophie a cat'`, and `newName` returns `'Zophie the cat'`

Note that the original string `'Zophie a cat'` is **not** modified, instead a brand new string
is created. This is because strings are *immutable*.

On the other hand, **lists** are *mutable*:
```python
eggs = [1, 2, 3]
eggs = [4, 5, 6]
eggs
``` 
in this example, the list value `eggs` isn't being changed; rather, an entirely **new** and 
different list value `[4, 5, 6]` is overwriting the old list value `[1, 2, 3]`

Therefore, changing a value of a *mutable* data type, like with `del` and `append()`, 
changes the value *in place*, since the variable's value is not replaced

### The Tuple Data Type

The **tuple** data type is *almost* identical to the list data type except:
* typed with `(`parenthesis`)` insead of `[]` square brackets
* are immutable, like strings

```python
eggs = ('hello', 42, 0.5)
```
so:
* `eggs[0]` returns `'hello'`
* `eggs[1:3]` returns `(42, 0.5)`
* `len(eggs)` returns `3`
* but `eggs[1] = 99` returns `TypeError` because tuples **cannot** be modified

Note that leaving a *trailing comma* after a value inside parenthesis lets Python know it's a 
tuple value, not a string inside parenthesis:
* `type(('hello',))` returns `<class 'tuple'>`
* `type(('hello'))` returns `<class 'str'>`

Tuples are useful for an ordered sequence of values that never intend to change. Another benefit is,
because tuples are immutable, Python can implement optimizations to make using tuples faster than
using lists.

### Converting Types with the list() and tuple() Functions

The `list()` and `tuple()` functions can be used just like the `str()` and `int()` functions,
meaning they return a list/tuple version of the values passed to them:
```python
tuple(['cat', 'dog', 5])
list(('spoon', 'fork', 42))
list('hello')
```
This returns: (in order)
```
('cat', 'dog', 5)
['spoon', 'fork', 42]
['h', 'e', 'l', 'l', 'o']
```
Converting a tuple to a list is handy if you need a mutable version of a tuple value


## References

Technically, variable are storing *references* to the computer memory locations where the values
are stored. So:
```python
spam = 42
cheese = spam
spam = 100
```
the variable `spam` will now return `100`, but the `cheese` variable will still return `42`

This happens because when you assign `42` to the variable `spam`, you are actually creating the
`42` value in the computer's memory, and storing a **reference** to it in the `spam` variable

When you copy the value in `spam` and assign it to the variable `cheese`, you are actually copying
the **reference**

When you change the value in `spam` to `100`, you're creating a **new** `100` value, and storing a 
reference to it in `spam`. Note that this does not affect the value in `cheese`.

**Integers are immutable**, so changing the `spam` variable is actually making it refer to a 
completely different value in memory

### Identity and the id() Function

The `id()` function returns the numeric memory address where the value is stored:
```python
id('Howdy') # the returned number will be different on every machine
```
this returns a string of numbers like : `2506612030640`

Note that this also changes each time you run the code

On immutable values, like strings, a new object is made in a different place in memory:
```python
bacon = 'Hello'
id(bacon)

bacon += ' world!' # a new string is made
id(bacon)
```
the first `id(bacon)` will return a completely **different** id to the second `id(bacon)`

On mutable values, like lists, objects are modified *in place*:
```python
eggs = ['cat', 'dog']          # creates a new list
id(eggs)                       # reference to location in memory

eggs.append('moose')           # .append() modifies list "in place"
id(eggs)                       # same as first id

eggs = ['moose', ':)', 'orcs'] # creates a new list, new identity
id(eggs)                       # completey different from first 2 ids
```
Methods like: `append()`, `extend()`, `remove()`, `sort()`, `reverse()`, etc... modify their
lists in place, keeping the same id

> Python has an **Automatic Garbage Collector**, that deletes any values not being referred to
> by any variables to free up memory

### Passing References

```python
def eggs(someParameter):
    someParameter.append('Hello')

spam = [1, 2, 3]
eggs(spam)
print(spam)
```
this returns `[1, 2, 3, 'Hello']`

Notice that when `eggs()` is called, a return value is not used to assign a new value to `spam`.
Even though `spam` and `someParameter` contain seperate references, they both refer to the same list.

This is why the `append('Hello')` method call inside the function affects the list even after
the function is called

### The copy Module's copy() and deepcopy() Functions

The `copy` module provides the `copy()` and `deepcopy()` functions to...**copy** lists and dictionaries

Using `copy.copy()`, makes a duplicate copy of a mutable value:
```python
import copy

spam = ['A', 'B', 'C', 'D']

cheese = copy.copy(spam) # copies list to a new list
id(cheese)               # different list/different identity

cheese[1] = 42           # only affects cheese list
spam                     # returns: ['A', 'B', 'C', 'D']
cheese                   # returns: ['A', 42, 'C', 'D']
```

Similarly, the function `copy.deepcopy()`, will copy lists containg lists. It will copy the inner 
or nested lists as well.


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
