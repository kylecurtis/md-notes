Let us assume for a moment that we are tasked with doing a penetration test for a client with a locked-down user environment. While investigating our options for our `Assume Breach` test, i.e., a test assuming that we have already successfully compromised a regular user account and machine through phishing, we discover that we can run Python scripts. We can produce a list of potential user accounts, and we would also like to have a `target specific` list of potential passwords. We notice that the client's website contains many `buzzwords`, and we wonder if some users used variations of product names as their passwords. For this, we need to write a simple script that can produce a list of a website's most frequently occurring words. Since the client wants to get a copy, we will try our best to make the script easy to read and maintain.

Before we get ahead of ourselves, we need to carve out the essential building blocks. For this, let us talk about math. Math and programming have some things in common: both use variables and constants a fair bit, and both have functions. In Python, a variable is our way of storing a value of some sort in memory. For example, a number, some text, or the bytes of an image. Like in math, variables have a name that we make up, but the names should be descriptive in Python. Below are some examples:

#### A Few Simple Variables

```python
advice = "Don't panic"
ultimate_answer = 42
potential_question = 6 * 7
confident = True
something_false = False
problems = None
# Oh, and by the way, this is a comment. We can tell by the leading # sign.
```

#### Strings

The first variable, `advice`, is a `string`. Strings in Python can be specified using both `"double quotes"` and `'single quotes'`. When typing out strings that contain either symbol as a natural part of the string itself, e.g., `don't lie`, it is a good idea to use the `other` kind of quotes. Writing `"don't lie"` works just fine. However, using single quotes would throw an error.

#### Integers

Following the `advice` variable comes two numbers, or `integers`, the first of which is a number. The second variable, `potential_question`, is also a number but not until `runtime`. During runtime, the equation `6 * 7` is evaluated to `42`, which is then stored as the variable.

#### Booleans

Following the number variables come two `boolean` variables, `confident` and `something_false`. A boolean value is a truth value and can be either `True` or `False`. These will come in handy later. Right after comes the variable `problems`, which is set to `None`. [None](https://realpython.com/null-in-python/#:~:text=Python%20uses%20the%20keyword%20None,and%20a%20first%2Dclass%20citizen!) is a special "nothingness" of a value similar to `null` in other languages. The usefulness of this value is, among other things, that it allows us to `define variables` in the code but not give them a concrete value just yet. It also allows us to create a more meaningful program flow and decide to pass along `either` some data `or` `None`, e.g., in case of errors. Moreover, it allows us to return it as a value if "none of something" was found. This also enhances the program flow and readability.

#### Comments

Lastly, we see a comment. Comments work the same way in Python as they do in all other languages: they are ignored when the program runs and are only for the developers' eyes. It can sometimes be advisible to use comments to remember what a piece of code does or explain some oddity. However, it is strongly recommended to write clean and simple code that will not need further explanation other than the code itself. This is not always the easiest way to get started, but we will try to aim for this later.

<br>

---

<br>

## Combining Variables

Let us go through a few examples to see how all these variables can also be combined. Later on, whether for our projects or specific tasks, we will want to output variables (and thus also their contents) together. Therefore, let us first briefly go through some basic math operations with Python.

#### Basic Math Operations

```python
>>> 10 + 10		# Addition
20
>>> 20 - 10		# Subtraction
10
>>> 5 * 5		# Multiplication
25
>>> 10 / 5		# Division
2
```

For all of these values we can define variables to store them. As for the name itself, we can name them as we please, however with a few exceptions e.g. they must begin with a letter or `_`.

#### Saving Values to Variables

```python
>>> add = 10 + 10
>>> sub = 20 - 10
>>> multi = 5 * 5
>>> div = 10 / 5
>>>
>>> print(add, sub, multi, div)
20 10 25 2
```

This also allows us to work with the values stored in the individual variables.

#### Working with Variables

```python
...SNIP...
>>> print(add, sub, multi, div)
20 10 25 2
>>> result = (add * sub) - (multi * div)		# (20 * 10) - (25 * 2)
>>> print('Result: ', result)
Result:  150
```

Another handy feature of the Python interpreter is that the IDLE assigns the latest expression to the variable `_`. This allows us to continue working with the last value.

```python
>>> 38 + 4
42
>>> 50 - _		# 50 - 42
8
```

Note however that this is true _only_ for IDLE. In regular Python code that is run from `.py` files e.g. from the command line or in an Integrated Development Environment, `_` is simply just a variable. It is often used as a placeholder for values we do not care about, for example if a function returns two values, but only one of them is important to us, for example `x_coord, _ = get_position_of_birb()`. This is to show other developers, and ourselves a few months into the future, that the value returned, e.g. the y-coordinate from the previous example, is not needed.

<br>

---

<br>

## Coding Style

In Python, variable names follow the [snake_case](https://en.wikipedia.org/wiki/Snake_case) naming convention. This means that variable names should be all lower case initially, and an underscore should separate any potential need for multiple words in the name. While ignoring these naming conventions will not cause any issues for the script - Python could care less about what we call our things - other Python developers may get thrown off if they expect one set of rules but face others.

The main point here is that our code should be easy to follow and read. Every programmer has their style and preferences when it comes to writing code. There are even several style guides for Python, such as [PEP8](https://www.python.org/dev/peps/pep-0008/#type-variable-names), which describes certain types of variable or function definitions. Having a style guide is very important when we want someone to read the code we write. We usually write code so that someone can use it, benefit from it and possibly work on it or learn something new from it. Without a style guide, debugging, improving, or extending becomes immensely difficult. Of course, there are many other things besides the style guide that we as professional programmers need to pay attention to, such as code architecture, general principles for code quality, etc.