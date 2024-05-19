### Running programs with arguments

##### Run programs from terminal
When entering a command in terminal, the terminal checks for a program with that name in the current folder. If it does't find it, it will check the folders listed in the PATH environment variable.
To check on Windows: `echo %PATH%`
To check on mac/Linus: `echo $PATH`

To run Python programs: `python helloworld.py` or `python3 hello.py`

##### Run Python Program on macOS
You can create a shell script to run Python scripts:
```sh
#!/usr/bin/env bash
python3 /path/to/your/pythonScript.py
```
1. Save this as `runPyProg.command`
2. Make it executable `chmod u+x runPyProg.command`
3. Done. You can use Spotlight to run your Python script

##### Run Python Programs with Assertions Disabled
This will run an optimized version of your program that skips as
```sh
python3 -0 test.py
```


