# Pattern Matching with Regular Expressions

**Regular Expressions** allow you to search for exact *patterns* of text

## Finding Patterns of Text Without Regular Expressions

Think of American phone numbers: three numbers, a hyphen `-`, and four numbers (with an optional 
three numbers in the front for area code): `420-555-6969`

Sample Program *isPhoneNumber.py* to check for valid phone numbers:
```python
# Checks if text is a valid phone number w/out the use of regex
def isPhoneNumber(text):
    if len(text) != 12:                     # checks overall length; must be exactly 12
        return False
    for i in range(0, 3):                   # checks first 3 characters
        if not text[i].isdecimal():         # must be numbers
            return False
        if text[3] != '-':                  # checks 4th character; must be a hyphen '-'
            return False
        for i in range(4, 7):               # checks next 3 characters
            if not text[i].isdecimal():     # must be numbers
                return False
            if text[7] != '-':              # checks 8th characters; must be a hyphen '-'
                return False
            for i in range(8, 12):          # checks next 4 characters
                if not text[i].isdecimal(): # must be numbers
                    return False
            return True                     # all all checks passed, returns True

print('Is 415-555-4242 a phone number?')
print(isPhoneNumber('415-555-4242'))        # returns: True
print('Is Moshi moshi a phone number?')
print(isPhoneNumber('Moshi moshi'))         # returns: False
```
this returns:
```
Is 415-555-4242 a phone number?
True
Is Moshi moshi a phone number?
False
```
Or to search even larger strings, you would have to add more code:
```python
# This block searches the message for a valid phone number

message = 'Call me at 415-555-1011 tomorrow. 415-555-9999 is my office.'

for i in range(len(message)):
    chunk = message[i:i+12]                 # checks every 12 character 'chunk'
    if isPhoneNumber(chunk):                # runs 'chunk' through the function
        print('Phone number found: ' + chunk)
print('Done')
```
this returns:
```
Phone number found: 415-555-1011
Phone number found: 415-555-9999
Done
```


## Finding Patterns of Text With Regular Expressions

**Regular Expressions** or *regex* for short, are descriptions for a pattern of text

For example: `\d` in regex stands for a **digit** character: any single numeral from 0 to 9

So a phone number in regex can be: `\d\d\d-\d\d\d-\d\d\d\d`

Even further is using braces `{}`, to match the number of times: `\d{3}-\d{3}-\d{4}`

### Creating Regex Objects

All of the regex functions in Python are in the `re` module
```python
# VERY IMPORTANT if you want to use regex in Python:
import re
```
Passing a string value representing your regular expression to `re.compile()` returns a **Regex**
pattern object (or simply, a **Regex** object):
```python
phoneNumRegex = re.compile(r'\d{3}-\d{3}-\d{4}') # notice the 'r' for 'raw string'
# now the variable 'phoneNumRegex' contains a Regex object
```

### Matching Regex Objects

```python
phoneNumRegex = re.compile(r'\d{3}-\d{3}-\d{4}')        # notice the 'r' for 'raw string'

mo = phoneNumRegex.search('My number is 415-555-4242.') # mo == Match Object

# .group() used because mo contains 'Match' Object, not 'None'
print('Phone number found: ' + mo.group())

# this returns:
# Phone number found: 415-555-4242
```

### Review of Regular Expression Matching

Steps:
1. Import the regex module with `import re`
2. Create a *Regex* object with the `re.compile()` function (using an `r`string)
3. Pass the string to search into the *Regex* object's `search()` method, which returns a *Match* object
4. Call the *Match* object's `group()` method to return a string of the matched text


## More Pattern Matching With Regular Expressions

### Grouping with Parentheses

Adding parentheses `()` creates *groups* (like for an area code), then you can use the `group()`
match object method to grab the matching text for just one group:
```python
phoneNumRegex = re.compile(r'(\d\d\d)-(\d\d\d-\d\d\d\d)') # remember the 'r' for raw string
mo = phoneNumRegex.search('My number is 415-555-4242.')   # mo == Match Object

mo.group(1)
# returns: '415'

mo.group(2)
# returns: '555-4242'

mo.group(0)
# returns: '415-555-4242'

mo.group()
# returns: '415-555-4242'
```
Using the `groups()` (note the plural form of the name), retrieves all the groups at once:
```python
mo.groups()
# returns: ('415', '555-4242') -- a tuple

# Multiple Assignment Trick:
areaCode, mainNumber = mo.groups()

print(areCode)    # returns: 415
print(mainNumber) # returns: 555-4242
```

### Matching Multiple Groups with the Pipe

The `|` pipe symbol is used to match *one of many* expressions:
```python
heroRegex = re.compile(r'Batman|Tina Fey')
mo1 = heroRegex.search('Batman|Tina Fey')
mo1.group()
# this returns: 'Batman'

mo2 = heroRegex.search('Tina Fey|Batman')
mo2.group()
# this returns: 'Tina Fey'
```
Notice that when *both* `'Batman'` and `'Tina Fey'` appear in the string, the first occurence of
matching text is returned as the *Match* object

The `|` is also used to match one of several patterns as part of your regex:
```python
batRegex = re.compile(r'Bat(man|mobile|copter|bat)')

mo = batRegex.search('Batmobile lost a wheel')

mo.group()
# this returns: 'Batmobile'

mo.group(1)
# this returns: 'mobile'
```
Notice the use of `()` parenthesis after the prefix `'bat'` to specify the patterns to search

Note that to match an actual pipe character, you have to escape it: `\|`

### Optional Matching with the Question Mark

```python
batRegex = re.compile(r'Bat(wo)?man')

mo1 = batRegex.search('The Adventures of Batman')
mo1.group()
# this returns: 'Batman'

mo2 = batRegex.search('The Adventures of Batwoman')
mo2.group()
# this returns: 'Batwoman'
```
Notice the use of the `?` question mark after the `(wo)`, indicating that the `wo` is optional

This is why the regex `'Bat(wo)?man'`, matches both `'Batman'` **and** `'Batwoman'`

Using the earlier phone number example: (with an *optional* area code)
```python
phoneRegex = re.compile(r'(\d\d\d-)?\d\d\d-\d\d\d\d')

mo1 = phoneRegex.search('My number is 415-555-4242')
mo1.group()
# this returns: '415-555-4242'

mo2 = phoneRegex.search('My number is 555-4242')
mo2.group()
# this returns: '555-4242'
```
Notice how again, the regex pattern matches both instances because of the optional supplied

Think of the `?` as saying: "Match zero *or* one of the group preceding this question mark"

Note that to match an actual question mark, you have to escape it: `\?`

### Matching Zero or More with the Star

Think of the `*` star/asterisk as "match zero or more' times:
```python
batRegex = re.compile(r'Bat(wo)*man')

mo1 = batRegex.search('The Adventures of Batman')
mo1.group()
# this returns: 'Batman'

mo2 = batRegex.search('The Adventures of Batwowowowoman')
mo2.group()
# this returns: 'Batwowowowoman'
```
Notice how the regex matches `'Batman'` in the first string (no instances of `wo`), **AND** 
`'Batwowowowoman'` in the second string (4 instances of `wo`)

To match an actual star/asterisk character, you have to escape it: `\*`

### Matching One or More with the Plus

Think of the `+` plus as "match **one** or more":
```python
batRegex = re.compile(r'Bat(wo)+man')

mo1 = batRegex.search('The Adventures of Batwoman')
mo1.group()
# this returns: 'Batwoman'

mo2 = batRegex.search('The Adventures of Batwowowowoman')
mo2.group()
# this returns: 'Batwowowowoman'

mo3 = batRegex.search('The Adventures of Batman')
mo3 == None
# this returns: True
```
Notice how the last string returns `None` because the `wo` in not found **at all**

To match an actual plus character, you have to escape it: `\+`

### Matching Specific Repititions with Braces

Braces `{}` are used to specify a group repeated a specific number of times:
```python
haRegex = re.compile(r'(Ha){3}')

mo1 = haRegex.search('HaHaHa')
mo1.group()
# this returns: 'HaHaHa'

mo2 = haRegex.search('Ha')
mo2 == None
# returns: True
```
Notice how the second string `'Ha'` returns `None` because the specified `(Ha)` only appears **once**

Note that a range can also be passed to the braces : `{3,5}`, `{,6}`, or `{2,}`

## Greedy and Non-Greedy Matching

Python's regular expressions are *greedy* by default, meaning in ambiguous situations with braces, 
they will match the **longest** string possible

The *non-greedy*, aka *lazy*, version of braces has a question mark following the closing brace `}?`:
```python
greedyHaRegex = re.compile(r'(Ha){3,5}')
mo1 = greedyHaRegex.search('HaHaHaHaHa')
mo1.group()
# this returns: 'HaHaHaHaHa'

nongreedyHaRegex = re.compile(r'(Ha){3.5}?')
mo2 = nongreedyHaRegex.search('HaHaHaHaHa')
mo2.group()
# this returns: 'HaHaHa'
```

Note that question marks `?` can have 2 meanings in regular expressions:
1. declaring a *non-greedy* match
2. flagging an *optional group*

These 2 meanings are completely **unrelated** and should **not** be confused


## The findall() Method


## Character Classes

**Shorthand Codes for Common Character Classes**:
| Shorthand Character Classes | Represents |
| :---: | :--- |
| `\d` | Any numeric digit from 0-9 |
| `\D` | Any character that is **not** a digit from 0-9 |
| `\w` | Any letter, numeric digit, or the `_` underscore |
| `\W` | Any character that is **not** a letter, numeric digit, or `_` underscore |
| `\s` | Any space, tab, or newline character |
| `\S` | Any character that is **not** a space, tab, or newline |


## Making Your Own Character Classes


## The Caret and Dollar Sign Characters


## The Wildcard Character


### Matching Everything with Dot-Star

### Matching Newlines with the Dot Character


## Review of Regex Symbols


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
