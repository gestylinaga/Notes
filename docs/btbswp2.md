# Environment Setup and the Command Line

*Environment Setup* is the process of organizing your computer so you can write code

This involves:
* Installing any necessary tools
* Configuring said tools
* Handling any hiccups in the process

There is no single setup process because everyone has a different computer with a different operating 
system, with different versions of that OS, with different versions of Python, and so on...


## The Filesystem

The *filesystem* is how your operating system organizes data to be stored and retrieved

A *file* has 2 properties: a *filename*, and a *path*

For example imagine a file:`C:\Useres\gestylinaga\Documents\project.docx`
* The filename is: `project.docx`
* The path is: `C:\Useres\gestylinaga\Documents`
    - `Users`, `gestylinaga`, and `Documents` are all referred to as *folders* (aka *directories*)
    - `C:\` is considered the *root folder* (which contains all other folders)
        + `C:\` is the root folder on Windows machines
        + `/` is the root folder on Linux/macOS

Note that additional volumes, like a DVD drive/USB flash drive, will appear as:
* On Windows: new lettered root drives like `D:\` or `E:\`
* On macOS: new folders in `/Volumes`
* On Linux: new folders in `/mnt` ("mount")

### Paths in Python

On Windows, the backslash `\` separates folders/filenames

But on Linux/macOS, the forward slash `/` separates folders/files

To simplify the hassle, just use the `Path` function from the `pathlib` module:
```python
from pathlib import Path
# Note: examples run on a Windows machine

Path('spam') / 'bacon' / 'eggs'
# this returns: WindowsPath('spam/bacon/eggs')

Path('spam') / Path('bacon/eggs')
# this returns: WindowsPath('spam/bacon/eggs')

Path('spam') / Path('bacon', 'eggs')
# this returns: WindowsPath('spam/bacon/eggs')
```
Notice that since the examples are being run on a Windows machine, the return is a `WindowsPath`

Linux and macOS machines will return a `PosixPath` object instead

### The Home Directory

All users have a *home folder* or *home directory* for their own files on a machine. 
* On Windows: in `C:\Users`
* On macOS: in `/Users`
* On Linux: in `/home`

You can get the *Path* object of the home folder by calling:
```python
Path.home()
# this returns: WindowsPath('C:/Users/gestylinaga')
```

### The Current Working Directory

Every program that runs on your computer has a *current working directory* (or *cwd*). Any filenames/paths 
that don't start with the root folder are assumed to be in the *cwd*.

You can get the *Path* object of the cwd, and change directories by calling:
```python
from pathlib import Path
import os

Path.cwd()
# this returns: WindowsPath('C:/Users/gestylinaga/Github/Notes')

os.chdir('C:\\Windows\\System32')
Path.cwd()
# now this returns: WindowsPath('C:/Windows/System32')
```
Note that the older way (on older versions of Python) to do this was with `os.getcwd()`

### Absolute vs. Relative Paths

Two ways to specify a file path:
* An *absolute path*, which laways beings with the root folder
* A *relative path*, which is relative to the current working directory

There is also the dot `.` and dot-dot `..` which aren't *real* folders:
* `.` for "this directory"
* `..` for "the parent folder"

For example: `.\spam.txt` and `spam.txt` refer to the same file


## Programs and Processes

A *program* is any software application that you can run, such as:
* A web browser
* A spreadsheet application
* A word processor

A *process* is a running instance of a program. Processes are separate from each other, even when 
running the same program.

To view a list of running processes:
* On Windows: `CTRL+SHIFT+ESC` to bring up the Task Manager application
* on macOS: run `Applications > Utilities > Acitvity Monitor`
* on Ubuntu Linux: `CTRL+ALT+DEL` to bring up the Task Manager application


## The Command Line

The *command line* is a text-based program that let you enter commands to interact with the 
operating system, and run programs.

Other names:
* the Command Line Interface (or CLI)
* Command Prompt
* terminal
* shell
* console

The command line program exists in an executable file on your computer:
* on Windows: `C:\Windows\System32\cmd.exe`
* on macOS: `/bin/bash`
* on Linux: `/bin/bash`

### Opening a Terminal Window

### Running Programs from the Command Line

### Using Command Line Arguments

### Running Python Code from the Command Line with -c

### Running Python Programs from the Command Line

### Running the py.exe Program

### Running Commands from a Python Program

### Minimizing Typing with Tab Completion

### Viewing the Command History

### Working with Common Commands

> Short Command Names


## Environment Variables and PATH

### Viewing Environment Variables

### Working with the PATH Environment Variable

### Changing the Command Line's PATH Environment Variable

### Permanently Adding Folders to PATH on Windows

### Permanently Adding Folders to PATH on macOS and Linux


## Running Python Programs Without the Command Line

### Running Python Programs on Windows

### Running Python Programs on macOS

### Running Python Programs on Ubuntu Linux


## Summary 


---
[back to Beyond the Basic Stuff with Python](btbswp.md)

[back to Index/Table of Contents](index.md)
