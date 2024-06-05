Now let us spice things up a little. This section will go over conditional statements - ifs and elses - and various types of loops. Below is an example of what an if/else `block` of code looks like, i.e., the amount of code that constitutes a particular technique and is visually grouped (typically indented at the same level).

#### A Simple Feature Switch

```python
happy = True

if happy:
    print("Happy and we know it!")
else:
    print("Not happy...")
```

A few things happened here already. Pay close attention to the indentation of the code. Python does not require how wide each indentation must be, as long as there is `consistency`. Some people prefer two spaces, others 4. Some people prefer a single tab character. We will continue to use four spaces going forward.

Besides indentations, two new keywords are used here: `if` and `else`. First, we define a variable which, for the sake of demonstration, is currently TRUE. Then we check `if` the variable `happy` is `True` (`if some_var` is easier to read but also shorthand for `if some_var == True`), and if it is `True`, then we print "Happy and we know it!" to the terminal. If `happy` is `not` `True`, i.e., it is `False`, then the `else` block is executed instead, and "Not happy..." is printed to the terminal.

Nevertheless, we also have to consider the situation that we want to bring in more than just two different options. The `elif` (else-if) expression means that we continue with this one if the previous condition is not met. Basically, `elif` is the shortened notation of nested `if` statements.

#### If-Elif-Else Statement

```python
happy = 2

if happy == 1:
    print("Happy and we know it!")
elif happy == 2:
    print("Excited about it!")
else:
    print("Not happy...")
```

This brings us to the first type of loop: the `while-loop`. Consider the below code:

#### The While-Loop

```python
counter = 0

while counter < 5:
    print(f'Hello #{counter}')
    counter = counter + 1
```

Before we dive into the code, it is essential to know how a while-loop works in the first place. A while-loop is a loop that will execute its content (the "block") as long as the defined condition is `True`. This means that `while True` will run forever, and `while False` will never run. By doing what we do in the example, we tell Python to run the contents of the while-loop for as long as the `counter` variable is below 5. Inside the while-loop, we must then remember to increase the `counter` by (at least) 1 every time we make an iteration or eventually, anyway. If we try to run the above example, `print` will be called five times and print the contents of the function.

Now, what are the contents of `print`? Let us quickly talk about formatted strings before continuing with loops. A format string is a string that lets us `populate the string` with values during runtime. A new formatting string was introduced with Python 3.6: the [f-string](https://realpython.com/python-f-strings/) (above example).

While a regular string could look something like `'Hello world'`, an f-string adds an `f` at the beginning: `f'Hello world'`. These particular two strings are of the same value. The benefit of the f-string, however, is that we can swap out parts of the strings with other values and variables by enclosing them in a pair of curly braces, like this:

#### Format Strings

```python
equation = f'The meaning of life might be {6 * 7}.'  # -> The meaning of life might be 42.

me = 'Birb'
greeting = f'Hello {me}!'  # -> Hello Birb!
```

Now that we know that a while-loop is a loop that continues to execute `while` some condition is true, and we know that `f'Hello #{counter}'` will equal `Hello #` followed by the number of the iteration - starting at 0 - we are ready to try to execute the code!

#### While-Loop

Conditional Statements and Loops

```bash
user@htb[/htb]$ vim loop1.py
user@htb[/htb]$ python3 loop1.py

Hello #0
Hello #1
Hello #2
Hello #3
Hello #4
```

Once again: the loop checks if the counter, which is set to 0 initially, is below 5 - it is - and then prints "Hello #0" and sets the `counter` variable to the value of itself (0) + 1. Next iteration, it checks if `counter`, which is now 1, is less than 5 - it is - and then prints "Hello #1" and sets `counter` to the value of itself (1) + 1. On the 3rd iteration, `counter` is 2 (because we started at 0), and so forth.

In the next section, we will continue looking at loops, but this time a simpler type of loop and one we will be favoring over the other as much as possible.

<br>

---

<br>

## Loops and Lists

Recall from the previous section that a loop is a block of code that keeps iterating the contents until some condition is met. This section will look at one kind of loops often referred to as the "for-each loop". This is a loop that iterates over `each element` in some collection of elements and does something `for each` individual element. Consider the below line of code:

#### A List of Strings

```python
groceries = ['Walnuts', 'Grapes', 'Bird seeds']
```

This is a list of strings. The square brackets indicate a list, and the comma-separated values inside of it are strings. Similarly, `[]` is an empty list, and `[42]` is a list with just one element, the `int` value `42`. When pointing out values inside lists, Python numbers the elements in a list from 0 and upwards. This means that the above list has `three elements` and that `the first` element is at `index 0`. The second element is at index 1, and the third element is at index 2. Like so:

#### Value Indexes

```python
groceries = ['Walnuts', 'Grapes', 'Bird seeds']
# index:         0          1          2
```

We can also write lists the following way for easier readability (especially with much larger lists):

#### Alternative Syntax

```python
groceries = [
    'Walnuts',    # index 0
    'Grapes',     # index 1
    'Bird seeds'  # index 2
]
```

The last thing to mention about lists before we move on is how to retrieve an element from the list. Say we want to print the first element to the console. This is done by referencing the variable name of the list, e.g., `groceries` and which index is desired like so: `groceries[0]` to get the first element, `'Walnuts'`. The last element, `'Bird seeds'` would in this example then be `groceries[2]` because the value `'Bird seeds'` is located at index 2 in the list. Python can even count backward, so we could also have gotten the last element of the list - regardless of how many elements are in it - by asking for index -1: `groceries[-1]`. It works the same way we did with strings.

#### Strings Indexing

Strings can also be indexed. This is especially useful when we want to filter out certain parts of some output. We can think of each word as a list of letters with indexes. However, there is also the negative index, which allows us to start counting the string letters from the end. Let us take the following string as an example: `ABCDEF`

|**Negative Index**|**Index**|**Character**|
|---|---|---|
|`-6`|`0`|A|
|`-5`|`1`|B|
|`-4`|`2`|C|
|`-3`|`3`|D|
|`-2`|`4`|E|
|`-1`|`5`|F|

We use the index to tell Python which letter we want to output from it. In this example, we want to output the first and the last letter.

Code: python

```python
>>> var = "ABCDEF"
>>> print(var[0], var[1], var[2], var[3], var[4], var[5])
A B C D E F
>>> print(var[-1], var[-2], var[-3], var[-4], var[-5], var[-6])
F E D C B A
```

We can also work with these indexes to give us particular substrings.

#### Substrings

```python
>>> var = "ABCDEF"
>>> print(var[:2])	# Up to index 2
AB
>>> print(var[2:])	# Ignore everything up to index 2
CDEF
>>> print(var[2:4])	# Everything between index 2 and 4 ("2" is counted)
CD
>>> print(var[-2:])	# Up to negative index 2 (last two characters)
EF
```

<br>

---

<br>

## For-Each Loop

As already mentioned, Python allows us to loop over each element (or value) in a list. Consider the below piece of code where we at first have defined a list and then the loop.

#### The For-Each Loop

```python
groceries = ['Walnuts', 'Grapes', 'Bird seeds']

for food in groceries:
    print(f'I bought some {food} today.')
```

The for-each loop is structured this way: first the `for` keyword, then the variable name we choose, followed by the `in` keyword and a collection to iterate over. In this example, we told Python to run the code inside the block "for each element," where we then call the current element `food`. We then tell Python where to find these elements, which in this case is inside `groceries`". Let us break the entire iteration process down.

At the start of the first iteration, a variable `food` is set to the first value in `groceries`, `'Walnuts'`. Then we print `'I bought some Walnuts today.'` because the f-string inserts the current value of `food` into the string. We then repeat the process; however, `food` is set to the `second` element in the list `'Grapes'`. The third time around, `food` is set to the last element in the list of three elements, `'Bird seeds'`, because we asked Python to run the print `for` each element in the list.

Try to implement the example in a new Python script and run it. It should look something like this:

#### While-Loop

Conditional Statements and Loops

```bash
user@htb[/htb]$ vim groceries.py
user@htb[/htb]$ python3 groceries.py

I bought some Walnuts today.
I bought some Grapes today.
I bought some Bird seeds today.
```

Note that in Python we can iterate over each element produced by a "generator" as well as a collection of data. We will not be covering generators in this module, because we usually don't need to worry about them when writing Python programs.

<br>

---

<br>

## Exercises

Below are the relevant code blocks for the exercises in this section.

#### Code Block 1

```python
list_1  = [5, 3, 'Cake', True, 4, 5]
```

#### Code Block 2

```python
list_2 = [4, 3, 2, 1]

for num in list_2:
    __________
```

#### Code Block 3

```python
list_3 = ['Accidental', '4daa7fe9', 'eM131Me', 'Y!.90']
secret = []

for x in list_3:
    secret.append(x[:2])

print(''.join(secret))
```
