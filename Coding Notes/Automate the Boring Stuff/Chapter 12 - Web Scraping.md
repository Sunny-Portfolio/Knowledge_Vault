
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
`sys.argv` stores a list of the program's filename and command line arguments. If it has more than just the filename, 
```py
import webbrowser, sys
if len(sys.argv) > 1:
	# Get address from command line.
	address = ' '.join(sys.argv[1:])
```
