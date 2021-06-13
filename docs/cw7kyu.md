# 7 kyu Difficulty

## 1. Vowel Count

Description:

Return the number (count) of vowels in the given string.

We will consider `a, e, i, o, u` as vowels for this Kata (but not `y`).

The input string will only consist of lower case letters and/or spaces.

My Solution:
```python
def get_count(input_str):
    num_vowels = 0                                                      # initial count
    for i in input_str:                                                 # for each character in input_str
        if (i == 'a' or i == 'e' or i == 'i' or i == 'o' or i == 'u'):  # vowels
            num_vowels += 1                                             # add 1 to count
    return num_vowels                                                   # return final count
```

Other Possible Solutions:
```python
def getCount(inputStr):
    return sum(1 for let in inputStr if let in "aeiouAEIOU")
```
```python
def getCount(inputStr):
    num_vowels = 0
    for char in inputStr:
        if char in "aeiouAEIOU":
           num_vowels = num_vowels + 1
    return num_vowels
```
```python
def getCount(inputStr):
    return sum(inputStr.count(char) for char in ['a', 'e', 'i', 'o', 'u'])
```


## 2. Disemvowel Trolls

Description:

Trolls are attacking your comment section!

A common way to deal with this situation is to remove all of the vowels from the trolls' comments, 
neutralizing the threat.

Your task is to write a function that takes a string and return a new string with all vowels 
removed.

For example, the string "This website is for losers LOL!" would become "Ths wbst s fr lsrs LL!".

Note: for this kata y isn't considered a vowel.

My Solution:
```python
def disemvowel(string_):
    for i in string_:                        # checks each character in string
        if i in "aeiouAEIOU":                # if a vowel
            string_ = string_.replace(i, '') # replaces value with a blank string ''
    return string_                           # returns final string
```

Other Possible Solutions:
```python
def disemvowel(string):
    return string.translate(None, 'aeiouAEIOU')
```
```python
def disemvowel(s):
    for i in "aeiouAEIOU":
        s = s.replace(i,'')
    return s
```
```python
import re

def disemvowel(string):
    return re.sub(r"[aeiouAEIOU]", "", string)
```


## 3. Get the Middle Character

Description:

You are going to be given a word. Your job is to return the middle character of the word. If the 
word's length is odd, return the middle character. If the word's length is even, return the middle 
2 characters.

Examples:
```
Kata.getMiddle("test") should return "es"

Kata.getMiddle("testing") should return "t"

Kata.getMiddle("middle") should return "dd"

Kata.getMiddle("A") should return "A"
```

> Input
>> A word (string) of length 0 < str < 1000 (In javascript you may get slightly more than 1000 in 
>> some test cases due to an error in the test cases). You do not need to test for this. This is only 
>> here to tell you that you do not need to worry about your solution timing out.
>
> Output
>> The middle character(s) of the word represented as a string.

My Solution:
```python
```


## 4. Exes and Ohs

Description:

Check to see if a string has the same amount of 'x's and 'o's. The method must return a boolean 
and be case insensitive. The string can contain any char.

Examples:
```
XO("ooxx") => true
XO("xooxx") => false
XO("ooxXm") => true
XO("zpzpzpp") => true // when no 'x' and 'o' is present should return true
XO("zzoo") => false
```

My Solution:
```python
def xo(s):
    # Initial Counter (equal even if none are present)
    xCount = 0
    oCount = 0
    
    # Main Program Loop
    for c in s:                          # for each character in string
        if (c == 'x') or (c == 'X'):     # x's added to xCount
            xCount += 1
        elif (c == 'o') or (c == 'O'):   # o's added to oCount
            oCount += 1
            
    if xCount == oCount:                 # if counts are equal
        return True
    
    else:                                # if counts are not equal
        return False
```

Other Possible Solutions:
```python
def xo(s):
    s = s.lower()
    return s.count('x') == s.count('o')
```
```python
def xo(s):
    return True if s.lower().count('x') == s.lower().count('o') else False
```
```python
def xo(s):
    return s.lower().count('x') == s.lower().count('o')
```


## 5. Beginner Series #3 Sum of Numbers

Description:

Given two integers `a` and `b`, which can be positive or negative, find the sum of all the integers 
between and including them and return it. If the two numbers are equal return `a` or `b`.

Note: `a` and `b` are not ordered!

Examples:
```
get_sum(1, 0) == 1   // 1 + 0 = 1
get_sum(1, 2) == 3   // 1 + 2 = 3
get_sum(0, 1) == 1   // 0 + 1 = 1
get_sum(1, 1) == 1   // 1 Since both are same
get_sum(-1, 0) == -1 // -1 + 0 = -1
get_sum(-1, 2) == 2  // -1 + 0 + 1 + 2 = 2
```

My Solution:
```python
def get_sum(a,b):
    sum = 0                        # initial sum
     
    if a == b:                     # if values are equal
        sum = a                    # sum is either vaue
         
    # if values are NOT equal: 
    elif a < b: 
        for i in range(a, b + 1):  # iterates over each integer including last value
            sum += i               # adds integer to sum
    elif b < a: 
        for i in range (b, a + 1): # iterates over each integer including last value
            sum += i               # adds integer to sum
            
    return sum                     # returns final sum total
```

Other Possible Solutions:
```python
def get_sum(a,b):
    return sum(range(min(a, b), max(a, b) + 1))
```
```python
def get_sum(a,b):
    if a>b : a,b = b,a
    return sum(range(a,b+1))
```
```python
def get_sum(a,b):
    return sum([x for x in range(min(a,b),max(a,b)+1)])
```


## 6. Sum of Two Lowest Positive Integers

Description:

Create a function that returns the sum of the two lowest positive numbers given an array of 
minimum 4 positive integers. No floats or non-positive integers will be passed.

For example, when an array is passed like `[19, 5, 42, 2, 77]`, the output should be `7`.

`[10, 343445353, 3453445, 3453545353453]` should return `3453455`.

My Solution:
```python
def sum_two_smallest_numbers(numbers):
    numbers.sort()                           # sorts lists, smallest to greatest
    return int(numbers[0]) + int(numbers[1]) # returns sum of lowest 2 values
```

Other Possible Solutions:
```python
def sum_two_smallest_numbers(numbers):
    return sum(sorted(numbers)[:2])
```
```python
def sum_two_smallest_numbers(numbers):
   numbers.sort()
   return numbers[0] + numbers[1]
```
```python
def sum_two_smallest_numbers(numbers):
    return sorted(numbers)[0] + sorted(numbers)[1]
```


## 7.
## 8.
## 9.
## 10.


---
[back to CodeWars main page](codeWars.md)

[back to Index/Table of Contents](index.md)
