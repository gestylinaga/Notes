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

### Moving and Renaming Files and Folders

### Permanently Deleting Files and Folders

### Safe Deletes with the send2trash Module


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
