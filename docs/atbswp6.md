# Manipulating Strings

## Working With Strings

String Literals:
Typing: 
```python
'That is Alice's cat.'
```
won't work because Python will read this as `'That is Alice'` 
and `s cat.`, seperately.

## Double Quotes

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

## Indexing and Slicing Strings


---
[back to Automate the Boring Stuff with Python](atbswp.md)

[back to Index/Table of Contents](index.md)
