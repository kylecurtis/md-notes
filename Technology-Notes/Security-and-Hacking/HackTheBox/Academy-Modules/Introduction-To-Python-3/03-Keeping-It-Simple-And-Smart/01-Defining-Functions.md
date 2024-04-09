So far, we have been looking at common techniques for controlling code flow, making it possible for us to build simple tools, for example, counters or even a simple wordlist enricher. For example: for each word in the wordlist, first set the counter to 0, while the counter is less than 100, print the word and the counter and increase the counter by 1. For reference, this could look something like this:

#### Password Generator Example

```python
wordlist = ['password', 'john', 'qwerty', 'admin']

for word in wordlist:
    counter = 0
    while counter < 100:
        print(f'{word}{counter}')
        counter = counter + 1
```

In this case, the for-loop repeats the loop until it has processed all entries from the list. As shown, even with simple building blocks, we can achieve a lot. Let us talk about the following important building block in software: `Functions`

<br>

---

<br>

## Functions

Functions let us define code blocks that perform a range of actions, produce a range of values, and optionally return one or more of these values. Like in math, where `f(x)` is a `function f of x` and produces the same result when given the same input. For example `f(x) = x + 1` is a function `f` of `x` which returns `x + 1`. Thus `f(2)` would be `3`, because `f(2) = 2 + 1` which is `3`.

Similarly, in Python, we can define and call functions to reuse code and work with our data more efficiently - as we do not need to reinvent the wheel all the time. We can define functions in Python in their simplest form very easily.

Here is an example of defining `f(x) = 2 * x + 5` as a function in Python:

#### First Function

```python
def f(x):
    return 2 * x + 5
```

Besides the (essential) syntax with indentation at the `inner scope` of the function - the code inside the function - what is important to note here are the `def` and `return` keywords. The `def` keyword is how we define functions in Python. Following `def` comes the function name (written in snake_case), input parameters inside the parentheses, and a colon. This first line of a function is called the `signature` of the function. After having written a couple of different functions, we can tell them apart by simply looking at their names and the arguments they accept. We can tell them apart by comparing their function signatures.

Let us create a function to calculate and return that one value to the power of another value:

#### Power_Of Function

```python
def power_of(x, exponent):
    return x ** exponent
```

In Python, the `**` symbols mean "power of". If we call `power_of(4, 2)`, we will get back four-to-the-power-of-two or simply four squared. Now, where does this result end up? It will end up in one of two places, depending on what we do: 1) the empty void of nothingness, 2) a variable. Consider this example:

#### Function Call

```python
def power_of(x, exponent):
    return x ** exponent

power_of(4, 2)  		# The function was run, but nothing caught the return value.
eight = power_of(2, 3)  # Variable "eight" is now equal to two-to-the-power-of-three.
```

So is the first form pointless, then? No. As with the input/output of a terminal, we can "pipe" the function's output to the "input" of another. We can use the result of calling a function as the input for another one. For example:

```python
print('My favourite number is:')
print(power_of(4, 2))
```

Here we are calling the function `print` and giving it first a string as input, and next, we are giving it `the result` of another function call. At `runtime`, during the script's actual execution, Python will first execute the first line and then go to the 2nd line and execute the commands from inside out. It will, in other words, start by calculating `power_of(4, 2)` and then use this result as input to the `print` function.

Imagine if we were to call a function with ten parameters. Having to remember each parameter is challenging once the amount of parameters increases above two, so in addition to these `positional` parameters, Python supports what is called `named parameters`. While positional parameters require us to always insert the parameters in the correct order, named parameters let us use whichever order we prefer. However, they require us to specify which value goes to which parameter explicitly. Using named parameters might seem silly, but after a week or a month of looking at other things, it can be a blessing to have expressly specified, by parameter names, which is which. Let us look at an example. Consider the below function, which is a template invitation to a school event.

#### Invitation.py

```python
def print_sample_invitation(mother, father, child, teacher, event):

    # Notice here the use of a multi-line format-string: f''' text here '''
    sample_text = f'''
Dear {mother} and {father}.
{teacher} and I would love to see you both as well as {child} at our {event} tomorrow evening. 

Best regards,
Principal G. Sturgis.
'''
    print(sample_text)

print_sample_invitation()
```

If we were just to fill out the blanks, chances are we would forget who is who within minutes, rather than weeks. Note: the above code will error because we do not provide any arguments for the `print_sample_invitation` function.

What we can do instead is to specify exactly who is who, like so:

```python
print_sample_invitation(mother='Karen', father='John', child='Noah', teacher='Tina', event='Pizza Party')
```

Specifying the names within the function will change our script to this:

#### Invitation.py - Modified

```python
# Defining the function
def print_sample_invitation(mother, father, child, teacher, event):

    # Notice here the use of a multi-line format-string: f''' text here '''
    sample_text = f'''
Dear {mother} and {father}.
{teacher} and I would love to see you both as well as {child} at our {event} tomorrow evening. 

Best regards,
Principal G. Sturgis.
'''
    # Print output
    print(sample_text)

# Call function
print_sample_invitation(mother='Karen', father='John', child='Noah', teacher='Tina', event='Pizza Party')
```

This will produce the following output:

#### Invitation.py - Execution

```bash
user@htb[/htb]$ python3 invitation.py

Dear Karen and John.
Tina and I would love to see you both as well as Noah at our Pizza Party tomorrow evening.

Best regards,
Principal G. Sturgis.
```

Once again, Python scripts are executed from top to bottom, so always keep in mind that Python needs to know about the functions and variables before they are being referenced. Also, keep in mind the scopes of the code. Scopes let us reference variables and functions `outside` of our current scope (e.g., code in functions can use variables and the global scope), but not `inside` of it. In other words, we cannot reuse a variable we defined inside a function, outside of it. Besides that, Python comes with many different [Built-in Functions](https://docs.python.org/3/library/functions.html).

Now that we know the basics of defining and working with functions, let us add some more building blocks to our arsenal of coding tools: `Classes`