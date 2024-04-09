There are many ways to execute a piece of Python code. Two of the most frequently used methods are running the code from a `.py` file and running it directly inside the Python [IDLE](https://docs.python.org/3/library/idle.html), Integrated Development and Learning Environment. In this section, we will look at how to run code both ways. The file-based way is handy when developing an actual script and the IDLE way is very useful for quickly testing something small. We will start with the file-based approach.

<br>

---

<br>

## Python3

Let's start with a widespread, first piece of code that prints out "Hello world" to the terminal or screen. In Python, it looks like this:

#### welcome.py

```python
print("Hello Academy!")
```

If we run this script, the string `"Hello Academy!"` will be printed to the terminal. To try it out, we open a text editor, type in the above, and save the file as `welcome.py`. Next, we try running it by executing `python3 welcome.py`.

Executing Python Code

```bash
user@htb[/htb]$ vim welcome.py
user@htb[/htb]$ python3 welcome.py

Hello Academy!
```

<br>

---

<br>

## IDLE

We can utilize `IDLE`, Python's own integrated development environment, directly in our terminal for quicker prototyping. We launch this by executing the Python binary without any arguments. Within this, we can have it evaluate simple math equations, e.g., `4 + 2`, or store and use variables. When evaluating an expression, the result will be printed on the line below if a result is returned. However, if the expression is stored as a variable, nothing will be printed as nothing is returned (it is all contained in the variable). We can also import libraries and define functions and classes directly in the IDLE for usage in the same session. We will dive deeper into libraries, functions, and classes later on. To exit the IDLE again, we type `exit(0)`. The number `0` is the [return code](https://en.wikipedia.org/wiki/Exit_status) of the Python process, where 0 means all is OK and a number different from 0 indicates an error. Consider this example of how to use IDLE:

#### Python IDLE

```bash
user@htb[/htb]$ python3

Python 3.9.0 (default, Oct 27 2020, 14:15:17) 
[Clang 12.0.0 (clang-1200.0.32.21)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

```python
>>> 4 + 3
7
>>> foo = 3 * 5
>>> foo
15
>>> foo + 4
19
>>> print('Hello Academy!')
Hello Academy!
>>> exit(0)
```

Python executes the code from top to bottom. This is important to keep in mind when writing Python scripts because Python has no clue what is further down in the script until it gets to it. If we were to print a variable instead of a literal value, it must be defined before referencing. For example:

#### Hello Again, Academy

```python
>>> greeting = 'Hello again, Academy'
>>> print(greeting)
Hello again, Academy
```

However, we can print the output of not only one variable but of several in different variations.

#### Printing Multiple Variables

```python
>>> a = 'HTB'
>>> b = 'Academy'
>>> print(a, b)
HTB Academy
```

<br>

---

<br>

## Shebang

Another method is based on adding the [shebang](https://en.wikipedia.org/wiki/Shebang_%28Unix%29#Portability) (`#!/usr/bin/env python3`) in the first line of a Python script. On Unix-based operating systems, marking this with a pound sign and an exclamation mark causes the following command to be executed along with all of the specified arguments when the program is called. We can give the Python script execution rights and execute it directly without entering `python` at the beginning on the command line. The file name is then passed as an argument.

#### welcome.py

```python
#!/usr/bin/env python3

print("Hello Academy!")
```

#### Shebang Execution

```bash
user@htb[/htb]$ chmod +x welcome.py
user@htb[/htb]$ ./welcome.py

Hello Academy!
```