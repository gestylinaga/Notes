# Reading and Writing Files

## Files and File Paths

A file has 2 properties: a **filename** (usually 1 word), and a **path** (location on the computer)

For example: the filename `project.docx` in the path `C:\Users\Al\Documents`:
* the `.docx` is the file's *extension*, which tells you a file's type
    - `project.docx` is a Microsoft Word document
* the `Users`, `Al`, and `Documents` all refer to *folders*, aka *directories*
* the `C:\` part of the path it the *root folder*, which contains **all** other folders
    - known as `C:\` or `C:` *drive* on Windows
    - simply `/` on macOS and Linux

Additional drives, like a DVD drives or USB flash drives, are known as *volumes*:
* on Windows: appear as new, lettered root drives (such as `D:\` or `E:\`)
* on macOS: appear as new folders under the `/Volumes` folder
* on Linux: appear as new folders under the `/mnt` or 'mount' folder
    - note that file/folder names are case-sensitive in Linux

### Backslash on Windows and Forward Slash on macOS and Linux

* **Windows** uses the backslash `\` character as the separator between folder names

* **Linux** and **macOS** use the forward slash `/` character as the path separator

Note that if you want your program to work on all operating systems, you have to account for this

A simple way to do this, is the the `Path()` function in the `pathlib` module:
```python
from pathlib import Path         # saves from typing 'pathlib.Path' each time
Path('spam', 'bacon', 'eggs')
# on Windows, this returns: 
# WindowsPath('spam/bacon/eggs') # shows as forward slashes, but 'WindowsPath' object auto changes it

str(Path('spam', 'bacon', 'eggs'))
# this returns: 
# 'spam\\bacon\\eggs'            # simple string version of what the actual path looks like
```
Note that on Windows, a `WindowsPath` object is returned by `Path()`, but on Linux (or any other 
Unix-like OS), a `PosixPath` object is returned

These *Path* objects can be passed to several file-related functions, for example:
```python
from pathlib import Path
myFiles = ['accounts.txt', 'details.csv', 'invite.docx']
for filename in myFiles:
    print(Path(r'C:\Users\Al', filename))
```
this returns:
```
C:\Users\Al\accounts.txt
C:\Users\Al\details.csv
C:\Users\Al\invite.docx
```
On Windows, the backslash `\` character separates directories, so you can **not** use it in filenames 

This is not a problem in Linux/macOS

so `Path(r'spam\eggs')` refers to: 
* the file `egg` in the folder `spam` on **Windows**
* the folder `spam\eggs` on **Linux/macOS**

Therefore best practice is to use forward slashes `/` as the separator in Python code, and the 
`pathlib` module ensures it will work on all operating systems

Note that `pathlib` was introduced in Python 3.4 to replace `os.path` functions

[Official os.path Docs from Python](https://docs.python.org/3/library/os.path.html)

### Using the / Operator to Join Paths

Just like `+` is used to join strings, `/` can be used to join *Path* objects and strings:
```python
from pathlib import Path

Path('spam') / 'bacon' / 'eggs'
# on Windows this returns:
# WindowsPath('spam/bacon/eggs')

Path('spam') / Path('bacon/eggs')
# on Windows this returns:
# WindowsPath('spam/bacon/eggs')
```
this is safer/easier than: 
```python
# Using a '+':
homeFolder = r'C:\Users\Al'
subFolder = 'spam'
homeFolder + '\\' + subFolder
# this returns: `C:\\Users\\Al\\spam'

# Using the .join() method:
'\\'.join([homeFolder, subFolder])
# this returns: `C:\\Users\\Al\\spam'
```
this code is considered *unsafe* because the backslashes `\` would only work on Windows systems

but, `pathlib` solves this:
```python
homeFolder = Path('C:/Users/Al')
subFolder = Path('spam')
homeFolder / subFolder
# this returns:
# WindowsPath('C:/User/Al/spam')

str(homeFolder / subFolder) # for a string version on the output
# this returns: 'C:\\Users\\Al\\spam'
```
Important to note that when using the `/` operator for joining paths, one of the first two values 
must be a *Path* object, otherwise you'll get a `TypeError`

Python evaluates the `/` operator from left to right, and evaluates to a *Path* object, which is the 
reason why one of the first 2 values have be a *Path* object, because it adds the rest of the strings 
to the original *Path*

The `/` operator replaces the `os.path.join()` function -- [see Official Python Docs](https://docs.python.org/3/library/os.path.html#os.path.join)

### The Current Working Directory

Every program that runs on a computer has a *current working directory*, or *cwd*

Any filenames or paths that do **not** begin with the root folder are assumed to be under the *cwd*

You can get the current working directory as a string value with the `Path.cwd()` function, and 
changing it using `os.chdir()`:
```python
from pathlib impot Path
import os
Path.cwd()
# on Windows this returns:
# WindowsPath('C:/Users/gestylinaga/GitHub/Notes/docs')

os.chdir('C:\\Windows\\System32')
Path.cwd()
# on Windows this returns:
# WindowsPath('C:/Windows/System32')
```
Note that Python will return a `FileNotFoundError` if you try to change to a directory that does 
**not** exist

There is **no** `pathlib` function for changing the working directory

Before `pathlib`, the old way to get the *cwd* was the `os.getcwd()` function

### The Home Directory

The function `Path.home()` returns a *Path* object of the home directory:
```python
Path.home()
# on Windows this returns:
# WindowsPath('C:/Users/gestylinaga')
```
Depending on the OS:
* on Windows, under `C:\Users`
* on Mac, under `/Users`
* on Linux, under `/home`

### Absolute vs. Relative Paths

### Creating New Folders Using the os.makedirs() Function

### Handling Absolute and Relative Paths


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
