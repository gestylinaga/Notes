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

On Windows: click `Start` button, type `Command Prompt`, then press `Enter`

On macOS: click the `Spotlight` icon, type `Terminal`, then press `Enter`

On Ubuntu Linux: press the `Super`/`Win` key, type `Terminal`, then press enter (or `CTRL+ALT+t`)

Just like how the interactive shell has a `>>>` prompt, the terminal shell has it's own prompt:
* on Windows: `C:\Users\gestylinaga>your command goes here`
* on macOS: `gestys-MacBook-Pro:~ gesty$ your command goes here`
* on Linux: `gesty@laptopcantstop:~$ your command goes here`

Note that many books/tutorials represent the command line prompt as just `$` to simplify their 
examples

### Running Programs from the Command Line

To run a program or command, enter its name into the command line

Running the default calculator program:
* on Windows: enter `calc.exe`
* on macOS: enter `open -a Calculator` (technically, this runs the `open` program, then runs the `Calculator` program)
* on Linux: enter `gnome-calculator`

Note that commands and program names are **case sensitive** on Linux, but not on Windows or macOS

These calculator programs work as commands because they (`calc.exe`, `open`, and `gnome-calculator`) 
exist in folders that are included in the `PATH` environment variables
* on Windows: the shell checks the cwd before checking folders in `PATH`
* on Linux and macOS: a `./` typed before a filename indicates cwd

If the program isn't in a folder listed in `PATH` you can:
* `cd` into the folder that contains the program
    - `cd C:\Windows\System32`
    - `calc.exe`
* enter the full file path
    - `C:\Windows\System32\calc.exe`

Note that on Windows, if a program ends with the file extension `.exe` or `.bat`, including the 
extension is optional. Entering `calc` is the same as entering `calc.exe`

### Using Command Line Arguments

*Command line arguments* are bits of text you enter after the command name

For example:
* `cd C:\Users`
    - `cd` is the command
    - `C:\Users` is the argument, tells `cd` which folder to change to
* `python3 yourScript.py`
    - `python3` is the command
    - `yourScript.py` is the argument, tells `python3` which file to seek for instructions

*Command line options* (aka flags, switches, or simply options) are a single-letter or short-word 
command line arguments
* on Windows: begin with a forward slash `/`
* on Linux/macOS: begin with a single dash `-` or double dash `--`

Note that folders/filenames with spaces in them should be wrapped in double quotes `""` to avoid 
confusing the shell with passing 2 arguments:
```powershell
C:\Users\gestylinaga>cd "Vacation Photos"

# instead of:
C:\Users\gestylinaga>cd Vacation Photos
```

Another common argument for many commands is `--help` on Linux/macOS, and `/?` on Windows, to bring 
up more information for the command

### Running Python Code from the Command Line with -c

The `-c` argument is used to run a small amount of throwaway Python code that you can run once and 
then discard:
```powershell
C:\Users\gestylinaga>python -c "print('Hello, world!')"
# this returns: Hello, world!
```
Note that the code comes **after** the `-c` flag, wrapped in double quotes `""`

The `-c` flag is handy for when you want to see the results of a single Python instruction and don't 
want to waste time entering the interactive shell. For example, to quickly display the output of 
the `help()` function and return to the command line:
```powershell
# on Windows PowerShell:

PS C:\Users\gestylinaga> python -c "help(len)"
Help on built-in function len in module builtins:

len(obj, /)
    Return the number of items in a container.

PS C:\Users\gestylinaga>
```

### Running Python Programs from the Command Line

Python scripts are text files that have the `.py` extension. They are **not** executable files; 
rather, the Python interpreter reads the text files and carries out the instructions

On Windows: `python yourScript.py`

On Linux/macOS: `python3 yourScript.py`

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
