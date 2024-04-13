- Windows uses backslash \ as dir separator
- Linux/Mac uses forward slash / as dir separator

### On Mac OS
```py
>>> from pathlib import Path
>>> Path('spam', 'bacon', 'eggs')
PosixPath('spam/bacon/eggs')  # Linux version
WindowsPath('spam/bacon/eggs')  # Windows version
```

```py
>>> str(Path('spam', 'bacon', 'eggs'))
'spam\\bacon\\eggs' # Windows shows this 
'spam\bacon\eggs'   # Linux/mac shows this
```

##### Join filenames to folder name
```py
>>> myFiles = ['accounts.txt', 'details.csv', 'invite.docx']
>>> for filename in myFiles:
        print(Path(r'C:\Users\Al', filename))
C:\Users\Al\accounts.txt
C:\Users\Al\details.csv
C:\Users\Al\invite.docx
```


### Use / operator to join paths
Important!! one of the first 2 values must be a Path obj

```py
>>> from pathlib import Path
>>> Path('spam') / 'bacon' / 'eggs'
WindowsPath('spam/bacon/eggs')

>>> Path('spam') / Path('bacon/eggs')
WindowsPath('spam/bacon/eggs')

>>> Path('spam') / Path('bacon', 'eggs')
WindowsPath('spam/bacon/eggs')

>>> homeFolder = Path('C:/Users/Al')
>>> subFolder = Path('spam')
>>> homeFolder / subFolder
WindowsPath('C:/Users/Al/spam')
>>> str(homeFolder / subFolder)
'C:\\Users\\Al\\spam'
```


##### Path functions
```py
Path.cwd()      # current working dir
Path.home()     # home dir
Path.is_absolute()  # T/F if abosolute path
```

##### Create new folder with Path
```py
>>> from pathlib import Path
>>> Path(r'C:\Users\Al\spam').mkdir()
```

##### get absolute path with relative path
concat absolute path with cwd
```py
>>> Path.cwd() / Path('my/relative/path')
```
If your path is not cwd, then just add whatever path and concat them

### Use OS library for dir
##### Create new folder with os
```py
>>> import os
>>> os.makedirs('C:\\delicious\\walnut\\waffles')
```

```py
>>> os.path.abspath('.')
'C:\\Users\\Al\\AppData\\Local\\Programs\\Python\\Python37'
>>> os.path.abspath('.\\Scripts')
'C:\\Users\\Al\\AppData\\Local\\Programs\\Python\\Python37\\Scripts'
>>> os.path.isabs('.')
False
>>> os.path.isabs(os.path.abspath('.'))
True
```

##### Get parts of a file path
```py
>>> p = Path('C:/Users/Al/spam.txt')
>>> p.anchor
'C:\\'
>>> p.parent # This is a Path object, not a string.
WindowsPath('C:/Users/Al')
>>> p.name
'spam.txt'
>>> p.stem
'spam'
>>> p.suffix
'.txt'
>>> p.drive
'C:'
```


##### The parents att.
```py
>>> Path.cwd()
WindowsPath('C:/Users/Al/AppData/Local/Programs/Python/Python37')
>>> Path.cwd().parents[0]
WindowsPath('C:/Users/Al/AppData/Local/Programs/Python')
>>> Path.cwd().parents[1]
WindowsPath('C:/Users/Al/AppData/Local/Programs')
>>> Path.cwd().parents[2]
WindowsPath('C:/Users/Al/AppData/Local')
>>> Path.cwd().parents[3]
WindowsPath('C:/Users/Al/AppData')
>>> Path.cwd().parents[4]
WindowsPath('C:/Users/Al')
>>> Path.cwd().parents[5]
WindowsPath('C:/Users')
>>> Path.cwd().parents[6]
WindowsPath('C:/')
```
