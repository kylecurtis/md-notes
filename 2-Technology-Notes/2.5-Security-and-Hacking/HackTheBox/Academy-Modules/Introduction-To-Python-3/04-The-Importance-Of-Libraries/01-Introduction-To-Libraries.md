We have discussed how to create classes and functions, functions within classes, and other simple concepts. All of this has been inside one Python file, also known as `a module`, but it would be great if we could share the code inside this module with other people or reuse it in other projects. It would also be great to reuse code that other people have made for us, for example, code that lets us communicate with web servers or even something as simple as getting the current date. Enter libraries.

A `library` in programming is in many ways similar to a library in real life. It is a collection of knowledge that we can borrow in our projects without reinventing the wheel. Once we `import` a library, we can use everything inside it, including functions and classes. Some libraries ship along with Python, for example, `datetime`, which lets us get an object representing the current, local date, and time.

Let us see what classes and functions the library `datetime` contains. For that, we will use the built-in function called [dir()](https://docs.python.org/3/library/functions.html#dir).

#### Dir(datetime)

```python
>>> import datetime
>>> dir(datetime)
['MAXYEAR', 'MINYEAR', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'date', 'datetime', 'datetime_CAPI', 'sys', 'time', 'timedelta', 'timezone', 'tzinfo']
```

#### The datetime Library

```python
import datetime

now = datetime.datetime.now()
print(now)  # Prints: 2021-03-11 17:03:48.937590
```

As we see, we have to call `datetime.datetime.now()` to get the current timestamp. We import the library, or `module`, `datetime`, which then becomes available to reference by name. This module is also called `datetime`, which contains a `now()` function. So to get to the `now()` function, we first have to reference the module, then the class, and finally the function, all "chained together" to speak with dots.

This may become cumbersome and clutter the code, so let us look at alternative ways of importing:

#### Importing a Class From a Library

```python
from datetime import datetime

print(datetime.now())
```

#### Giving It a New Name

```python
from datetime import datetime as dt

print(dt.now())
```

The above example contains two newlines between the import statement and the code. This is because the PEP-8 style guide, Python's guidelines for "correct" Python, urges developers to add two new lines between import statements and the actual code. It also suggests using the CapWords convention for class names but notes a separate style guide for built-in names. See [https://www.python.org/dev/peps/pep-0008/#class-names](https://www.python.org/dev/peps/pep-0008/#class-names) for more information. This is why classes such as `datetime` are in lowercase.

Next up, we will dive deeper into how to install and manage external libraries in Python.