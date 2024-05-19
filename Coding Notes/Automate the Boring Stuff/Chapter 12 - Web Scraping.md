
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

### Running programs with arguments

##### Run programs from terminal
When entering a command in terminal, the terminal checks for a program with that name in the current folder. If it does't find it, it will check the folders listed in the PATH environment variable.
To check on Windows: `echo %PATH%`
To check 

