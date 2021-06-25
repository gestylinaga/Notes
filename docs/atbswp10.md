# Organizing Files

Consider the tasks:
* Making copies of all PDF files (and *only* the PDF files) in every subfolder of a folder
* Removing the leading zeros in the filename for every file in a folder of hundreds of files
    - ie: *spam001.txt*, *spam002.txt*, *spam003.txt*
* Compressing the contents of several folders into one zip file (like a backup system)

These can all be **automated** by Python

Note that filetype extensions are shown automatically on **Linux and macOS**

But on **Windows**:
1. Start
2. Control Panel
3. Appearance and Personalization
4. Folder Options
    - In the 'View' tab
    - Under Advanced Settings
    - Uncheck 'Hide extensions for known file types'


## The Shutil Module

The `shutil` module provides functions to copy, move, rename, and delete files in your Python 
programs:
```python
import shutil
```

### Copying Files and Folders

Calling `shutil.copy(source, destination)` will copy the file at the path *source* to the folder at 
the path *destination*:
* Note that both *source* and *destination* can be strings **or** *Path* objects
* If *destination* is a filename, it will be used as the new name of the copied file

```python
import shutil, os
from pathlib import Path
p = Path.home()

shutil.copy(p / 'spam.txt', p / 'some_folder')
# on Windows this returns: 'C:\\Users\\gestylinaga\\some_folder\\spam.txt' (path of newly copied file)

shutil.copy(p / 'eggs.txt', p / 'some_folder/eggs2.txt')
# on Windows this returns: WindowsPath('C:/Users/gestylinaga/some_folder/eggs2.txt')
```
Notice that the first example uses the **same** filename for the newly copied file, while the second 
example uses the new name `eggs2.txt`

The `shutil.copytree()` will copy an entire folder and every folder/file contained in it:
```python
import shutil, os
from pathlib import Path
p = Path.home()

shutil.copytree(p / 'spam', p / 'spam_backup')
# on Windows this returns: WindowsPath('C:/Users/Al/spam_backup')
```
this effectively makes a *backup* of everything inside the `'spam'` folder

### Moving and Renaming Files and Folders

Calling `shutil.move(source, destination)` will move the file/folder at the path *source* to the 
path *destination*, and will return a string of the absolute path of the new location

If *destination* points to a folder, the *source* file gets moves into *destination* and keeps its 
current file name:
```python
import shutil
shutil.move('C:\\bacon.txt', 'C:\\eggs')
# this returns: 'C:\\eggs\\bacon.txt'
```
Note that if a file already exists at the *destination*, it will be overwritten

If the *destination* is a filename, the *source* file is moved **and** renamed:
```python
shutil.move('C:\\bacon.txt', 'C:\\eggs\\new_bacon.txt')
# this returns: 'C:\\eggs\\new_bacon.txt'
```
Note that both previous examples assume a folder named `'eggs'` already exists, if not, the file 
`bacon.txt` will be renamed to `eggs` (a text file with no extension):
```python
shutil.move('C:\\bacon.txt', 'C:\\eggs')
# this returns: 'C:\\eggs'
```
Final note, the folders that make up the *destination* must already exist, or Python will throw an 
exception:
```
>>> shutil.move('spam.txt', 'c:\\does_not_exist\\eggs\\ham')
Traceback (most recent call last):
  --snip--
FileNotFoundError: [Errno 2] No such file or directory: 'c:\\does_not_exist\\
eggs\\ham'
```

The `move()` call can be very tricky to work with, keep the *Notes* in mind

### Permanently Deleting Files and Folders

Single files or a single empty folder can be deleted with functions in the `os` module, while the 
`shutil` module lets you delete a folder and all of its contents:
* calling `os.unlink(path)` will delete the file at *path*
* calling `os.rmdir(path)` will delete the folder at *path* (must be empty)
* calling `shutil.rmtree(path)` will remove the folder at *path*, and all files/folders it contains

Note that working with these functions can be dangerous, it is often a good idea to start with these 
calls commented out, with `print()` calls to show the files to be deleted first

Consider the following typo:
```python
import os
from pathlib import Path
for filename in Path.home().glob('*.rxt'): # typo here, '.rxt' instead of '.txt'
    os.unlink(filename)
```
If you have any important files with the extension `.rxt`, they would be permanently deleted

Instead, a safer way to first run the program would be:
```python
import os
from pathlib import Path
for filename in Path.home().glob('*.rxt'): # typo here, '.rxt' instead of '.txt'
    #os.unlink(filename)
    print(filename) # reveals that '.rxt' are chosen instead of '.txt'
```
Notice that the `print()` call will reveal the filenames to be deleted, while the `os.unlink()` call 
is commented out for safety

Once you are sure your program is working correctly (pointing to the correct files), you can 
uncommment the `os.unlink()` line, and delete the `print()` line, to make the program run as 
intended

### Safe Deletes with the send2trash Module

The third-party `send2trash` module is a safer way to delete files, because it sends files/folders 
to your computer's trash or recycle bin instead of permanently deleting them

Note that `send2trash` must be installed with `pip`:
```
pip install --user send2trash
```
After installation:
```python
import send2trash

baconFile = open('bacon.txt', 'a') # creates the file
baconFile.write('Bacon is not a vegetable.')
# this returns: 25 (number of characters added)

baconFile.close()
send2trash.send2trash('bacon.txt')
```
Note that the `send2trash()` function can only send files to the recycle bin, it **cannot** pull 
files out of it


## Walking a Directory Tree


## Compressing Files with the zipfile Module

### Reading ZIP Files

### Extracting from ZIP Files

### Creating and Adding to ZIP Files


## Summary


## Practice Questions

1. What is the difference between `shutil.copy()` and `shutil.copytree()`?
2. What function is used to rename files?
3. What is the difference between the `delete` functions in the `send2trash` and `shutil` modules?
4. ZipFile objects have a `close()` method just like File objects’ `close()` method. What ZipFile 
method is equivalent to File objects’ `open()` method?


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
