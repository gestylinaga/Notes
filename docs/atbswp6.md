# Manipulating Strings

## Working With Strings

String Literals:
Typing: 
```python
'That is Alice's cat.'
```
won't work because Python will read this as `'That is Alice'` 
and `s cat.`, seperately.

### Double Quotes

Using double quotes `""` is equivalent to using single quotes `''`, except you can use single
quotes inside them:
```python
spam = "That is Alice's cat."
```


## Escape Characters

An escape character `\` lets you use characters that are otherwise impossible to put into a string:
```python
spam = 'Say hi to Bob\'s mother'
```
Some Escape Characters:
| Escape Character | Prints as |
| --- | --- |
| `\'` | Single quote |
| `\"` | Double quote |
| `\t` | Tab |
| `\n` | Newline (line break) |
| `\\` | Backslash |

Example:
```python
print("Hello there!\nHow are you?\nI\'m doing fine.")
```
will return:
```
Hello there!
How are you?
I'm doing fine.
```

## Raw Strings

Placing an `r` before the opening quote `"` makes it a **Raw** string:
```python
print(r'That is Carol\'s cat.')
```
this returns: `That is Carol\'s cat.`

This is useful for typing strings with **many** backslashes, like Windows file paths:
```python
r'C:\Users\Al\Desktop'
```

## Multiline Strings with Triple Quotes

Multiline strings can be created with 3 single quotes `'''` or double quotes `"""`:
```python
print('''Dear Alice,

Eve's cat has been arrested for catnipping, cat burglary, and extortion.

Sincerely,
Bob''')
```
will return:
```
Dear Alice,

Eve's cat has been arrested for catnapping, cat burglary, and extortion.

Sincerely,
Bob
```
Notice how the single quote in `Eve's` does **not** need to be escaped


## Multiline Comments

While hash marks `#` are used for single line comments, multiline comments are made with 3 double
quotes:
```python
"""This is a test Python program
Look at this text

lalalalla
"""

def spam():
    """This multiline comment describes
    what this function is doing"""
    print('Hello!')
```

### Indexing and Slicing Strings

Strings use **indexes** and **slicing** the same way lists do:
```python
spam = 'Hello, world!'
```
So:
* `spam[0]` would return `'H'`
* `spam[4]` would return `'o'`
* `spam[-1]` would return `'!'`
* `spam[0:5]` would return `'Hello'`
* `spam[:5]` would return `'Hello'`
* `spam[7:]` would return `'world!'`

Note that slicing a string does **not** modify the original string:
```python
spam = 'Hello, world!' # original string
fizz = spam[0:5]       # applies slice to new variable

fizz                   # returns 'Hello'
spam                   # returns 'Hello, world!'
```

### The in and not in Operators with Strings

The `in` and `not in` operators work just like they do with lists:
```python
'Hello' in 'Hello, World'
# returns: True

'Hello' in 'Hello'
# returns: True

'HELLO' in 'Hello, World'
# returns: False

'' in 'spam'
# returns: True

'cats' no in 'cats and dogs'
# returns: False
```
Note that these expressions test if the **exact** string, case-sensitive, is found within the 
second string


## Putting Strings Inside Other Strings

The basic `+` operator and string concatenation:
```python
name = 'Al'
age = 4000
'Hello, my name is ' + name + '. I am ' + str(age)  + ' years old.'
```

Using **string interpolation**, with the `%` operator:
```python
name = 'Al'
age = 4000
'My name is %s. I am %s years old.' % (name, age)
```

From Python 3.6 forward, using **f-strings**, with an `f` and braces `{}`:
```python
name = 'Al'
age = 4000
f'My name is {name}. I am {age} years old.'
f'Next year I will be {age + 1}.'
```


## Useful String Methods

### The upper(), lower(), isupper(), and islower() Methods

The `upper()` and `lower()` string methods return a new string where all the letters in the string
are converted to upper/lower case:
```python
spam = 'Hello, world!'

spam = spam.upper()
spam
# returns: 'HELLO, WORLD!'

spam = spam.lower()
spam
# returns: 'hello, world!'
```
Note that these methods do **not** change the string itself, they return a new string

To change the original string, you have to call `upper()`/`lower()` on the string, and then assign
the new string to the variable where the original was stored

Think of `spam = spam.lower()` like `eggs = eggs + 3`; `eggs + 3` alone would **not** work, just
like `spam.lower()` by itself would **not** work

Useful in making case-insensitive comparisons:
```python
print('How are you?')
feeling = input()

if feeling.lower() == 'great':
    print('I feel great too.')
else:
    print('I hope the rest of your day is good.')
```
because the spelling case of the input is not important (can be `'Great'`, `'GrEaT'`, or even 
`'GREAT'`), using `feeling.lower()` checks if any version of `'great'` is entered

The `isupper()` and `islower()` methods return a Boolean value `True` if it has at least **one** 
letter, and **all** the letters are uppercase/lowercase:
```python
spam = 'Hello, world!'

spam.islower()
# returns False

spam.isupper()
# returns False

'HELLO'.isupper()
# returns True

'abc12345'.islower()
# returns True

'12345'.islower()
#returns False

'12345'.islower()
# returns True
```

Since the `upper()` and `lower()` string methods return strings themselves, you can call them on
themselves:
```python
'Hello'.upper()
# returns 'HELLO'

'Hello'.upper().lower()
# returns 'hello'

'Hello'.upper().lower().upper()
# returns 'HELLO'

'HELLO'.lower()
# returns 'hello'

'HELLO'.lower().islower()
# returns True
```

### The isX() Methods

Some Common *isX* String methods:
* `isalpha()` -- True if strings consists of only **letters**, and is not blank
* `isalnum()` -- True if string consists of only **letters and numbers**, and isn't blank
* `isdecimal()` -- True if string consists of only **numeric characters**, and isn't blank
* `isspace()` -- True if string consists of only **spaces, tabs, and newlines**, and isn't blank
* `istitle()` -- True if string consists of only **words that begin with an uppercase letter, 
followed by only lowercase letters**

```python
'hello'.isaplhpa()
# returns True

'hello123'.isalpha()
# returns False

'hello123'.isalnum()
# returns True

'hello'.isalnum()
# returns True

'123'.isdecimal()
# returns True

'    '.isspace()
# returns True

'This Is Title Case'.istitle()
# returns True

'This Is Title Case 123'.istitle()
# returns True

'This Is not Title Case'.istitle()
# returns False

'This Is NOT Title Case Either'.istitle()
# returns False
```
this is useful in validating user input

Sample Program *validateInput.py*:
```python
# a Program to Validate User Input

# First Validation Loop:
while True:
    print('Enter your age:')
    age = input()

    # Checks if Input is a Number
    if age.isdecimal():
        break # Only way to break out of loop

    # Implied else: (restarts loop)
    print('Please enter a number for your age.')


# Second Validation Loop:
while True:
    print('Select a new password (letters and numbers only):')
    password = input()

    # Checks if input is a letters or numbers ONLY
    if password.isalnum():
        break # Only way to break out of loop

    # Implied else: (restarts loop)
    print('Passwords can only have letters and numbers.')
```

### The startswith() and endswith() Methods

The `startswith()` and `endswith()` methods return `True` if the string value they are called on
begins/ends with the string passed to the method:
```python
'Hello, world!'.startswith('Hello')
# returns True

'Hello, world!'.endswith('world!')
# returns True

'abc123'.startswith('abcdef')
# returns False

'Hello, world!'.startswith('Hello, World!')
# returns True

'Hello, world!'.endswith('Hello, World!')
# returns True
```
these are useful alternatives to the `==` equals operator if you need to check only whether the 
first or last part of a string, instead of the whole thing, is equal to another string

### The join() and split() Methods

The `joint()` method is used to join a list of strings that need to be joined together into a single
string value:
```python
','.join(['cats', 'rats', 'bats'])
# returns: 'cats, rats, bats'

' '.join(['My', 'name', 'is', 'Simon'])
# returns: 'My name is Simon'

'ABC'.join(['My', 'name', 'is', 'Simon'])
# returns: 'MyABCnameABCisABCSimon'
```
Notice that the `join()` method is called on a **string value**, and passed a **list value**

The opposite is the `split()` method: (called on a **list**, passed a **string**)
```python
'My name is Simon'.split()
# returns: ['My', 'name', 'is', 'Simon']
```
Notice that by default (no string passed), the string is split wherever *whitespace* characters are
found (spaces, tabs, or newline characters):
```python
'MyABCnameABCisABCSimon'.split('ABC')
# returns: ['My', 'name', 'is', 'Simon']

'My name is Simon'.split('m')
# returns: ['My na', 'e is Si', 'on']
```
A common use is to pass `split()` the `'\n'` argument:
```python
spam = '''Dear Alice,
How have you been? I am fine.
There is a container in the fridge
that is labeled "Milk Experiment."

Please do not drink it.
Sincerely,
Bob'''

spam.split('\n')
```
this returns: `['Dear Alice,', 'How have you been? I am fine.', 'There is a container in the fridge',
'that is labeled "Milk Experiment,"', '', 'Please do not drink it.', 'Sincerely,', 'Bob']`

### Splitting Strings with the partition() Method

The `partition()` string method is used to split a string into the text before and after a separator
string:
```python
'Hello, world!'.partition('w')
# returns: ('Hello, ', 'w', 'olrd!')

'Hello, world!'.partition('world')
# returns: ('Hello, ', 'world', '!')
```
Notice how:
* the return result is a **tuple** value
* returns 3 substrings: 'before', 'separator', and 'after'

If a *separator* string occurs multiple times, the method only splits the string on the first
occurence:
```python
'Hello, world!'.partition('o')
# returns: ('Hell', 'o', ', world!')
```
If a *separator* string is **not** found, the entire string, and the other 2 substrings empty:
```python
'Hello, world!'.partition('XYZ')
# returns: ('Hello, world!', '', '')
```
The `partition()` method is useful for splitting a string whenever you need the parts before, 
including, and after a particular separator string

### Justifying Text with the rjust(), ljust(), and center() Methods

the `rjust()` and `ljust()` string methods return a *padded* version of the string they are called
on, with spaces inserted to justify the text:
```python
'Hello'.rjust(10)
# returns: '     Hello'

'Hello'.rjust(20)
# returns: '               Hello'

'Hello, World'.rjust(20)
# returns: '               Hello, World'

'Hello'.ljust(10)
# returns: 'Hello     '
```
Notice how:
* the first argument to both methods is an integer length for the *justified* string
* optionally, a second argument will specify a fill character instead of a space

```python
'Hello'.rjust(20, '*')
# returns: '***************Hello'

'Hello'.ljust(20, '-')
# returns: 'Hello---------------'
```
The `center()` string method works just like `ljust()` and `rjust()`, but centers the text rather
than justifyi it to the left/right:
```python
'Hello'.center(20)
# returns: '       Hello        '

'Hello'.center(20,'&')
# returns: '&&&&&&&Hello&&&&&&&&'
```

Sample Program *picnicTable.py*:
```python
# Displays dictionary values, neatly aligned using the .center(), ljust(), and rjust() methods

# The Sample Dictionary:
picnicItems = {'sandwhiches': 4, 'apples': 12, 'cups': 4, 'cookies': 8000}

def printPicnic(itemsDict, leftWidth, rightWidth):
    print('PICNIC ITEMS'.center(leftWidth + rightWidth, '-'))     # title line; justified with '-'
    for k, v in itemsDict.items():                                # (k)ey, and (v)alue in dictionary
        print(k.ljust(leftWidth, '.') + str(v).rjust(rightWidth)) # '.' for keys, and ' ' for values

printPicnic(picnicItems, 12, 5) # 12 for leftWidth, 5 for rightWidth
printPicnic(picnicItems, 20, 6) # 20 for leftWidth, 6 for rightWidth
```
this returns:
```
---PICNIC ITEMS--
sandwhiches.    4
apples......   12
cups........    4
cookies..... 8000
-------PICNIC ITEMS-------
sandwhiches.........     4
apples..............    12
cups................     4
cookies.............  8000
```

### Removing Whitespace with the strip(), rstrip(), and lstrip() Methods

The `strip()` string method returns a new string without any whitespace characters at the **beginning**
or **end**

The `lstrip()` and `rstrip()` methods will remove whitespace characters from the left/right ends

```python
spam = '    Hello, World    '

spam.strip()
# returns: 'Hello, World'

spam.lstrip()
# returns: 'Hello, World    '

spam.rstrip()
# returns: '    Hello, World'
```
Optionally, a string argument will specify which characters on the ends should be stripped:
```python
spam = 'SpamSpamBaconSpamEggsSpamSpam'
spam.strip('ampS')
# returns: 'BaconSpamEggs'
```
Notice how the order of the string passed,`'ampS'`, does **not** matter, only the correct case
* The same result can be obtained with `'mapS'`, `'Spam'`, or `'mpSa'`


## Numeric Values of Characters with the ord() and chr() Functions

Computers store information as bytes (strings of binary numbers), which means we need to be able to 
convert text to numbers. Because of this, every text character has a corresponding numberic value
called a **Unicode Code Point**.

The `ord()` function is used to get the code point of a one-character string, and the `chr()` 
function is used to get the one-character string of an integer code point:
```python
ord('A')
# returns: 65

ord('4')
# returns: 52

ord('!')
# returns: 33

chr(65)
# returns: 'A'
```
these can be useful when you need to do an ordering or mathematical operation on characters:
```python
ord('B')
# returns: 66

ord('A') < ord('B')
# returns: True

chr(ord('A'))
# returns: 'A'

chr(ord('A') + 1)
# returns: 'B'
```

For more Unicode and code point info, see Ned Batchelder's 2012 PyCon talk:
["Pragmatic Unicode, or, How Do I Stop the Pain?" YouTube Link](https://youtu.be/sgHbC6udIqc)



## Copying and Pasting Strings with the PyperClip Module

The `pyperclip` module has `copy()` and `paste()` functions that can send text to and receive text
from your computer's clipboard

**Note that pyperclip is NOT in Python's standard library, and must be installed differently**
```python
import pyperclip
pyperclip.copy('Hello, world!')
pyperclip.paste()
# returns: 'Hello, world!'
```


## Summary


## Practice Questions
1. What are escape characters?

2. What do the \n and \t escape characters represent?

3. How can you put a \ backslash character in a string?

4. The string value "Howl's Moving Castle" is a valid string. Why isn’t it a problem that the 
single quote character in the word Howl's isn’t escaped?

5. If you don’t want to put \n in your string, how can you write a string with newlines in it?

6. What do the following expressions evaluate to?
```
'Hello, world!'[1]
'Hello, world!'[0:5]
'Hello, world!'[:5]
'Hello, world!'[3:]
```
7. What do the following expressions evaluate to?
```
'Hello'.upper()
'Hello'.upper().isupper()
'Hello'.upper().lower()
```
8. What do the following expressions evaluate to?
```
'Remember, remember, the fifth of November.'.split()
'-'.join('There can be only one.'.split())
```
9. What string methods can you use to right-justify, left-justify, and center a string?

10. How can you trim whitespace characters from the beginning or end of a string?

---
[back to Automate the Boring Stuff with Python](atbswp.md)

[back to Index/Table of Contents](index.md)
