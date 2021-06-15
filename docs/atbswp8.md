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

### The blank Keyword Argument

### The limit, timeout, and default Keyword Arguments

### The allowRegexes and blockRegexes Keyword Arguments

### Passing a Custom Validation Function to inputCustom()

## Summary


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
