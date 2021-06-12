# Dictionaries and Structuring Data

## The Dictionary Data Type

Like lists, **dictionaries** are a mutable collection of many values

However, indexes for dictionaries are called **Keys**, and a key with its associated value is 
called a **Key-Value Pair**

Keys are typed with braces `{}`:
```python
myCat = {'size': 'fat', 'color': 'gray', 'disposition': 'loud'}
```
* this assigns a dictionary to the `myCat` variable
* the dictionary keys are: `size`, `color`, and `disposition`
* the values for these keys are: `fat`, `gray`, and `loud` respectively

To access values:
```python
myCat['size']

'My cat has ' + myCat['color'] + ' fur.'
```
This returns `'fat'` and `'My cat has gray fur.'`

Note that dictionaries can still use integer values for keys, but they don't have to start with 0:
```python
spam = {12345: 'Luggage Combination', 42: 'The Answer'}
```

### Dictionaries vs. Lists

Items in dictionaries are unordered, unlike lists
```python
# Lists:
spam = ['cats', 'dogs', 'moose']
bacon = ['dogs', 'moose', 'cats']
spam != bacon # these 2 lists are NOT EQUAL

# Dictionaries:
eggs = {'name': 'Zophie', 'species': 'cat', 'age': '8'}
ham = {'species': 'cat', 'age': '8', 'name': 'Zophie'}
eggs == ham # these 2 dicionaries ARE EQUAL
```
Note:
* because dictionaries are not ordered, they can't be sliced like lists
* trying to access a key that does not exist results in a `KeyError`, just like a list's `IndexError`

Example Program *birthdays.py*:
```python
# a Program to Remember Birthdays Using Dictionaries

birthdays = {'Alice': 'Apr 1', 'Bob': 'Dec 12', 'Carol': 'Mar 4'}

while True:
    print('Enter a name: (blank to quit)')
    name = input()
    if name == '':
        break

    if name in birthdays:
        print(birthdays[name] + ' is the birthday of ' + name)
    else:
        print('I do not birthday information for ' + name)
        print('What is their birthday?')
        bday = input()
        birthdays[name] = bday
        print('Birthday database updated.')
```

### Ordered Dictionaries in Python 3.7
Even though dictionaries do not have an ordered sequence, in Python 3.7 and above, the order of
their input is still remembered:
```python
eggs = {'name': 'Zophie', 'species': 'cat', 'age': '8'}
list(eggs)
```
this will return: `['name', 'species', 'age']`, while:
```python
ham = {'species': 'cat', 'age': '8', 'name': 'Zophie'}
list(ham)
```
returns: `['species', 'age', 'name']`.

Note that this behavior should **not** be relied upon because dictionaries are still *unordered*:
- You can **not** access items in dictionaries using indexes like `eggs[0]` or `spam[1]`

### The keys(), values(), and items() Methods

The methods `keys()`, `values()`, and `items()` will return *list-like* values of the dictionary's
keys, values, or both keys and values.

The values returned by these methods are not true lists -- they cannot be modified, and do not have 
an `append()` method

They (`dict_keys`, `dic_values`, and `dic_items`) **can** be used in `for` loops:
```python
spam = {'color': 'red', 'age': 42}

for v in spam.values(): # will return: 
    print(v)            # red
                        # 42

for k in spam.keys():   # will return:
    print(k)            # color
                        # age

for i in spam.items():  # will return:
    print(i)            # ('color', 'red')
                        # ('age', 42)
```
Notice that the values in the `dict_items` value returned by the `items()` method are **tuples**
of the key and value

To get a true list from one of these methods, you can pass it's *list-like* return value to the
`list()` function:
```python
spam = {'color': 'red', 'age': 42}
spam.keys()
# returns: dict_keys(['color', 'age'])
list(spam.keys())
# returns: ['color', 'age']
```

Using the multiple assignment trick in a `for` loop to assign the key and value to seperate variables:
```python
spam = {'color': 'red', 'age': 42}

for k, v in spam.items():
    print('Key: ' + k + ' Value: ' + str(v))

# returns:
# Key: age Value 42
# Key: color Value: red
```

### Checking Whether a Key or Value Exists in a Dictionary

The `in` and `not in` operators work just they would with lists:
```python
spam = {'name': 'Zophie', 'age': 7}

'name' in spam.keys()
# returns True

'Zophie' in spam.values()
# returns True

'color' in spam.keys()
# returns False

'color' not in spam.keys()
# returns True

'color' in spam # same as `'color' in spam.keys()`
# returns False
```

### The get() Method

The `get()` method takes 2 arguments:
* the key of the value to retrieve and
* a fallback value to return if that key does not exist
```python
picnicItems = {'apples': 5, 'cups': 2}
'I am bringing ' + str(picnicItems.get('cups', 0)) + ' cups.'
# returns: 'I am bringing 2 cups.'

'I am bringing ' + str(picnicItems.get('eggs', 0)) + ' eggs.'
# returns: 'I am bringing 0 eggs.'
```
this works because the key `eggs` does not exist in the dictionary, so the default value `0` is 
returned by the `get()` method. Without one, it would result in an error.

### The setdefault() Method

To add a value to a dictionary for a certain key that does not exist yet:
```python
spam = {'name': 'Mookie', 'age': 5}
if 'color' not in spam:
    spam['color'] = 'spots'
```

Or use the `setdefault()` method to do it in one line of code:
```python
spam = {'name': 'Mookie', 'age': 5}
spam.setdefault('color', 'spots')
spam # returns: {'color': 'spots', 'age': 5, 'name': 'Mookie'}

# running again, with different value
spam.setdefault('color', 'brown')
spam # returns: {'color': 'spots', 'age': 5, 'name': 'Mookie'} again. No change.
```
Notice how running the line of code a second time with a different value does **not** change the 
value because the key `'color'` already exists

Sample Program *characterCount.py*:
```python
message = 'It was a bright cold day in April, and the clocks were striking thirteen.'
count = {}

for character in message:
    count.setdefault(character, 0)
    count[character] = count[character] + 1

print(count)
```
this returns:
```
{' ': 13, ',': 1, '.': 1, 'A': 1, 'I': 1, 'a': 4, 'c': 3, 'b': 1, 'e': 5, 'd': 3, 'g': 2,
'i': 6, 'h': 3, 'k': 2, 'l': 3, 'o': 2, 'n': 4, 'p': 1, 's': 3, 'r': 5, 't': 6, 'w': 2, 'y': 1}
```
the `setdefault()` method call ensures that the key is in the `'count'` dictionary (with default 
value of `0`) so that the program doesn't result in a `KeyError` when `count[character] += 1`
is executed


## Pretty Printing

The `pprint` module gives access to the `pprint()` and `pformat()` methods that will *pretty print*
a dictionary's values:
```python
import pprint

message = 'It was a bright cold day in April, and the clocks were striking thirteen.'
count = {}

for character in message:
    count.setdefault(character, 0)
    count[character] += 1

pprint.pprint(count)
```
this returns:
```
{' ': 13,
 ',': 1,
 '.': 1,
 'A': 1,
 'I': 1,
 --snip-- # cut for brevity
 't': 6,
 'w': 2,
 'y': 1}
```
`pprint.pprint()` is especially helpful when the dictionary itself contains nested lists/dictionaries

The `pprint.pformat()` method is used to format the value as a string instead of printing it on
the screen:
```python
# These 2 lines are the same:
pprint.pprint(someDictionaryValue)
print(pprint.pformat(someDictionaryValue))
```


## Using Data Structures to Model Real-World Things

### A Tic-Tac-Toe Board


---
[back to Automate the Boring Stuff with Python](atbswp.md)

[back to Index/Table of Contents](index.md)
