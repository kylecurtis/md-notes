Recall what we discussed in the beginning about importing modules and that Python scripts are executed from top to bottom, even when imported. This means that if somebody were to import our script, e.g., reuse some of our functions (it could be ourselves), the code would run as soon as imported. The typical way to avoid this is to put all the code that `does something` into the "main" block. Let us do that:

#### The "main" Block

```python
if __name__ == '__main__':
    page_url = 'http://target:port'
    the_words = get_all_words_from(page_url)
    top_words = get_top_words_from(the_words)

    for i in range(10):
        print(top_words[i][0])
```

The most important thing to know about the conditional statement is what we need to type to have the code inside it run whenever we execute it with the Python binary. Please refer to the brilliant answer at [StackOverflow](https://stackoverflow.com/a/419185) for an in-depth explanation of what is going on here. The critical takeaway is that the code inside this conditional statement only gets executed when the script is `run`, not `imported`.

However, we can remove the constant `PAGE_URL`, which we relied on before, and have everything inside the code's main block.

Another improvement we can make is getting rid of the URL variable altogether by making the script flexible and accepting an input argument when running Python and the script. For example, we could enhance the program to accept input arguments along the lines of `python3 wordextractor.py http://foo.bar/baz` or better yet, prepare the script to accept named parameters in an arbitrary order, e.g.:

#### Accepting Arguments

```bash
user@htb[/htb]$ python3 wordextractor.py --url http://foo.bar/baz
```

Doing so would allow us to easily extend the program with, for example, a word length limit, so we avoid uninteresting words like `and`, `is` and `that`.

Let us look at one module to help us achieve this: [click](https://click.palletsprojects.com).

To understand what `click` does, we need to talk about `decorators`. However, since this is a bit of a mouthful to jump right into, let us leave it as optional reading at the end of this section. All we need to know about `click` at this point is a few simple click-specific concepts that are easy to memorize. Let us get started by installing it as always using pip: `pip3 install click`. The following is an example script from the official documentation, but slightly modified for simplicity's sake:

#### A Simple Click Script

```python
import click

@click.command()
@click.option('--count', default=1, help='Number of greetings.')
@click.option('--name', prompt='Your name', help='The person to greet.')
def hello(count, name):
    for i in range(count):
        click.echo('Hello %s!' % name)

if __name__ == '__main__':
    hello()
```

Lots of new things happened here in relatively few lines of code. First of all, there are the `decorators` which, in a sense, "decorate functions." These are the things about the function definition that start with an `@`. We need to focus on not getting too technical too quickly because these decorators in `click` let us set up command-line arguments to the script. First, we specify the `@click.command()` decorator, indicating that we will have a command-line input for this `hello` function. Then two `@click.option` options are specified. In this example, the parameters are pretty straightforward: we have got a `default` for the count, in case this is not specified as a command-line argument, we have `help` text for the `--help` output, and we have a `prompt` parameter. This tells Python to `prompt` the user for input if no command-line argument is given.

Lastly and probably most importantly, notice that all the "main part" of the code does is call the `hello()` function. Click requires us to call a function with these decorators specified to work. Also, notice that the parameter names for the function `hello` and the input argument names `--count` and `--name` match names if we ignore the `--`.

Let us look at some examples to illustrate things better. First up is a plain run without any arguments. Here we are prompted for an input for the `--name` parameter:

#### Playing With Click

```bash
C:\Users\Birb> python click_test.py

Your name: Birb
Hello Birb!
```

This we can also specify explicitly:

```bash
C:\Users\Birb> python click_test.py --name Birb

Hello Birb!
```

Moreover, the `--count` parameter can be explicitly set instead of it being 1 by default:

```bash
C:\Users\Birb> python click_test.py --name Birb --count 3

Hello Birb!
Hello Birb!
Hello Birb!
```

Lastly, here is the `--help` output:

```bash
C:\Users\Birb> python click_test.py --help

Usage: click_test.py [OPTIONS]

Options:
  --count INTEGER  Number of greetings.
  --name TEXT      The person to greet.
  --help           Show this message and exit.
```

As we can see in the help message, `INTEGER` and `TEXT` are printed. However, we never actually specified this in the code. The reason is that `click` will attempt to `guess the correct type` based on things like the `default` parameter. For more information, please refer to the (relatively well written) documentation.

In preparation for using `click`, we will move all the code previously in the "main part" of the script into its own, new `main()` function. The name of this new function is not essential as long as the function is being called.

#### Refactoring Into Separate Function

```python
def main():
    page_url = 'http://target:port'
    the_words = get_all_words_from(page_url)
    top_words = get_top_words_from(the_words)

    for i in range(10):
        print(top_words[i][0])

if __name__ == '__main__':
    main()
```

We then need to add the click functionality to the function, as well as replace variables where needed:

#### Adding Click Options

```python
@click.command()
@click.option('--url', '-u', prompt='Web URL', help='URL of webpage to extract from.')
@click.option('--length', '-l', default=0, help='Minimum word length (default: 0, no limit).')
def main(url, length):
    the_words = get_all_words_from(url)
    top_words = get_top_words_from(the_words, length)
    # Remaining code omitted
```

As can be seen, we added two parameters to the function, `url` and `length`, and used these instead of the hardcoded URL we used before. The parameter names must be the same as the `--name` in the option spec for click to automatically map the input to those variables. If we were to use an input argument (i.e., a `click.option`) that had to be different than the parameter name in Python - e.g., for aesthetic reasons - we could tell `click` to map the variables appending the Python parameter name after the argument option names, e.g., `@click.option('--url', '-u', 'target_uri', ...)`.

In this case, we can let the `count_occurrences_in` function deal with the filtering. To do this, we need to first pass in the length variable into the `get_top_words_from` function, and inside this one, pass it along to the `count_occurrences_in` function. There are many ways to do this. If we were to add another filtering option, e.g., only find words that match some regex, it could be a good idea to keep the filtering a separate process that can apply a filter on a list of words and return those that match. The following two functions were updated:

```python
def count_occurrences_in(word_list, min_length):
    word_count = {}

    for word in word_list:
        if len(word) < min_length:
            continue
        if word not in word_count:
            word_count[word] = 1
        else:
            current_count = word_count.get(word)
            word_count[word] = current_count + 1
    return word_count

def get_top_words_from(all_words, min_length):
    occurrences = count_occurrences_in(all_words, min_length)
    return sorted(occurrences.items(), key=lambda item: item[1], reverse=True)
```

Starting at the bottom, we pass along the `min_length` parameter to the first function. In here we add one additional check: `if len(word) < min_length`. If it is, we `continue`, which in the context of a loop means "do not bother about the rest of this block, simply skip ahead to the next element and forget about this one." So, if the word is shorter than our minimum length, we will `continue` to the next word and thus _not_ add it to the `word_count` dictionary.

The final script looks like this:

#### The Final Script

```python
import click
import requests
import re
from bs4 import BeautifulSoup

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

def count_occurrences_in(word_list, min_length):
    word_count = {}

    for word in word_list:
        if len(word) < min_length:
            continue
        if word not in word_count:
            word_count[word] = 1
        else:
            current_count = word_count.get(word)
            word_count[word] = current_count + 1
    return word_count

def get_all_words_from(url):
    html = get_html_of(url)
    soup = BeautifulSoup(html, 'html.parser')
    raw_text = soup.get_text()
    return re.findall(r'\w+', raw_text)

def get_top_words_from(all_words, min_length):
    occurrences = count_occurrences_in(all_words, min_length)
    return sorted(occurrences.items(), key=lambda item: item[1], reverse=True)

@click.command()
@click.option('--url', '-u', prompt='Web URL', help='URL of webpage to extract from.')
@click.option('--length', '-l', default=0, help='Minimum word length (default: 0, no limit).')
def main(url, length):
    the_words = get_all_words_from(url)
    top_words = get_top_words_from(the_words, length)

    for i in range(10):
        print(top_words[i][0])

if __name__ == '__main__':
    main()
```

For the extra adventurous student, here is a list of ideas for further extension of the tool:

- Add a `--output` / `-o` argument that lets us define an output file to print to instead of the console (something like `with open('path.txt', 'w') as wr:` and `wr.write(word)`).
    
- Add common password mutations to the output, e.g., Capitalized, lowercase, UPPERCASE, and with various bits appended like the current and recent years, random numbers or symbols, e.g., 2019, 1!, 2!, 3!, 01, 123. `Summer2021!` and similar variations are depressingly frequent passwords.
    
- Add a `--depth` / `-d` argument specifying the _crawl depth_ of the script. This implies the ability to grab not only words but also URLs on the webpage(s), check if they are within scope (e.g., domain), and add them to a list of pages to crawl next.
    
- The program currently crashes if a minimum length of 10 or higher is specified. Try to figure out why and fix it (hint: check out that last for-loop).