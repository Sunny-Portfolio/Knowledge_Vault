###### Example things to do with Python:
- Make copies of all PDF files in every sub folder of a folder
- Removing leading zeros in filenames
- Compressing files of multiple folders into ZIP

### The shutil Modle (Shell Utilities)
Let you copy, move, rename, and delete files in your Python programs.

`shutil.copy(source, destination)` copy a single files to destination
- Source and destination can be string or Path objects
- Returns string or Path Object of the copied file

```py
>>> import shutil, os
>>> from pathlib import Path
>>> p = Path.home()
>>> shutil.copy(p / 'spam.txt', p / 'some_folder') # use original name
'C:\\Users\\Al\\some_folder\\spam.txt'
>>> shutil.copy(p / 'eggs.txt', p / 'some_folder/eggs2.txt') # use new name
WindowsPath('C:/Users/Al/some_folder/eggs2.txt')
```


`shutil.copytree(source, destination)` will copy the folder at the path source, along with all of its files and subfolders, to the folder at the path destination.
- Source and destination parameter are both strings
- Returns string of the path of the copied folder
