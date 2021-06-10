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


## 4.
## 5.
## 6.
## 7.
## 8.
## 9.
## 10.


---
[back to CodeWars main page](codeWars.md)

[back to Index/Table of Contents](index.md)
