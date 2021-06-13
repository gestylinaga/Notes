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


---
[back to Automate the Boring Stuff with Python](atbswp.md)

[back to Index/Table of Contents](index.md)
