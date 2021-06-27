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

Consider the task of renaming every file in some folder, and also every file in every subfolder of 
that folder, in this example the folder `C:\delicious`:

```
* C:\
    - delicious
        - cats
            + catnames.txt
            + zophie.jpg
        - walnut
            - waffles
                + butter.txt
        + spam.txt
```
Python has a way to *walk* you through the directory tree, touching each file as you go, using the 
`os.walk()` function:
```python
import os

for folderName, subfolders, filenames in os.walk('C:\\delicious'):
    print('The current folder is ' + folderName)

    for subfolder in subfolders:
        print('SUBFOLDER OF ' + folderName + ': ' + subfolder)

    for filename in filenames:
        print('FILE INSIDE ' + folderName + ': ' + filename)

    print('')
```
The `os.walk()` function is passed a single string value, and when used in a `for` loop return:
* a string of the current folder's name
* a list of strings of the **folders** in the current folder
* a list of strings of the **files** in the current folder

The output of the previous program, with the previous example directory tree:
```
The current folder is C:\delicious
SUBFOLDER OF C:\delicious: cats
SUBFOLDER OF C:\delicious: walnut
FILE INSIDE C:\delicious: spam.txt

The current folder is C:\delicious\cats
FILE INSIDE C:\delicious\cats: catnames.txt
FILE INSIDE C:\delicious\cats: zophie.jpg

The current folder is C:\delicious\walnut
SUBFOLDER OF C:\delicious\walnut: waffles

The current folder is C:\delicious\walnut\waffles
FILE INSIDE C:\delicious\walnut\waffles: butter.txt
```


## Compressing Files with the zipfile Module

ZIP files (with the `.zip` extension), hold the compressed contents of many other files

Compressing a file reduces its size, which is useful when transferring files over the internet

ZIP files are also known as *archive* files

Consider the contents of `example.zip`:
```
* cats
    - catnames.txt
    - zophie.jpg
* spam.txt
```

### Reading ZIP Files

To read the contents of a ZIP file, you must first create a *ZipFile* object (note the capital 'Z' 
and 'F')
```python
import zipfile, os
from pathlib import Path

p = Path.home()
exampleZip = zipfile.ZipFile(p / 'example.zip')

exampleZip.namelist()
# this returns ['spam.txt', 'cats/', 'cats/catnames.txt', 'cats/zophie.jpg']

spamInfo = exampleZip.getinfo('spam.txt')
spamInfo.file_size
# this returns: 13908

spamInfo.compress_size
# this returns: 3828

f'Compressed file is {round(spamInfo.file_size / spamInfo.compress_size, 2)}x smaller!'
# this returns: 'Compressed file is 3.63x smaller!'

exampleZip.close()
```

### Extracting from ZIP Files

The `extractall()` method for *ZipFile* objects extracts all the files and folders from a ZIP file 
into the current working directory:
```python
import zipfile, os
from pathlib import Path
p = Path.home()

exampleZip = zipfile.ZipFile(p / 'example.zip')
exampleZip.extractall()
exampleZip.close()
```
Note that running the code above would extract the contents of `example.zip` to `C:\`
    - optionally you can replace it with `exampleZip.extractall('C:\\delicious')` to extract it 
into a newly created `C:\delicious` folder if it doesn't already exist    

The `extract()` method for *ZipFile* objects will extract a single file from the ZIP file:
```python
exampleZip.extract('spam.txt')
# this returns: 'C:\\spam.txt'

exampleZip.extract('spam.txt', 'C:\\some\\new\\folders')
# this returns: `C:\\some\\new\\folders\\spam.txt'

exampleZip.close()
```
Notice that 
* the first example extracts the file to the *cwd* or the root directory in this case
* the second example has a second argument, the path to a folder other than the *cwd*
    - will create the necessary folders if necessary
    - returns the absolute path where the file was extracted

### Creating and Adding to ZIP Files

To create your own compressed ZIP files, you must open the *ZipFile* object in *write* mode by 
passing a `'w'` as the second argument: (similar to write mode in the `open()` function)
```python
import zipfile
newZip = zipfile.ZipFile('new.zip', 'w')
newZip.write('spam.txt', compress_type=zipfile.ZIP_DEFLATED)
newZip.close()
```
Note that the compress type `zipfile.ZIP_DEFLATED` refers to the *deflate* compression algorithm, 
which works well on all types of data

Also note that just as with writing to text files, `'w'` write mode will overwrite any existing 
files. If you want to add files to an existing ZIP file, you should pass an `'a'` as the second 
argument for *append mode*


## Summary

* The `os` and `shutil` modules offer functions for copying, moving, renaming, and deleting files
* The third-party `send2trash` module moves files to the trash/recyle bin instead of permanently 
deleting them
* When working with programs that handle files, it's smart to test run with `print()` calls before 
doing any actual deleting/moving/renaming
* The `os.walk()` function will perform operations on all files in a folder, and any nested files/folders
* The `zipfile` module has ways to compress and extract ZIP archives


## Practice Questions

1. What is the difference between `shutil.copy()` and `shutil.copytree()`?
    - `'shutil.copy()' is for single files`
    - `'shutil.copytree()' is for entire folders`
2. What function is used to rename files?
    - `the 'shutil.move(source, destination)' function, with a new name in the destination`
3. What is the difference between the `delete` functions in the `send2trash` and `shutil` modules?
    - `in 'send2trash' it is sent to the recycle bin`
    - `in 'shutil' it is premanently deleted`
4. ZipFile objects have a `close()` method just like File objects’ `close()` method. What ZipFile 
method is equivalent to File objects’ `open()` method?
    - `'zipfile.ZipFile()' and 'zipfile.extract()'`


---
[back to Automate the Boring Stuff with Python main page](atbswp.md)

[back to Index/Table of Contents](index.md)
