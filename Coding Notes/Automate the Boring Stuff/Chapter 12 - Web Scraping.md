
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
- `iter_content()`returns "chunks" of the content on each iteration via the loop. 
- pass a number as the number of byte in chunk size to `iter_content()`

---
### Parsing HTML the bs4 (Beautiful Soup 4) Module
Beautiful Soup is a module for extracting information from an HTML page.

Install bs4:
```sh
pip install --user beautifulsoup4
```

##### Creating a BeautifulSoup Object from HTML
You can use HTML web page from internet or locally stored HTML file.

Use `requests.get()` to download web page:
```py
>>> import requests, bs4
>>> res = requests.get('https://nostarch.com')
>>> res.raise_for_status()
>>> noStarchSoup = bs4.BeautifulSoup(res.text, 'html.parser')
>>> type(noStarchSoup)
<class 'bs4.BeautifulSoup'>
```

Load HTML file from your drive:
```py
>>> exampleFile = open('example.html')
>>> exampleSoup = bs4.BeautifulSoup(exampleFile, 'html.parser')
>>> type(exampleSoup)
<class 'bs4.BeautifulSoup'>
```

`html.parser` comes with Python, but you can use the faster `lxml` parser if you have it.
```sh
pip install --user lxml
```

##### Finding an Element with `select()` Method
```py
soup.select('div') # All elements named <div>
soup.select('#author') # The element with an id attribute of author
soup.select('.notice') # All elements that use a CSS class attribute named notice
soup.select('div span') # All elements named <span> that are within <div>
soup.select('div > span') # All elements named <span> that directly within
						  # <div>, with no other element in between
soup.select('input[name]') # All elements named <input> that have a name attr
soup.select('input[type="button"]') # All elements named <input> that have an
									# attribute named type with value button
```

E.g. `soup.select('p #author')` will match any element that has an id attribute of author, as long as it is also inside a `<p>` element.

- `select()` method returns a list of Tag objects. The list will contain one Tag object for every match in BeautifulSoup object's HTML.
- Tag values can be passed to the `str()` function to show the HTML tags they represent.
```py
>>> import bs4
>>> exampleFile = open('example.html')
>>> exampleSoup = bs4.BeautifulSoup(exampleFile.read(), 'html.parser')
>>> elems = exampleSoup.select('#author')
>>> type(elems) # elems is a list of Tag objects.
<class 'list'>
>>> len(elems)
1
>>> type(elems[0])
<class 'bs4.element.Tag'>
>>> str(elems[0]) # The Tag object as a string.
'<span id="author">Al Sweigart</span>'
>>> elems[0].getText()
'Al Sweigart'
>>> elems[0].attrs
{'id': 'author'}
```

To pull all the `<p>` elements from the Beautiful Soup object:
```py
>>> pElems = exampleSoup.select('p')
>>> str(pElems[0])
'<p>Download my <strong>Python</strong> book from <a href="https://
inventwithpython.com">my website</a>.</p>'
>>> pElems[0].getText()
'Download my Python book from my website.'
>>> str(pElems[1])
'<p class="slogan">Learn Python the easy way!</p>'
>>> pElems[1].getText()
'Learn Python the easy way!'
>>> str(pElems[2])
'<p>By <span id="author">Al Sweigart</span></p>'
>>> pElems[2].getText()
'By Al Sweigart'
```

##### Getting Data from an Element's Attributes
Use `get()` method for Tag objects to access attribute values from an element.
```py
>>> import bs4
>>> soup = bs4.BeautifulSoup(open('example.html'), 'html.parser')
>>> spanElem = soup.select('span')[0]
>>> str(spanElem)
'<span id="author">Al Sweigart</span>'
>>> spanElem.get('id')  # get the id
'author'
>>> spanElem.get('some_nonexistent_addr') == None
True
>>> spanElem.attrs
{'id': 'author'}
```