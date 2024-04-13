### Ch2 Flow Control

`import sys`  // required by sys.exit()
`sys.exit()`  // cause program to terminate or exit before last instruction

`break`       // break out of loop
`continue`    // skip to next iteration

`import random`
`random.randint()`

### Ch3 Functions

`None`    // value of null in Python
print function returns None in Python
Any function that has no return statement returns None

`print('Hello', end="")`  // end keyword  
`print('cats', 'dogs', 'mice', sep=',')`  // sep keyword

#### Call stack
----------
When a program calls a function, it creates a frame object on the top of the
call stack. Frame objects store the line number of the original function call so
python knows where to return.
When function returns, Python removes a frame object from the top of the stack,
and move execution to the line number stored in it.

If you need to modify a global variable inside a function
def spam():
    global eggs     // use global statement to declare eggs as global var
    eggs = 'spam'

import time
time.sleep(o.1)     // pause for 1/10 sec

Ch 4 Lists
==========
you can add item to the list by doing this:
catname += 'Cracker'
catname.append('Cracker')   // modified in place
catname.insert(2, 'Meow')   // modified in place

To iterate via a list over it's indexes, use this trick
for i in range(len(dogs))
    print('Dog name is: ' + dogs[i])

without index, it would be the typical
for dog in dogs
    print(dog)


Multiple assignment trick (tuple unpacking):
-----------
>>> cat = ['fat', 'gray', 'loud']
>>> size = cat[0]
>>> color = cat[1]
>>> disposition = cat[2]

# Tuple unpacking for the above statements
>>> cat = ['fat', 'gray', 'loud']
>>> size, color, disposition = cat

enumerate() function
--------------------
# Can be used instead of range(len(someList)) in for loop
>>> supplies = ['pens', 'staplers', 'flamethrowers', 'binders']
>>> for index, item in enumerate(supplies):
... print('Index ' + str(index) + ' in supplies is: ' + item)


Random with List
----------------
# random.choice()
>>> import random
>>> pets = ['Dog', 'Cat', 'Moose']
>>> random.choice(pets)

# random.shuffle() reorder the list in place (not returning new list)
>>> import random
>>> people = ['Alice', 'Bob', 'Carol', 'David']
>>> random.shuffle(people)
>>> people
['Carol', 'David', 'Alice', 'Bob']


String vs List:
Both are similar but string is immutable and list is mutable.

Tuple vs List:
Both are similar, but tuple immutable, tuple use () instead of []

You can cast tuple to list and vise versa, like str(4) or int(1.2)
>>> tuple(['cat', 'dog', 5])
('cat', 'dog', 5)
>>> list(('cat', 'dog', 5))
['cat', 'dog', 5]
>>> list('hello')
['h', 'e', 'l', 'l', 'o']


id() - returns a numeric memory address of the value
>>> id('Howdy') # The returned number will be different on your machine.
44491136

The copy module's copy() and deepcopy():
>>> import copy
>>> spam = ['A', 'B', 'C', 'D']
>>> cheese = copy.copy(spam)    # duplicate copy of a mutalbe collection
If it is a list of list, then use copy.deepcopy()


Ch5 Dictionary
==============
key(), value(), items()
key(), value(), don't return true list. They return dict_values

>>> spam = {'color': 'red', 'age': 42}
>>> for v in spam.values():
... print(v)

# items() returns tuples of key and value
>>> for i in spam.items():
... print(i)
('color', 'red')
('age', 42)


get() - used to get item with a defaul fallback value if key not found
str(picnicItems.get('cups', 0))

setdefault() - set a value for a key if that key is not available.
if 'color' not in spam:
    spam['color'] = 'black'

>>> spam.setdefault('color', 'black')   # same as the above 2 lines


Pretty Printing  - access to pprint() and pformat() that pretty print dict
---------------
import pprint
pprint.pprint(count)

# These two are the same thing
pprint.pprint(someDictionaryValue)
print(pprint.pformat(someDictionaryValue))



Ch6 - Manipulating Strings
==========================
Raw Strings:
>>> print(r'That is Carol\'s cat.')
The r marks that the string is a raw strings and ignores all escape characters

Multiline Comments:
""" this is 
multiline
comment"""

Use string interpolation %s for string concatenation
>>> name = 'Al'
>>> age = 4000
>>> 'My name is %s. I am %s years old.' % (name, age)

Python 3.6+ can use f-strings. This seems more intuitive.
>>> name = 'Al'
>>> age = 4000
>>> f'My name is {name}. Next year I will be {age + 1}.'


join() and split() methods
>>> ', '.join(['cats', 'rats', 'bats'])
'cats, rats, bats'

>>> 'My name is Simon'.split()
['My', 'name', 'is', 'Simon']


Splitting with partition() method
>>> 'Hello, world!'.partition('o')
('Hell', 'o', ', world!')

If separator string not found, 1st string is whole string, 2nd 3rd empty

Assign 3 return strings:
>>> before, sep, after = 'Hello, world!'.partition(' ')


Justifying string with rjust(), ljust(), and center() methods
>>> 'Hello'.rjust(10)   # hello is 5 spaces, so add 5 to left
'     Hello'

>>> 'Hello'.ljust(20, '-')  # add a fill character
'Hello---------------'

Useful to print stuff like this:
---PICNIC ITEMS--
sandwiches..    4
apples......   12
cups........    4
cookies..... 8000
-------PICNIC ITEMS-------
sandwiches..........     4
apples..............    12
cups................     4
cookies.............  8000


Use ord() and chr() functions to get Unicode code point
>>> ord('!')
33
>>> chr(65)
'A'


Copy and paste with pyperclip module:
pyperclip module has copy() and paste() functions that sends text to and from
computer's clipboard. Makes it easy to copy paste to email, word, etc.
Pyperclip module doesn't come with Python. It is 3rd party.
>>> import pyperclip
>>> pyperclip.copy('Hello, world!')
>>> pyperclip.paste()
'Hello, world!'













