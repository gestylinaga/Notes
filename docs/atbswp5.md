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

Dictionaries can be used to visualize something like a chess board:
* 1-8 vertically top to bottom
* a-z horizontally left to right
* w/b Rook, Knight, Bishop, King, Queen, and Pawns
```python
# Starting Chess Positions
chessBoard = {'1a': 'bRook', '2a': 'bKnight', '3a': 'bBishop', '4a': 'bKing', '5a': 'bQueen', '6a': 'bBishop', '7a': 'bKnight', '8a': 'bRook',
    '1b': 'bPawn', '2b': 'bPawn', '3b': 'bPawn', '4b': 'bPawn', '5b': 'bPawn', '6b': 'bPawn', '7b': 'bPawn', '8b': 'bPawn',
    '1c': ' ', '2c': ' ', '3c': ' ', '4c': ' ', '5c': ' ', '6c': ' ', '7c': ' ', '8c': ' ',
    '1d': ' ', '2d': ' ', '3d': ' ', '4d': ' ', '5d': ' ', '6d': ' ', '7d': ' ', '8d': ' ',
    '1e': ' ', '2e': ' ', '3e': ' ', '4e': ' ', '5e': ' ', '6e': ' ', '7e': ' ', '8e': ' ',
    '1f': ' ', '2f': ' ', '3f': ' ', '4f': ' ', '5f': ' ', '6f': ' ', '7f': ' ', '8f': ' ',
    '1g': 'wPawn', '2g': 'wPawn', '3g': 'wPawn', '4g': 'wPawn', '5g': 'wPawn', '6g': 'wPawn', '7g': 'wPawn', '8g': 'wPawn',
    '1h': 'wRook', '2h': 'wKnight', '3h': 'wBishop', '4h': 'wKing', '5h': 'wQueen', '6h': 'wBishop', '7h': 'wKnight', '8h': 'wRook'}
```

### A Tic-Tac-Toe Board

the same can be done with a simpler game tic-tac-toe

Sample Program *ticTacToe.py*:
```python
# a Simplified Tic-Tac-Toe Game Program
# no win-condition, program exits when board is full (9 turns)

# Board as a dictionary: (blank)
theBoard = {'topL': ' ', 'topM': ' ', 'topR': ' ',
        'midL': ' ', 'midM': ' ', 'midR': ' ',
        'botL': ' ', 'botM': ' ', 'botR': ' '}

# Prints a visual 'Game Board' on screen:
def printBoard(board):
    print(board['topL'] + '|' + board['topM'] + '|' + board['topR'])
    print('-+-+-')
    print(board['midL'] + '|' + board['midM'] + '|' + board['midR'])
    print('-+-+-')
    print(board['botL'] + '|' + board['botM'] + '|' + board['botR'])

# User input game:
turn = 'X'                                               # initial turn

for i in range(9):                                       # runs a set number of times (9)
    printBoard(theBoard)                                 # prints current board status
    print('Turn for ' + turn + '. Move on which space?') # User Prompt
    print('Options: top, mid, bot + L,M,R (example: topR, midM, botL)') # Show Options
    move = input()                                       # saves input as `move`
    theBoard[move] = turn                                # overwrites chosen move with 'X' or 'O'
    if turn == 'X':                                      # after 'X' goes,
        turn = 'O'                                       # turn changes to 'O'
    else:                                                # if 'X' did not go,
        turn = 'X'                                       # turn changes to 'X'

printBoard(theBoard)
```

### Nested Dictionaries and Lists

Remember:
* lists contain an ordered series of values
* dictionaries contain are useful for associating keys with values

Sample Program *totalBrought.py*:
```python
# a dictionary that stores picnic guests and items they brought
# displays total number of selected items

# Dictionary holding picnic guests and items they brought:
allGuests = {'Alice': {'apples': 5, 'pretzels': 12},
        'Bob': {'ham sandwhiches': 3, 'apples': 2},
        'Carol': {'cups': 3, 'apple pies': 1}}

# Calculates total number of items brought:
def totalBrought(guests, item):      # inputs name of guest, and name of item brought
    numBrought = 0                   # default number of item brought
    for k, v in guests.items():      # k = guest name; v = picnic item brought
        numBrought += v.get(item, 0) # if item exists (as a key), add to total; else `0`
    return numBrought                # returns final number of items brought

# Proof of Concept Printout:
print('Number of things being brought:')

# Syntax: functionName(dictName, 'stringToSearch')
print('Apples: ' + str(totalBrought(allGuests, 'apples')))
print('Cups: ' + str(totalBrought(allGuests, 'cups')))
print('Cakes: ' + str(totalBrought(allGuests, 'cakes')))
print('Ham Sandwhiches: ' + str(totalBrought(allGuests, 'ham sandwhiches')))
print('Apple Pies: ' + str(totalBrought(allGuests, 'apple pies')))
```
this returns:
```
Number of things being brought:
Apples: 7
Cups: 3
Cakes: 0
Ham Sandwhiches: 3
Apple Pies: 1
```


## Summary

* **Lists** and **Dictionaries** are values that can contain multiple values, including other lists
and dictionaries
* Dictionaries can map an item, or the **Key**, to another, the **Value**
* Dictionaries are accessed using square brackets `[]`, just like lists
* Instead of an integer index, dictionaries have **Keys**, which can be made up of:
    - integers
    - floats
    - strings
    - tuples


## Practice Questions
1. What does the code for an empty dictionary look like?
    - `emptyDict = {}`
2. What does a dictionary value with a key 'foo' and a value 42 look like?
    - `{'foo': 42}`
3. What is the main difference between a dictionary and a list?
    - `lists are ordered (index), dictionaries are not`
    - `dictionaries store key pair values, lists just store values`
4. What happens if you try to access spam['foo'] if spam is {'bar': 100}?
    - `KeyError: 'foo'`
5. If a dictionary is stored in spam, what is the difference between the expressions 'cat' in 
spam and 'cat' in spam.keys()?
    - `"'cat' in spam" means the value 'cat'`
    - `"'cat' in spam.keys()" means the key 'cat'`
6. If a dictionary is stored in spam, what is the difference between the expressions 'cat' in 
spam and 'cat' in spam.values()?
    - `they are equivalent statements`
7. What is a shortcut for the following code?
```python
if 'color' not in spam:
    spam['color'] = 'black'
```
```python
# Answer in One Line:
spam.setdefault('color', 'black')
```
8. What module and function can be used to “pretty print” dictionary values?
    - `pprint.pprint() and pprint.format()`


---
[back to Automate the Boring Stuff with Python](atbswp.md)

[back to Index/Table of Contents](index.md)
