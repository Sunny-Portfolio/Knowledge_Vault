##### Example things to do with Python:
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
- Source and destination parameter are both strings (or Path objects?)
- Returns string of the path of the copied folder (or Path objects?)
```py
>>> import shutil, os
>>> from pathlib import Path
>>> p = Path.home()
>>> shutil.copytree(p / 'spam', p / 'spam_backup')
WindowsPath('C:/Users/Al/spam_backup')
```

`shutil.move(source, destination)` will move the file or folder at the path source to the path destination and will return a string of the absolute path of the new location.
```py
>>> import shutil
>>> shutil.move('C:\\bacon.txt', 'C:\\eggs')
'C:\\eggs\\bacon.txt'
>>> shutil.move('C:\\bacon.txt', 'C:\\eggs')  # if egg folder DNE,renamed eggs
'C:\\eggs'
```

### Permanently Deleting Files and Folders
- `os.unlink(path)` will delete the file at path.
- `os.rmdir(path)` will delete the folder at path.
	- This folder must be empty of any files or folders.
- `shutil.rmtree(path)` will remove the folder at path, and all files and folders it contains will also be deleted.
	- irreversibly delete files and folders
	- Better way to use `send2trash` module

The following will delete `*.rxt` files. (But safer to call with print first)
Safer to to print filenames before delete operation:
```py
import os
from pathlib import Path
for filename in Path.home().glob('*.rxt'):
#os.unlink(filename)
print(filename)
```

##### send2trash Module
Move files and folders to recycle bin instead of permanently deleting them. But it cannot pull files out of it.

How to install:
```py
pip install --user send2trash
```

Example:
```py
>>> import send2trash
>>> baconFile = open('bacon.txt', 'a') # creates the file
>>> baconFile.write('Bacon is not a vegetable.')
25
>>> baconFile.close()
>>> send2trash.send2trash('bacon.txt')
```

### Walking a Directory Tree
Use `os.walk()` in for loop to walk a directory tree.
import os

for folderName, subfolders, filenames in os.walk('C:\\delicious'):

print('The current folder is ' + folderName)

for subfolder in subfolders:

print('SUBFOLDER OF ' + folderName + ': ' + subfolder)

for filename in filenames:

print('FILE INSIDE ' + folderName + ': '+ filename)

print('')