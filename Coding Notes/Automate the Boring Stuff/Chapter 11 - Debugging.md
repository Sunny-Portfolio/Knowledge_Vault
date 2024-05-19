### Raising Exceptions
##### Raise keyword and Exception() function
```py
>>> raise Exception('This is the error message.')
Traceback (most recent call last):
File "<pyshell#191>", line 1, in <module>
raise Exception('This is the error message.')
Exception: This is the error message.
```
##### Use try except statement:
```py
for sym, w, h in (('*', 4, 4), ('O', 20, 5), ('x', 1, 3), ('ZZ', 3, 3)):
	try:
		boxPrint(sym, w, h)
	except Exception as err:
		print('An exception happened: ' + str(err))
```

##### Traceback
Traceback includes the error message, the line number of the line that caused the error, and the sequence of the function calls that led to the error. This sequence of calls is called the call stack. Here is an example of traceback output:
```py
Traceback (most recent call last):
  File "errorExample.py", line 7, in <module>
    spam()
  File "errorExample.py", line 2, in spam
    bacon()
  File "errorExample.py", line 5, in bacon
    raise Exception('This is the error message.')
Exception: This is the error message.
```

You can get the string of the traceback by calling `traceback.format_exc()`. You can also save it to a file:
```py
>>> import traceback
>>> try:
... raise Exception('This is the error message.')
except:
... errorFile = open('errorInfo.txt', 'w')
... errorFile.write(traceback.format_exc())
... errorFile.close()
... print('The traceback info was written to errorInfo.txt.')
```


### Assertions
Assertions is a sanity check to make sure your code isn't doing something obviously wrong.
