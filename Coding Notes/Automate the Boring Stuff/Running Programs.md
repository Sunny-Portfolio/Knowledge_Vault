### Running programs with arguments

##### Run programs from terminal
When entering a command in terminal, the terminal checks for a program with that name in the current folder. If it does't find it, it will check the folders listed in the PATH environment variable.
To check on Windows: `echo %PATH%`
To check on mac/Linus: `echo $PATH`

To run Python programs: `python helloworld.py` or `python3 hello.py`

##### Run Python Program on macOS
You can create a shell script to run y