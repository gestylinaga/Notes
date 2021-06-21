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
* on Linux: appear as new folders under the `/mnt` or "mount" folder
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
from pathlib import Path
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

Two ways to specify a file path:
1. an *absolute path*, which **always** begins with the root folder
2. a *relative path*, which is relative to the program's current working directory

The *dot* `.` and *dot-dot* `..` folders, special names that can be used in a path
* dot `.` shorthand for "*this directory*"
* dot-dot `..` shorthand for "*the parent folder*"

ie: `.\spam.txt` and `spam.txt` refer to the same file

### Creating New Folders Using the os.makedirs() Function

Your programs can create new directories with the `os.makedirs()` function:
```python
import os
os.makedirs('C:\\delicious\\walnut\\waffles')
```
this creates the folder `waffles`, **and** any necessary intermediate folders to ensure that the 
full path exists (`delicious`, and `walnut` beforehand)

You can also make a directory from a *Path* object by calling the `mkdir()` method:
```python
from pathlib import Path
Path(r'C:\Users\Al\spam').mkdir()
# makes a folder named spam
```
Note that `mkdir()` can only make **one** folder at a time, and won't make subdirectories like 
`os.mkdirs()` can

### Handling Absolute and Relative Paths

The `pathlib` module provides the `is_absolute()` method, which when used on a *Path* object, 
returns `True` if it represents an absolute path, and `False` for relative paths:
```python
Path.cwd()
# on Windows this returns: WindowsPath('C:/Users/gestylinaga/GitHub/Notes/docs')

Path.cwd().is_absolute()
# this returns: True

Path('spam/bacon/eggs').is_absolute()
# this returns: False
```
To get an absoute path *from* a relative path, you can put `Path.cwd()` and `/` in front of the relative 
*Path* object:
```python
Path('my/relative/path')
# on Windows this returns: WindowsPath('my/relative/path')

Path.cwd() / Path('my/relative/path')
# on Windows this returns:
# WindowsPath('C:/Users/gestylinaga/GitHub/Notes/docs/my/relative/path')
```
or using the home directory instead:
```python
Path.home() / Path('my/relative/path') # notice the .home() insead of .cwd()
# on Windows this return:
# WindowsPath('C:/Users/gesteratops/my/relative/path')
```
The `os.path` module also has:
* `os.path.abspath(path)` will return a string of the absolute path of the argument, an *easy* way 
of converting a relative path into an absolute one
* `os.path.isabs(path)` will return `True` if the argument is an absolute path, and `False` if it 
is a relative path
* `os.path.relpath(path, start)` will return a string of a relative path from the *start* path to 
*path*. If *start* is not provided, the current working directory is used as the start path

`os.path` examples:
```python
os.path.abspath('.')
# on Windows this returns:
# 'C:\\Users\\gestylinaga\\Github\\Notes\\docs'

os.path.abspath('.\\Scripts')
# on Windows this returns:
# 'C:\\Users\\gestylinaga\\GitHub\\Notes\\docs\\Scripts'

os.path.isabs('.') # shorthand for "this directory"
# this returns: False

os.path.isabs(os.path.abspath('.'))
# this returns: True
```

### Getting the Parts of a File Path

The attributes of a file path:
```
# Windows:
C:\Users\gestylinaga\spam.txt
```
* `C:\` **Anchor**, or root folder of the filesystem
    - `C:` **Drive**, a physical hard drive, or other storage device
* `\Users\gestylinaga\` **Parent**, folder containing the file
* `spam.txt` **Name**
    - `spam` **Stem**, or *base name*
    - `.txt` **Suffix**, or *extension*
```
# Linux/macOS:
/home/gestylinaga/spam.txt
```
* `/` **Anchor**, or root folder of the filesystem
* `home/gestylinaga/` **Parent**, folder containing the file
* `spam.txt` **Name**
    - `spam` **Stem**, or *base name*
    - `.txt` **Suffix**, or *extension*

Note that Windows *Path* objects have a *drive* attribute, but macOS and Linux *Path* objects do 
**not**. Also note that the *drive* attribute doesn't include the first backslash `\`

To extract each attribute from the file path:
```python
p = Path('C:/Users/gestylinaga/spam.txt')

p.anchor
# this returns: 'C:\\'

p.parent # this is a path object, not a string
# this returns: WindowsPath('C:/Users/gestylinaga')

p.name
# this returns: 'spam.txt'

p.stem
# this returns: 'spam'

p.suffix
# this returns: '.txt'

p.drive
# this returns: 'C:'
```
The *parents* attribute (different from the *parent* attribute) evaluates to the ancestor folders 
of a *Path* object with an integer index:
```python
Path.cwd()
# returns:WindowsPath('C:/Users/gestylingaga/GitHub/Notes/docs')

Path.cwd().parents[0]
# returns: WindowsPath('C:/Users/gestylinaga/GitHub/Notes')

Path.cwd().parents[1]
# returns: WindowsPath('C:/Users/gestylinaga/GitHub')

Path.cwd().parents[2]
# returns: WindowsPath('C:/Users/gestylinaga')

Path.cwd().parents[3]
# returns: WindowsPath('C:/Users')

Path.cwd().parents[4]
# returns: WindowsPath('C:/')
```

The older `os.path` module has similar functions for getting the different parts of a path:
```
C:\Windows\System32\calc.exe
```
* `C:\Windows\System32` is the *Dir name*
* `calc.exe` is the *Base name*

Calling `os.path.dirname(path)` will return a string of everything that comes **before** the last 
slash in the *path* argument

Calling the `os.path.basename(path)` will return a string of everything that comes **after** the 
last slash in the *path* argument
```python
calcFilePath = 'C:\\Windows\\System32\\calc.exe'

os.path.basename(calcFilePath)
# this returns: 'calc.exe'

os.path.dirname(calcFilePath)
# this returns: 'C:\\Windows\\System32'
```
or, you can call `os.path.split()` to get a tuple value of the 2 strings:
```python
calcFilePath = 'C:\\Windows\\System32\\calc.exe'

os.path.split(calcFilePath)
# this returns: ('C:\\Windows\\System32', 'calc.exe')
```
you can also do this by calling `os.path.dirname()`/`os.path.basename()`, and placing their return 
values inside a tuple:
```python
calcFilePath = 'C:\\Windows\\System32\\calc.exe'

(os.path.dirname(calcFilePath), os.path.basename(calcFilePath))
# this returns: ('C:\\Windows\\System32', 'calc.exe')
```

### Finding File Sizes and Folder Contents

* Calling `os.path.getsize(path)` will return the size in bytes of the file 
* Calling `os.listdir(path)` will return a list of filename strings for each file in the 
    - important to note, this is in the `os` module, **not** `os.path`

```python
os.path.getsize('C:\\Windows\\System32\\calc.exe')
# this returns: 27648

os.listdir('C:\\Windows\\System32')
# this returns:
# ['0409', '12520437.cpx', '12520850.cpx', '5U877.ax', 'aaclient.dll',
# --snip--
# 'xwtpdui.dll', 'xwtpw32.dll', 'zh-CN', 'zh-HK', 'zh-TW', 'zipfldr.dll']
```
To find the total size of all the files in a directory, you can use `os.path.getsize()` and `os.listdir()` 
together:
```python
totalSize = 0
for filename in os.listdir('C:\\Windows\\System32'):
    totalSize = totalSize + os.path.getsize(os.path.join('C:\\Windows\\System32', filename))
print(totalSize)
# this returns the total size in bytes
```

### Modifying a List of Files Using Glob Patterns

Using the `glob()` method is simpler than using `listdir()` to work on specific files:
* glob patterns are a simplified version of regular expressions
* return a *generator* object, which require a `list()` to easily view
```python
p = Path('C:/Users/Al/Desktop')

p.glob('*')
# this returns:
# <generator object Path.glob at 0x000002A6E389DED0>

list(p.glob('*')) # Make a list from the generator.
# this returns:
# [WindowsPath('C:/Users/Al/Desktop/1.png'), WindowsPath('C:/Users/Al/
# Desktop/22-ap.pdf'), WindowsPath('C:/Users/Al/Desktop/cat.jpg'),
#   --snip--
# WindowsPath('C:/Users/Al/Desktop/zzz.txt')]
```

**Creating complex expressions like regex**:

An asterisk `*` for "multiple of any character":
```python
list(p.glob('*.txt') # Lists all text files
# this returns:
# [WindowsPath('C:/Users/Al/Desktop/foo.txt'),
#   --snip--
# WindowsPath('C:/Users/Al/Desktop/zzz.txt')
```
The question mark `?` for "any single character":
```python
list(p.glob('project?.docx')
# this returns:
# [WindowsPath('C:/Users/Al/Desktop/project1.docx'), WindowsPath('C:/Users/Al/
# Desktop/project2.docx'),
#   --snip--
# WindowsPath('C:/Users/Al/Desktop/project9.docx')]
```
Combining both for something complex:
```python
list(p.glob('*.?x?')
# this returns:
# [WindowsPath('C:/Users/Al/Desktop/calc.exe'), WindowsPath('C:/Users/Al/
# Desktop/foo.txt'),
#   --snip--
# WindowsPath('C:/Users/Al/Desktop/zzz.txt')]
```
Using a for loop to iterate ober the generator that `glob()` returns:
```python
p = Path('C:/Users/Al/Desktop')
for textFilePathObj in p.glob('*.txt'):
    print(textFilePathObj) # Prints the Path object as a string
    # Do something with the text file.
```

### Checking Path Validity

Most Python functions will crash with an error if you supply them with a path that does not exist, 
but *Path* objects have methods to check whether a given path exists and whether it is a file/folder:
* calling `p.exists()` returns `True` if the path exists, or returns `False` if it doesn't exist
* calling `p.is_file()` returns `True` if the path exists **and** is a file
* calling `p.is_dir()` returns `True` if the path exists **and** is a directory

```python
winDir = Path('C:/Windows')
notExistsDir = Path('C:/This/Folder/Does/Not/Exist')
calcFile = Path('C:/Windows/System32/calc.exe')

winDir.exists()
# this returns: True

winDir.is_dir()
# this returns: True

notExistDir.exists()
# this returns: False

calcFile.is_File()
# this returns: True

calcFile.is_dir()
# this returns: False
```
For example, checking for a flash drive with the volume name `D:\`:
```python
dDrive = Path('D:/')
dDrive.exists()
# this returns: False
```
Note that the older `os.path` module can accomplish the same task with:
* `os.path.exists(path)`
* `os.path.isfile(path)`
* `os.path.isdir(path)`


## The File Reading/Writing Process

*Plaintext files* contain only basic text characters and do not include font, size, or color info:
* *.txt* -- text files
* *.py* -- Python script files

*Binary files* are all other file types, such as:
* word processing documents
* PDFs
* images
* spreadsheets
* executable programs

### Opening Files with the open() Function

### Reading the Contents of Files

### Writing to Files


## Saving Variables with the Shelve Module


## Saving Variables with the pprint.pformat() Function


## Summary


## Practice Questions

1. What is a relative path relative to?
    - `relative to the current working directory`
2. What does an absolute path start with?
    - `always starts with the root folder`
3. What does `Path('C:/Users') / 'Al'` evaluate to on Windows?
4. What does `'C:/Users' / 'Al'` evaluate to on Windows?
5. What do the `os.getcwd()` and `os.chdir()` functions do?
6. What are the `.` and `..` folders?
    -   `'.' is 'this directory'`
    - `'..' is 'parent directory'`
7. In `C:\bacon\eggs\spam.txt`, which part is the dir name, and which part is the base name?
8. What are the three “mode” arguments that can be passed to the `open()` function?
9. What happens if an existing file is opened in write mode?
10. What is the difference between the `read()` and `readlines()` methods?
11. What data structure does a shelf value resemble?


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
