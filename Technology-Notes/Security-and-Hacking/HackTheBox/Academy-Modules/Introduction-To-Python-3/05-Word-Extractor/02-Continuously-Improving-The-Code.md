At this point, we have a working Python script that will extract words from a webpage and print the top-10 most occurring ones to the console.

Let us suppose that our engagement required us to count words on two web pages. We would then need to repeat large amounts of the above code for the new webpage. Alternatively, we could _refactor_ the current code and move the word counting part into its function.

#### Extracting The Counting Code to Its Function

```python
def count_occurrences_in(word_list):
    word_count = {}
    for word in word_list:
        if word not in word_count:
            word_count[word] = 1
        else:
            current_count = word_count.get(word)
            word_count[word] = current_count + 1
    return word_count
```

Notice how we added an input parameter and replaced the list of words to iterate over to this new `word_list` parameter. We also added a `return statement` at the bottom so that our function can give back the result. We can do the same for the code that currently acts like glue in our script:

#### Current Glue

```python
html = get_html_of(PAGE_URL)
soup = BeautifulSoup(html, 'html.parser')
raw_text = soup.get_text()
all_words = re.findall(r'\w+', raw_text)
```

By simply replacing the `PAGE_URL` constant (by naming convention - it's not constant) with the `url` variable and returning the result of the regular expression `findall` call, we've turned the static glue into reuseable code:

#### Refactored to Its Function

```python
def get_all_words_from(url):
    html = get_html_of(url)
    soup = BeautifulSoup(html, 'html.parser')
    raw_text = soup.get_text()
    return re.findall(r'\w+', raw_text)

all_words = get_all_words_from(PAGE_URL)
```

If we perform the same exercise for the remaining code, we get this:

#### Refactoring the Remaining Code

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

def count_occurrences_in(word_list):
    word_count = {}

    for word in word_list:
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

def get_top_words_from(all_words):
    occurrences = count_occurrences_in(all_words)
    return sorted(occurrences.items(), key=lambda item: item[1], reverse=True)

all_words = get_all_words_from(PAGE_URL)
top_words = get_top_words_from(all_words)

for i in range(10):
    print(top_words[i][0])
```

Notice, in addition to the above, the following piece of refactored code.

#### Glue, But Cleaner

```python
def get_top_words_from(url):
    all_words = get_all_words_from(url)
    occurrences = count_occurrences_in(all_words)
    return sorted(occurrences.items(), key=lambda item: item[1], reverse=True)
```

This function takes a URL as a parameter and then immediately uses the URL to call another function that gets the list of words needed. This additional refactoring made the code a fair bit cleaner and easier to read `in this situation`. If we were to crawl ten pages, we would need to refactor yet again, not to repeat ourselves over and over again. Alternatively, we could load a list of URLs from a text file, do the word collecting for each URL and aggregate the data in the end. However, instead of trying to solve a problem that does not exist, let us move on.