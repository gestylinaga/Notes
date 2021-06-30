# Dealing with Errors and Asking for Help

Computers are the most sophisticated tools most of us will ever interact with, but still, they're 
just tools

As a programmer, being able to find answers on your own is far more important than any algorithm or 
data structure knowledge


## How to Understand Python Error Messages

Finding answers is a two-step process:
1. examining the traceback
2. doing an internet search of the error message

### Examining Tracebacks

Python programs crash when the code raises an exception that an `except` statement doesn't handle

When this happens, Python displays the exception's message and a **traceback** (aka a *stack trace*)
* shows the place in your program where the exception happened and the trail of functions that led 
up to it

Example buggy program, *abcTraceback.py*:
```python
def a():
    print('Start of a()')
    b() # calls b()

def b():
    print('Start of b()')
    c() # calls c()

def c():
    print('Start of c()')
    42 / 0 # Causes a zero divide error

a() # calls a()
```
this returns:
```
Start of a()
Start of b()
Start of c()
Traceback (most recent call last):
  File "C:\Users\gestylinaga\Github\Notes\abcTraceback.py", line 13, in <module>
    a() # calls a()
  File "C:\Users\gestylinaga\Github\Notes\abcTraceback.py", line 3, in a
    b() # calls b()
  File "C:\Users\gestylinaga\Github\Notes\abcTraceback.py", line 7, in b
    c() # calls c()
  File "C:\Users\gestylinaga\Github\Notes\abcTraceback.py", line 11, in c
    42 / 0 # Causes a zero divide error
ZeroDivisionError: division by zero
```
**Traceback Breakdown**: (by line)
```
Traceback (most recent call last):
```
* lets you know that the following message is a traceback
* also indicates that calls are listed in order of when they were called (most recent call being last)
```
File "C:\Users\gestylinaga\Github\Notes\abcTraceback.py", line 13, in <module>
    a() # calls a()
```
* **Frame Summary** -- show information inside a frame object
* **Frame Object** -- hold local variables and other data associated with function calls
    - created when the function is called; destroyed when the function returns
```
File "C:\Users\gestylinaga\Github\Notes\abcTraceback.py", line 3, in a
  b() # calls b()
File "C:\Users\gestylinaga\Github\Notes\abcTraceback.py", line 7, in b
  c() # calls c()
```
* these next 4 lines are the next 2 frame summaries
* notice that the `print()` calls are not included in the traceback
    - only the lines containing function calls that lead up to the exception
```
File "C:\Users\gestylinaga\Github\Notes\abcTraceback.py", line 11, in c
  42 / 0 # Causes a zero divide error
ZeroDivisionError: division by zero
```
* The last frame summary shows the line that caused the unhandled exception
* also shows the name of the exception and the exception's message

Note that the line number given by the traceback is where Python finally detected an error, not 
necessarily where the bug is

In the above example, the `ZeroDivisionError` is easy to detect, because we can see the line:
```
42 / 0
```
in the code, but for a more complicated example, *zeroDivideTraceback.py*:
```python
def spam(number1, number2):
    return number1 / (number2 - 42)

spam(101, 42)
```
this returns:
```
Traceback (most recent call last):
  File "C:\Users\gestylinaga\Github\Notes\zeroDivideTraceback.py", line 4, in <module>
    spam(101, 42)
  File "C:\Users\gestylinaga\Github\Notes\zeroDivideTraceback.py", line 2, in spam
    return number1 / (number2 - 42)
ZeroDivisionError: division by zero
```
Notice how you get the same `ZeroDivisionError`, but the cause is not as obvious

Sometimes the traceback might indicate an error on the line **after** the true cause of the bug:
```python
print('Hello.' # missing the closing `)`
print('How are you?')
```
this returns:
```
File "<stdin>", line 2
    print('How are you?')
    ^
SyntaxError: invalid syntax
```
Notice how the error is on line 1, but the error message shows line 2

This is because the Python interpreter didn't notice the syntax error until it read the second line. 
Traceback errors can indicate where things went wrong, but that isn't always the same as where the 
actual cause of the bug is.

### Searching for Error Messages

Error messages are usually short, and **not** full sentences

They are meant to be *reminders* to programmers who see them often

But, for more information you can type them into an internet search engine:
* include the keyword `python`
* use double quotes `""` to enlcose the error message

ie: typing `python "ZeroDivisionError: division by zero"` into google


## Preventing Errors with Linters

The best way to fix mistakes it to not make them in the first place

Lint software, or *linters*, are applications that analyze your source code to warn you of any 
potential errors
* The name references the small fibers and debris collected by a clothes dryer's lint trap

Many text editors and IDEs incorporate a linter that runs in the background, and can point out 
problems in real time

If your editor/IDE does **not** come with a linter, you can install the plug-in/module `pyflakes`:
* [Official Pyflakes Website](https://pypi.org/project/pyflakes/)
* on Windows: `pip install --user pyflakes`
* on Linux/macOS: `pip3 install pyflakes`

Note that IDLE, the IDE that comes with Python, does **not** have a linter, or the capability of 
installing one


## How to Ask for Progamming Help

There is an etiquette to efficiently asking for programming advice on the internet

Asking strangers for help should be a last resort:
* no guaranteed timeframe response
* not guaranteed correct

Instead you should search for question that have already been answered, or online documentation

Common mistakes to avoid:
* asking if it's ok to ask a question, instead of just asking it
* implying your question, instead of directly asking it
* asking your question on the wrong forum/website
* writing an unspecific headline/title like "I have a problem" or "Please help"
* sating "my program doesn't work", but not explaining what you want it to do
* not including the **full** error message
* not sharing your code
* sharing poorly formatted code
* not explaining what you've already tried
* not giving operation system or version information
* asking someone to write a program for you

Remember someone's first step in helping you is usually running your code, and trying to reproduce 
your errors. It far more common to give too little information than too much.

### Limit Back and Forth by Providing your Information Upfront

Avoid:
* asking if it's ok to ask a question, instead of just asking it

Asking for help isn't like a real life conversation, there's no need for niceties. In real conversation, 
asking if can ask a question is fine, it checks to see if the listener has time to help. Online, people 
can just hold off on answering until they know the answer, no need to wait.

### State Your Question in the Form of an Actual Question 

Avoid:
* implying your question, instead of directly asking it

It's easy to assume that someone helping you knows exactly what you're talking about when you explain 
your problem, but that is **not** always the case. Although sentences that start with, "I want to..." 
and "The code isn't working" can imply a question, be sure to include explicit questions.

Literally, just a sentence with a question mark `?`, otherwise it's probably unclear what you're asking

### Ask Your Question on the Appropriate Website

Avoid:
* asking your question on the wrong forum/website

Asking a Python question on a JavaScript forum, or an algorithm question on a network security 
mailing list is obviously unproductive

Mailing lists and forums usually have a *Frequently Asked Questions* (aka FAQ), that detail what 
topics are appropriate to discuss there

see [Python's Official Help Page](https://www.python.org/about/help/)

### Summarize Your Question in the Headline

Avoid:
* writing an unspecific headline/title like "I have a problem" or "Please help"

Documenting your question, and the subsequent answer, for future programmers on the internet
is part of the benefit of asking it online. Having a concise title/headline makes it easier 
for search engines to find. For emails, having a meaningful subject line lets whoever is helping 
see your question while scanning their inbox.

### Explain What You Want the Code to Do

Avoid:
* sating "my program doesn't work", but not explaining what you want it to do

Your/your program's intentions are not always obvious. Even a simple question like "Why am I 
getting this error?" benefits from knowing the end-goal. In some cases, someone might point 
out a completely different approach, and you can abandon your problem altogether.

### Include the Full Error Message

Avoid:
* not including the **full** error message

Make sure to copy/paste the **entire** error message, including the traceback.

It's also helpful to describe how often you encounter the problem. If it only happens during 
certain circumstances, share those details too.

### Share Your Complete Code

Avoid:
* not sharing your code

Along with the full error code (including full traceback), it's important to supply your 
program's entire source code. This lets whoever is helping you run your program on their 
machine, under a debugger, to see what's happening.

If your program is just 1 file, it's easy to just send it over for examination

But for bigger projects, it's important to produce a *minimum*, *comlete*, and *reproducible* (*MCR*) 
example that reliably reproduces your problem (name comes from StackOverflow):
* 'Minimal' meaning the code example is as short as possible (while still being able 
to reproduce the problem)
* 'Complete' meaning the code example contains everything it needs to reproduce the 
problem
* 'Reproducible' meaning the code example **reliably** reproduces the problem

> Stack Overflow and Building an Answer Archive
>> The purpose of Stack Overflow is to exist as an *answer archive* on the internet, it's 
>> **not** a place for simple general questions. It's real purpose is **not** a place to answer 
>> questons really, but instead it's to build and archive of programming questions 
>> matched with their answers.
>
>> Meaning they're looking for specific, unique, and non-opinionated questions. The 
>> questions need to be detailed and well-stated so that search engines can find them.
>
>> see the XKCD comic: ["Wisdom of the Ancients"](https://xkcd.com/979/) to see what the internet was like 
>> before Stack Overflow
>
>> see Stack Overflow's guide ["How do I ask a good question?"](https://stackoverflow.com/help/how-to-ask/)
>
>> for a more casual forum to ask questions, see [r/learnpython](https://old.reddit.com/r/learnpython/)

### Make Your Code Readable with Proper Formatting

Avoid:
* sharing poorly formatted code

Part of making code *readable* is making sure it's properly formatted. Your helper's intent is to 
copy your code and run your program on their machine. 

But, if you copy/paste your source code into some email clients, they might remove all indentation:
```python
# Improper Formatting: (no indents)
def knuts(self, value):
if not isinstance(value, int) or value < 0:
raise WizCoinException('kuts attr must be a positive int')
self._knuts = value
```
To make sure your code is properly formatted, you can enter it into a *pastebin* website like:
* [Pastebin](https://pastebin.com/)
* [Github Gist](https://gist.github.com/)

These store your code snippets as a short, public URL like: `https://pastebin.com/XeU3yusC`

If you're entering code into [Stack Overflow](https://stackoverflow.com/), [r/learnpython](https://old.reddit.com/r/learnpython/), 
or a similar forum, use the available text box tools:
* Indent with 4 spaces `'    '` *usually* changes to a monospace *Code Font*, which is easier to read
* Enclosing code with `backticks` also changes it to monospace *Code Font*

Otherwise, forum text boxes might render your code as:
```python
# Improper Formatting: (no line breaks)
def knuts(self, value):if not isinstance(value, int) or value < 0:raise WizCoinException('kuts attr must be a positive int')self._knuts = value
```

Note that taking screenshots of code is **not** efficient. It makes it impossible to copy/paste and 
subsequently run your program. It usually makes it harder to read too.

### Tell Your Helper what You've Already Tried

Avoid:
* not explaining what you've already tried
* asking someone to write a program for you

Explaining what you've already done, and the results of those efforts has multiple benefits:
* Avoids helper retrying those *false leads*
* Shows you've put in effort yourself
* Shows you're asking for *Help*, not asking someone to code for you

### Describe Your Setup

Avoid:
* not giving operation system or version information

Your machine's particular setup might affect how your program runs, and what errors it produces. To 
make sure anyone helping can reproduce your error, it's important to inlcude:
* The operating system and version
    - "Windows 10 Professional"
    - "macOS Catalina"
* The Python version 
    - "Python 3.7"
    - "Python 3.6.6"
* Any third-party modules and their versions
    - "Django 2.1.1"

Note that you can find the versions of third-party modules by running `pip list` in the terminal

Or, in the interactive shell:
```python
import django
django.__version__
# this returns: '2.1.1'
```
This info may be unnecessary, but it's informative to include it anyways

## Examples of Asking a Question

A properly asked question:
```
Selenium webdriver: How do I find ALL of an element's attributes?

In the Python Selenium module, once I have a WebElement object I can get the value of any of its 
attributes with get_attribute():

    foo = elem.get_attrubute('href')

If the attribute name 'href' doesn't exist, None is returned.

My question is, how can I get a list of all the attributes that an element has? There doesn't seem 
to be a get_attributes() or get_attribute_names() method.

I'm using version 2.44.0 of the Selenium module for Python 
```


## Summary

* Independently answering your own programming questions is the most important skill a programmer 
**must** learn
* Programmers made the internet...programming answers can be found on the internet too
* Error messages can be copy/pasted into google for more information
* The error's traceback shows where in the program the error occured
* Linters point out typos in real-time
* If you can't find the answer on the internet, post the a question to a forum/in an email
* Remember that *Not knowing* something is fine, even experienced progammers have to look up answers. 
The skill to focus on is being proficient in finding solutions.


---
[back to Beyond the Basic Stuff with Python main page](btbswp.md)

[back to Index/Table of Contents](index.md)
