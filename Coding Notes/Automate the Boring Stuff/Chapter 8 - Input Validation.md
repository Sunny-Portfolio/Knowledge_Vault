Use Pyinputplus for validation of user input.
It is not part of python standard library and must be imported and installed
It ensures that user input the intended data

Some pyinputplus functions:
```py
inputStr()
inputNum()
inputChoice()   #user enter one of the provided choices
inputMenu()     #similar to choice but with numbered/lettered options
inputDatetime()
inputYesNo()    # yes / no response
inputBool()
inputEmail()
inputFilepath() # check input is a path and optionally check if exist
inputPassword()
```

inputNum(), inputInt(), inputFloat() functions also have min, max, greaterThan, lessThan keyword arguments
```py
>>> import pyinputplus as pyip
>>> response = pyip.inputNum('Enter num: ', min=4)
Enter num:3
Input must be at minimum 4.
Enter num:4
>>> response
4
```

##### Allow blank keyword argument
```py
>>> response = pyip.inputNum(blank=True)
(blank input entered here)
>>> response
''
```

##### Limit the attempts of input with keywords limit / timeout
```py
>>> import pyinputplus as pyip
>>> response = pyip.inputNum(limit=2)
blah
'blah' is not a number.
Enter num: number
'number' is not a number.
Traceback (most recent call last):
--snip--
pyinputplus.RetryLimitException
```

```py
>>> response = pyip.inputNum(timeout=10)
42 (entered after 10 seconds of waiting)
Traceback (most recent call last):
--snip--
pyinputplus.TimeoutException
```

Use the two keywords argument but also passing a default key argument instead of raising exception:
```py
>>> response = pyip.inputNum(limit=2, default='N/A')
hello
'hello' is not a number.
world
'world' is not a number.
>>> response
'N/A'
```

##### Use allowRegexes and blockRegexes
```py
>>> import pyinputplus as pyip
>>> response = pyip.inputNum(allowRegexes=[r'(I|V|X|L|C|D|M)+', r'zero'])
XLII
```

```py
>>> import pyinputplus as pyip
>>> response = pyip.inputNum(blockRegexes=[r'[02468]$'])
42
This response is invalid.
```

If specify both allowRegexes and blockRegexes, the allow list overrides the block list.

##### Use inputCustom() to define your own validation
```py
>>> response = pyip.inputCustom(addsUpToTen)
Useful when it is difficult to write regex to validate input, such as add to 10
```


