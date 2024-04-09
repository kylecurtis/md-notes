We will start implementing the program little by little, always ensuring that we reach a milestone where the code works, even though it may not be entirely complete yet. Even if we have a firm idea of how the code will be implemented and what it will look like in the end, it is still a good idea to take it slow and build things up layer by layer.

Since we want to end up with a program that can fetch all words of a webpage and perhaps also have a few other features, let us first write the code needed to do the most basic task: printing the HTML of a webpage. In short, this is what we should be aiming for:

- The code will download and print the entire HTML of a webpage.
- The URL of the webpage is fixed inside the code.
- We will write the code in its simplest form and rewrite bits and pieces as needed when we need to.
- We will use the `requests` library.

So first things first, let us import the requests library and store the target URL in a variable. Then we use the requests library to get the URL that we provided and print the HTML.

#### Printing Web Page Source Code

```python
import requests

PAGE_URL = 'http://target:port'

resp = requests.get(PAGE_URL)
html_str = resp.content.decode()
print(html_str)
```

Now, what happens if we misspell the URL? Let's try it out in our Python interactive terminal and see:

#### Experimenting in IDLE

```python
>>> r = requests.get('http://target:port/missing.html')
>>> r.status_code

404
>>> print(r.content.decode())

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
        "http://www.w3.org/TR/html4/strict.dtd">
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
        <title>Error response</title>
    </head>
    <body>
        <h1>Error response</h1>
        <p>Error code: 404</p>
        <p>Message: File not found.</p>
        <p>Error code explanation: HTTPStatus.NOT_FOUND - Nothing matches the given URI.</p>
    </body>
</html>
```

On a positive note, we do get a proper `status_code` from the webserver, which in this example is the webserver module that comes along with Python (`http.server`). However, if we were expecting that the HTML output contains specific elements that we then tried to access and use, for example, a `<div id="products">`, our Python program would crash while trying to use things that do not exist. There are no products on this error page! Whoops. Let us implement a simple fail check that makes sure we do not try to work with broken links.

#### Naive "error" Handling

```python
import requests

PAGE_URL = 'http://target:port'

resp = requests.get(PAGE_URL)

if resp.status_code != 200:
    print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
    exit(1)

html_str = resp.content.decode()
print(html_str)
```

Now though, we have some code that does something, but it is not in a function. To avoid cluttering the code, it is advisable to keep things `simple` and `separate`, so let us go ahead and `refactor` the code, that is, let us change and thus improve the code.

---

## The get_html_of Function

Let us take a look at the following code:

```python
import requests

PAGE_URL = 'http://target:port'

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

print(get_html_of(PAGE_URL))
```

We moved the part of the code that fetches the HTML into a function and then changed the last line of the code to print the result of this function call instead of a variable (which no longer exists). Also, notice the indentation within the function.

Having gotten the most basic functionality in place, we can begin to work with the HTML page. So, let us for a moment think about what it is we need to do. For this kind of exercise, it can be a good idea to list actions upon a piece of paper, and then for each action, ask oneself, "How do I do this?" and then write up those steps next to it. In our case, we need to:

- Find all words on the page, ignoring HTML tags and other metadata.
- Count the occurrence of each word and note it down.
- Sort by occurrence.
- Do something with the most frequently occurring words, e.g., print them.

How do we find all words on the page, ignoring HTML tags and other metadata? This is where BeautifulSoup comes into play. A quick look at the documentation (https://www.crummy.com/software/BeautifulSoup/bs4/doc/) shows that we can call the `get_text()` BeautifulSoup object to get all of the text on the webpage as a string.

Next, we need to count the occurrences of each word. There are many ways to do this. We could pick the first word, count all occurrences of that, note it down, and note down which word we already counted. Then we could move to the next word and - if it has not already been counted - count the occurrence and note this down along with checking off the word as "counted." This process is relatively simple but also rather slow. Imagine doing this exercise for an entire book full of words. This is relatively inefficient.

Let us be more innovative and think for a moment if an application or machine in real life already accounts for several items of a specific size, shape, or value. The coin counter in old vending machines comes to mind.

#### Old School Vending Machines

Before smartphones and the digitalization of many machines was a thing, vending machines would have to count the number of coins somebody inserted and how many of each. Some machines could do this by having the coin slide down a ramp and have the coin slide into the smallest possible hole, starting from small to large. As such, a large coin would slide over a small coin hole, whereas a small coin would fall through the hole. A coin would then be accounted for once (e.g., by activating a small metal arm/switch as it falls).

If we count words the same way some vending machines count coins, we can count all occurrences of all words and only need to go through the text once. We will have a `dictionary` of word occurrences and then, for each word, check if this has been seen before. If it has, we will increment the count by one. If it has not been added before, we will add a record of the word and an occurrence of one of the words.

After this, we have to sort by occurrence to see which words occurred the most, and then finally, we can decide to print the ten most used words. Alternatively, we could filter the words and only look at those above four characters or append variations of numbers and symbols and generate a dictionary for password attacks. More on that later.

<br>

---

<br>

## Regex

The first step was to find all words in the HTML while ignoring HTML tags. If we use the `get_text()` function we discussed earlier, we can use the `regular expression` module `re` to help us. This module has a `findall` function which takes some string of `regex` (shorthand for "`reg`gular `ex`pression") and some text as parameters and then returns all occurrences in a list. We will use the regex string `\w+`, which matches all word characters, that is, `a-z`, `A-Z`, `0-9`, and `_`. Here is the updated code:

#### Finding All Words in HTML

```python
import requests
import re
from bs4 import BeautifulSoup

PAGE_URL = 'http://target:port'

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

html = get_html_of(PAGE_URL)
soup = BeautifulSoup(html, 'html.parser')
raw_text = soup.get_text()
all_words = re.findall(r'\w+', raw_text)
```

One new addition to the mix is the `r'...'` string. This is a `r`aw string, meaning Python should assume that characters inside the string are the actual characters to use. Normally a `\` is used as an `escape-character`, which helps us define special characters - or bytes rather - for example, the `\n` or `\t`, the new line and tab characters, respectively. Here `r'\w+'` is telling Python to interpret the `\w` part of the string as two individual characters and not an escaped `w`.

When we run this, nothing happens except in memory. The `all_words` variable is, assuming everything goes well, a list of all the words from the webpage in order of occurrence and including duplicates. We will next loop through this list and count each word. One way to achieve that is this below piece of code:

#### Counting Word Occurrences

```python
# Previous code omitted
all_words = re.findall(r'\w+', raw_text)

word_count = {}

for word in all_words:
    if word not in word_count:
        word_count[word] = 1
    else:
        current_count = word_count.get(word)
        word_count[word] = current_count + 1
```

This snippet should look familiar. To recap quickly, we declare a new variable `word_count` as an empty dictionary - a data structure of key/value pairs allowing the lookup of some value given some key. Then we go through each word in `all_words` and check if it exists already. We set the key (word) to a value of `1` if it does not. Otherwise (else), we get the current value set for `word` and set the new value of `word` to the previous value plus one.

We now have a dictionary of all the words found on the website and their respective occurrence.

|**Advanced Tricks: "Python is easy"**|
|---|
|It is often said that Python is easy, to which my reply always is "simple Python is easy, complex Python is not". The previous example of counting words can in fact be cut down to these two lines:  <br>  <br>for word in all_words:  <br>    word_count[word] = word_count.setdefault(word, 0) + 1  <br>  <br>However the amount of things happening here is quite surprising. In short, "setdefault" will EITHER set the value of the key ("word") to the specified value (0), if the dictionary does not already contain a "word" key, OR it will return the current value of the "word" key. The 2nd line thus EITHER sets a value of 1 for the "word" key, OR it fetches the current value and increments it by one. Confusing? Yes. Our point? Fancy code is not always the best choice, so keep it simple and smart. We are not here to show off, we are here to solve problems.|

To get a sorted list of the words so that we can focus on the most occurring ones, we either magically come up with the below piece of code or - more realistically - we Google for help ("python sort dictionary by values" and similar search terms) and find the below answer.

#### Sorting Words in a List

```python
top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True)
```

As with all things online, do not just blindly trust that they are not malicious. As for highly-rated content and answers with lots of positive feedback, a bit of advice is the old saying: trust, but verify. Once we are sure that the piece of code we found is what we need. We can finally print the top-10 words like so:

#### Printing 10 Elements

```python
>>> top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True)
>>> for i in range(10):
...    print(top_words[i])
```

Doing so will print an output along the lines of:

```python
>>> top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True)
>>> for i in range(10):
...    print(top_words[i])

('foo', 6)
('bar', 5)
('bas', 5)
('hello', 4)
('academy', 4)
('birb', 1)
```

This looks perhaps a little odd or at least not very useful for our onwards journey. What we can do is to print the actual word instead of printing each tuple of (word, occurrence) by selecting the first element of the tuple for each tuple (`top_words[i][0]`). The current iteration of the entire code looks like this:

#### The First Iteration

```python
import requests
import re
from bs4 import BeautifulSoup

PAGE_URL = 'http://target:port'

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

html = get_html_of(PAGE_URL)
soup = BeautifulSoup(html, 'html.parser')
raw_text = soup.get_text()
all_words = re.findall(r'\w+', raw_text)

word_count = {}

for word in all_words:
    if word not in word_count:
        word_count[word] = 1
    else:
        current_count = word_count.get(word)
        word_count[word] = current_count + 1

top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True)

for i in range(10):
    print(top_words[i][0])
```