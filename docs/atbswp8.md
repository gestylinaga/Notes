# Input Validation

**Input Validation** code checks that values entered by a user, such as text from the `input()` 
function, are formatted correctly:
```python
while True:            # near-infinite loop
    print('Enter your age:')
    age = input()
    try:
        age = int(age) # checks if input is a number
    except:
        print('Please use numeric digits.')
        continue       # returns to top of loop if invalid
    if age < 1:        # checks if age is a valid number
        print('Please enter a positive number.')
        continue       # returns to top of loop if invalid
    break              # if all checks passed, breaks out of loop

print(f'Your age is {age}.')
```


## The PyInputPlus Module

[Official PyInputPlus Docs](https://pyinputplus.readthedocs.io/)

**Note that the PyInputPlus module is NOT in the standard library, and must be installed with pip**

The PyInputPlus module contains functions similar to `input()` for several kinds of data: numbers, 
dates, email addresses, and more. If users ever enter invalid input, PyInputPlus reprompts them for 
input, just like the code in the previous section:
```python
import pyinputplus
```
* `inputStr()` is like the built-in `input()` function, but has the general PyInputPlus features
* `inputNum()` ensures the user enters a number and returns an int or float
* `inputChoice()` ensures the user enters one of the provided choices
* `inputMenu()` is similar to `inputChoice()`, but provides a menu with numbered or lettered options
* `inputDatetime()` ensures the user enters a date and time
* `inputYesNo()` ensures the user enters a 'yes' or 'no' response
* `inputBool()` is similar to `inputYesNo()`, but takes a 'True' or 'False' response and returns 
a Boolean value
* `inputEmail()` ensures the user enters a valid email address
* `inputFilepath()` ensures the user entes a valid file path and filename, and can optionally check 
that a file with that name exists
* `inputPassword()` is like the built-in `input()`, but displays `*` characters as the user types so 
that passwords, or other sensitive information, aren't displayed on the screen

These functions **automatically** reprompt the user for as long as they enter invalid input:
```
>>> import pyinputplus as pyip
>>> response = pyip.inputNum()

five
'five' is not a number

42
>>> response
42
```
Notice the `as pyip` code in the import statement, this saves us from typing `pyinputplus` each time 
we want to call a PyInputPlus function

Note that unlike `input()`, these functions return an *int* or *float* value, instead of a *string*

Just like `input()`, you can pass a string as an argument to display a prompt:
```
>>> response = input('Enter a number: ')
Enter a number: 42
>>> response
'42'
>>> import pyinputplus as pyip
>>> response = pyip.inputInt(prompt='Enter a number: ')
Enter a number: cat
'cat' is not an integer.
Enter a number: 42
>>> response
42
```

### The min, max, greaterThan, and lessThan Keyword Arguments

The `inputNum()`, `inputInt()`, and `inputFloat()` functions (which accept int and float 
numbers) , also have a `min`, `max`, `greaterThan`, and `lessThan` keyword argument for specifying 
a **range** of valid values:
```python
import pyinputplus as pyip

response = pyip.inputNum('Enter num: ', min=4) # minimum response of 4

response = pyip.inputNum('Enter num: ', greaterThan=4) # must be greater than 4

response = pyip.inputNum('>', min=4, lessThan=6) # must be minimum of 4, less than 6
```
Note that these keywords are *optional*, but if supplied, must be in the range supplied


### The blank Keyword Argument

By default, blank input is **not** allowed unless the `blank` keyword argument is set to `True`:
```python
import pyinputplus as pyip

response = pyip.inputNum('Enter num: ')
# blank values NOT allowed here

response = pyip.inputNum(blank=True)
# blank input IS ALLOWED here
```

### The limit, timeout, and default Keyword Arguments

By default, the PyInputPlus functions will continue unless validated...forever.

To set the function to stop after a set number of times, theres the `limit`, and `timout` 
keyword arguments:
```python
import pyinputplus as pyip

response = pyip.inputNum(limit=2)
# only allows 2 attempts before RetryLimitException error

response = pyip.inputNum(timeout=10)
# 10 second timeout before TimeoutException error
```
To get around this, you can pass a *default* keyword argument, that the function can return 
instead of raising an exception:
```python
response = pyip.inputNum(limit=2, default='N/A')
# this returns 'N/A', if the limit is reached
```

### The allowRegexes and blockRegexes Keyword Arguments

The `allowRegexes` and `blockRegexes` keyword arguments take a list of regular expression 
strings to determine what the PyInputPlus funcion will accept/reject as a valid input:
```python
import pyinputplus as pyip

response = pyip.inputNum(allowRegexes=[r'(I|V|X|L|C|D|M)+', r'zero'])
# only allows roman numerals (in caps) as responses


response = pyip.inputNum(allowRegexes=[r'(i|v|x|l|c|d|m)+', r'zero'])
# only allows roman numerals (in lower case) as responses
```
Note that while these 2 functions only allow roman numerals, it does **NOT** check if they 
are in a valid order

You can also specify a list of regular expression strings that a PyInputPlus function 
will **not** accept, using the `blockRegexes` keyword argument:
```python
import pyinputplus as pyip

response = pyip.inputNum(blockRegexes=[r'[02468]$'])
# will NOT accept any even numbers
```
Note that if you specify both an `allowRegexes` **and** `blockRegexes`, the allow list overrides 
the block list:
```python
import pyinputplus as pyip

response = pyip.inputStr(allowRegexes=[r'caterpillar', 'category'], blockRegexes=[r'cat'])
# this allows 'caterpillar' and 'category', but blocks ANYTHING else with 'cat' in it
```


### Passing a Custom Validation Function to inputCustom()

The `inputCustom()` function allows you to perform your own custom validation logic

Custom Validation Functions can:
* accept a single string argument of what the user entered
* raise an exception if the string fails validation
* return `None` (or has no `return` statement) if `inputCustom()` should return the string
unchanged
* returns a non-`None` value if `inputCustom()` should return a different string from the 
one the user entered
* be passed as the first argument to `inputCustom()`

Sample *addsUpToTen()* function:
```python
import pyinputplus as pyip

def addsUpToTen(numbers):
    numbersList = list(numbers)
    for i, digit in enumerate(numbersList):
        numbersList[i] = int(digit)
    if sum(numbersList) != 10:
        raise Exception('The digits must add up to 10, not %s.' % (sum(numbersList)))
    return int(numbers) # return an int form of numbers

response = pyip.inputCustom(addsUpToTen) # no parentheses after
```
Note that the `inputCustom()` function also supports the general PyInputPlus features:
* `blank`
* `limit`
* `timeout`
* `default`
* `allowRegexes`
* `blockRegexes`


## Summary

* Input validation code is easy to forget, but without it, your program will almost
certainly have buges
* You can use regex to create your own input validation, or use existing modules (like 
`PyInputPlus`)
* You can also `import pyinputplus as pyip` to save yourself time typing
* If none of the pyinputplus module's functions fit your needs, you can create your own 
while still utilizing pyinputplus' other features with `inputCustom()`


## Practice Questions

1. Does PyInputPlus come with the Python Standard Library?
    - `No, must be installed w/ pip`
2. Why is PyInputPlus commonly imported with import pyinputplus as pyip?
    - `To make it easier to type while coding`
3. What is the difference between inputInt() and inputFloat()?
    - `both require numbers, but inputFloat() requires a decimal`
4. How can you ensure that the user enters a whole number between 0 and 99 using 
PyInputPlus?
    - `inputNum(min=0, max=99)`
5. What is passed to the allowRegexes and blockRegexes keyword arguments?
    - `regex that is allowed/blocked in the input`
6. What does inputStr(limit=3) do if blank input is entered three times?
    - `RetryLimitException error`
7. What does inputStr(limit=3, default='hello') do if blank input is entered three times?
    - `returns 'hello' string`


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
