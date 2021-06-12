# Dictionaries and Structuring Data

## The Dictionay Data Type

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

> Ordered Dictionaries in Python 3.7

### The keys(), values(), and items() Methods

### Checking Whether a Key or Value Exists in a Dictionary


---
[back to Automate the Boring Stuff with Python](atbswp.md)

[back to Index/Table of Contents](index.md)
