# 8 kyu Difficulty

## Multiply

This code does not execute properly. Try to figure out why.

My Solution:
```python
def multiply(a, b):
    return a * b # added return statement
```

## Even or Odd

Create a function (or write a script in Shell) that takes an integer as an argument and returns 
"Even" for even numbers or "Odd" for odd numbers.

My Solution:
```python
def even_or_odd(number):
    answer = number % 2 # modulus/remainder operator
    if answer == 0:     # `0` remainder means divisible by 2
        return "Even"   # divisible by 2 means an even number
    else:               # anything other than `0`
        return "Odd"    # any remainder means an odd number
```

Other Possible Solutions:
```python
def even_or_odd(number):
    return 'Odd' if number % 2 else 'Even'
```
```python
def even_or_odd(number):
  if number % 2 == 0:
    return "Even"
  else:
    return "Odd"
```
```python
def even_or_odd(number):
  return ["Even", "Odd"][number % 2]
```


## Opposite Number

Very simple, given a number, find its opposite.

Examples:
```
1: -1
14: -14
-34: 34
```

My Solution:
```python
def opposite(number):
    return number * -1 # multiplying by -1 reverses the sign
```

Other Possible Solutions:
```python
def opposite(number):
    return -number
```
```python
def opposite(number):
    return abs(number) if number < 0 else 0 - number
```


## Reversed Strings

Description:

Complete the solution so that it reverses the string passed into it.

```
'world'  =>  'dlrow'
```

My Solution:
```python
def solution(string):
    # extended slice [start:stop:step]
    return string[::-1]
```

Other Possible Solutions:
```python
def solution(string):
    return ''.join(i for i in reversed(string))
```
```python
def solution(string):
    newstring = ""
    letter = len(string) - 1
    for x in string:
        x = string[letter]
        newstring = newstring + x
        letter = letter -1 
    return newstring
```
```python
def solution(string):
    temp = list(string)
    temp.reverse()
    return ''.join(temp)
```


## Convert boolean values to strings 'Yes' or 'No'.

 Complete the method that takes a boolean value and return a `"Yes"` strings for `true`, or a `"No"`
 string for `false`.

 My Solution:
 ```python
 def bool_to_word(boolean):
    if boolean == True:
        return 'Yes' # yes == True
    else:            # no == False
        return 'No'
 ```

 Other Possible Solutions:
 ```python
 def bool_to_word(bool):
    return "Yes" if bool else "No"
 ```
 ```python
def bool_to_word(bool):
     if bool:
         return "Yes"
     return "No"
 ```
 ```python
def bool_to_word(bool):
    return ['No', 'Yes'][bool]
 ```


## String Repeat

Write a function called `repeatStr` which repeats the given string `string` exactly `n` times.

Example:
```python
repeatStr(6, "I") // "IIIIII"
repeatStr(5, "Hello") // "HelloHelloHelloHelloHello"
```

My Solutions:
```python
def repeat_str(repeat, string):
    return repeat * string
```

Other Possible Solutions:
```python
repeat_str = lambda r, s: s * r
```
```python
def repeat_str(repeat, string):
    solution = ""
    for i in range(repeat):
        solution += string
    return solution
```
```python
def repeat_str(repeat, string):
    return "".join([string]*repeat)
```


## Return Negative

In this simple assignment you are given a number and have to make it negative. But maybe the 
number is already negative?

Example:
```python
make_negative(1);  # return -1
make_negative(-5); # return -5
make_negative(0);  # return 0
```

Notes:
```
* The number can be negative already, in which case no change is required.
* Zero (0) is not checked for any specific sign. Negative zeros make no mathematical sense.
```

My Solution:
```python
def make_negative(int):
    if int >= 0:        # ignores negatives and zeros
        return int * -1 # makes int negative
    else:               # for negative numbers and zeros
        return int      # leaves number as is
```

Other Possible Solutions:
```python
def make_negative( number ):
    return -abs(number)
```
```python
def make_negative( number ):
    return -number if number>0 else number
```
```python
def make_negative(n):
    return n if n <= 0 else -n
```


## Convert a Number to a String!

We need a function that can transform a number into a string. 
What ways of achieving this do you know?

Examples:
```
123 --> "123"
999 --> "999"
```

My Solution:
```python
def number_to_string(num):
    return str(num) # `str()` converts parameter to a string
```

Other Possible Solutions:
```python
def number_to_string(num):
    try:
        return str(num)
    except:
        return None
```
```python
number_to_string = lambda n: str(n)
```
```python
def number_to_string(num):
    return "{}".format(num)
```


## Remove First and Last Character

Description:

It's pretty straightforward. Your goal is to create a function that removes the first and last 
characters of a string. You're given one parameter, the original string. You don't have to worry 
with strings with less than two characters.

My Solution:
```python
def remove_char(s):
    # string slice syntax: [start:stop:step]
    return s[1:len(s) - 1]
    # `len(s) - 1` for last index
```

Other Possible Solutions:
```python
def remove_char(s):
    return s[1:-1] # `-1` is the same as `len(s) - 1`
```


---
[back to Code Wars main page](codeWars.md)

[back to Index/Table of contents](index.md)
