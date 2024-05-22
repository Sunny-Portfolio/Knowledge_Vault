
| Tech       | Function                                                                                                                     |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------- |
| webbrowser | Comes with Python and opens a browser to a specific page.                                                                    |
| requests   | Downloads files and web pages from the internet.                                                                             |
| bs4        | Parses HTML, the format that web pages are written in.                                                                       |
| selenium   | Launches and controls a web browser. The selenium module is able to fill in forms and simulate mouse clicks in this browser. |

### Web Browser
To launch a new browser and load website:
```py
>>> import webbrowser
>>> webbrowser.open('https://google.com/')
```

You will need to know how to [run a program](Running%20Programs.md) on your OS's terminal.

##### Get command line arguments
`sys.argv` stores a list of the program's filename and command line arguments. If it contains more than just the filename, then the length is > 1.
```py
import webbrowser, sys
if len(sys.argv) > 1:
	# Get address from command line.
	address = ' '.join(sys.argv[1:]) # joins all argu to a string
else:
	# Get address from clipboard.
	address = pyperclip.paste()
webbrowser.open('https://www.google.com/maps/place/' + address)
```

### Downloading Files from the Web with requests Module
Allows you to easily download files from the web without having to worry about complicated issues such as network errors, connection problems, and data compression.

Does not come with Python, install with `pip install --user requests`. Refer to [Install 3rd Party Modules](Install%203rd%20Party%20Modules.md).

##### Download web page with requests.get()
This function takes a URL string to download:
```py
>>> import requests
>>> res = requests.get('https://automatetheboringstuff.com/files/rj.txt')
>>> type(res) # returns a Response object
<class 'requests.models.Response'>
>>> res.status_code == requests.codes.ok # check status code
True
>>> len(res.text)
178981
>>> print(res.text[:250])
```
Here is a [list](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) of HTTP status codes. 200 is "OK". 404 is "Not Found".

##### Checking for Errors (Response Object)
Simpler way than checking Response object status code is to call `raise_for_status()`. You can wrap with `try` and `except` to handle the error.
```py
import requests
res = requests.get('https://google.com/page_that_does_not_exist')
try:
	res.raise_for_status()
except Exception as exc:
	print('There was a problem: %s' % (exc))
```

##### Saving Downloaded Files
You can save web page to a file with standard `open()` function and `write()` method, but you need to write binary data instead of text to maintain the *Unicode encoding* of the text.
```py
>>> import requests
>>> res = requests.get('https://automatetheboringstuff.com/files/rj.txt')
>>> res.raise_for_status()
>>> playFile = open('RomeoAndJuliet.txt', 'wb')  # pass 'wb' to write binary
>>> for chunk in res.iter_content(100000):  # pass 10000 as chunk size in bytes
		playFile.write(chunk)
		
100000
78981
>>> playFile.close()
```
`iter_content()`returns "chunks" of the content on each iteration via the loop. 
pass a number as the number of byte in chunk 