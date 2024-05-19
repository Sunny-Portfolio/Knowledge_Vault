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
Assertions is a sanity check to make sure your code isn't doing something obviously wrong. If fails, then AssertionError exception is raised.
```py
>>> ages = [26, 57, 92, 54, 22, 15, 17, 80, 47, 73]
>>> ages.reverse()
>>> ages
[73, 47, 80, 17, 15, 22, 54, 92, 57, 26]
>>> assert ages[0] <= ages[-1] # Assert that the first age is <= the last age.
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
AssertionError
```

- Unlike exceptions, your code should not handle assert statements with try and except; if an assert fails, your program should crash.
- Assertions are for programmer errors, not user errors.
	- A finished program should never have assertion errors.
- Run a Python script with `python -O myscript.py` instead of `python myscript.py` will skip assert statements.

### Logging
To enable Python's logging mode:
```py
import logging
logging.basicConfig(level=logging.DEBUG, format='%(asctime)s - %(levelname)s - %(message)s')
logging.debug('Start of program')

def factorial(n):
	logging.debug('Start of factorial(%s%%)' % (n))
	total = 1
	for i in range(n + 1):
		total *= i
		logging.debug('i is ' + str(i) + ', total is ' + str(total))
	logging.debug('End of factorial(%s%%)' % (n))
	return total
print(factorial(5))
logging.debug('End of program')
```
When Python logs an event, it creates a *LogRecord object* that hold info of the event. The logging module’s `basicConfig()` function lets you specify what details about the *LogRecord object* you want to see and how you want those details displayed.
```py
2019-05-23 16:20:12,664 - DEBUG - Start of program
2019-05-23 16:20:12,664 - DEBUG - Start of factorial(5)
2019-05-23 16:20:12,665 - DEBUG - i is 0, total is 0
2019-05-23 16:20:12,668 - DEBUG - i is 1, total is 0
2019-05-23 16:20:12,670 - DEBUG - i is 2, total is 0
2019-05-23 16:20:12,673 - DEBUG - i is 3, total is 0
2019-05-23 16:20:12,675 - DEBUG - i is 4, total is 0
2019-05-23 16:20:12,678 - DEBUG - i is 5, total is 0
2019-05-23 16:20:12,680 - DEBUG - End of factorial(5)
0
2019-05-23 16:20:12,684 - DEBUG - End of program
```

##### Logging vs Print for debugging
**print()**
- time consuming to remove all the print statements
- may accidentally remove print() that you actually need
**logging()**
- you can simply disable all logs with `logging.disable(logging.CRITICAL)`

##### Logging Levels
Logging levels provide a way to categorize your log messages by importance. Allowing you to change what priority of logging message you want to see in the log.

There are five logging levels:

| **Level** | **Logging function** | **Description**                                                  |
| --------- | -------------------- | ---------------------------------------------------------------- |
| DEBUG     | logging.debug()      | Lowest level. Used for small details that you care about.        |
| INFO      | logging.info()       | Used to record general events info.                              |
| WARNING   | logging.warning()    | Used to indicate a potential problem.                            |
| ERROR     | logging.error()      | Used to record error that cause program to fail doing something. |
| CRITICAL  | logging.critical()   | Highest level. Used to indicate fatal error.                     |
Setting `basicConfig()` to `logging.ERROR` will show only ERROR and CRITICAL messages.

##### Disabling Logging
`logging.disable(logging.WARNING)` will suppress all log messages at that level or lower.
```py
>>> import logging
>>> logging.basicConfig(level=logging.INFO, format=' %(asctime)s - %(levelname)s - %(message)s')
>>> logging.critical('Critical error! Critical error!')
2019-05-22 11:10:48,054 - CRITICAL - Critical error! Critical error!
>>> logging.disable(logging.CRITICAL)  # disable all logging after this
>>> logging.critical('Critical error! Critical error!')
>>> logging.error('Error! Error!')
```

##### Logging to file
You can write the log to a text file:
```py
import logging
logging.basicConfig(filename='myProgramLog.txt', level=logging.DEBUG, format='
%(asctime)s - %(levelname)s - %(message)s')
```

### Debugger
##### Continue
- execute normally until it terminates or reaches a breakpoint.
##### Step In
- execute next line of code and then pause again.
- If next line is a function call, debugger will *step into* the function to first line of function.
##### Step Over
- execute next line of code similar to *step in*.
- If next line is a function call, *step over* to execute function at normal speed and pause when function returns.
##### Step Out
- execute lines of code at full speed until it returns from the current function.
- Click to *step out* of the current function call.
##### Stop
- Click if you want to stop debugging entirely.

### Breakpoint
You can set a breakpoint on a specific line of code to force the debugger to pause.
E.g. You have a loop that runs a 1000 times and you want to pause when it is half done.
