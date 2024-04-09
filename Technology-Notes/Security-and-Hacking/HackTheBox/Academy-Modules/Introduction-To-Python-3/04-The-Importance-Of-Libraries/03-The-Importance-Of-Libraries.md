Now that we know how important libraries can be for our development and how to manage them let us discuss two of the more popular ones that we will use in our project, starting with the `requests` library.

<br>

---

<br>

## The Requests Package

The [requests](https://requests.readthedocs.io/en/master/) library is an elegant and simple HTTP library for Python. From the documenation:

Requests allows you to send HTTP/1.1 requests extremely easily. There’s no need to manually add query strings to your URLs, or to form-encode your POST data. Keep-alive and HTTP connection pooling are 100% automatic, thanks to urllib3.

Let us install requests just like we have learned.

#### Installing requests

```bash
user@htb[/htb]$ python3 -m pip install requests

Collecting requests
  Downloading requests-2.25.1-py2.py3-none-any.whl (61 kB)
     |████████████████████████████████| 61 kB 3.8 MB/s
Collecting chardet<5,>=3.0.2
  Downloading chardet-4.0.0-py2.py3-none-any.whl (178 kB)
     |████████████████████████████████| 178 kB 6.8 MB/s
Collecting certifi>=2017.4.17
...SNIP...
Successfully installed certifi-2020.12.5 chardet-4.0.0 idna-2.10 requests-2.25.1 urllib3-1.26.3
```

Once installed, we can import the library into our code by typing `import requests` and then use it right away.

The two most useful things to know about the requests library are making HTTP requests, and secondly, it has a `Session` class, which is useful when we need to maintain a certain context during our web activity. For example, if we need to keep track of a range of cookies, we could use a `Session` object. To get one of these, we `import requests` and create an object of the `Session` class like `sess = requests.Session()`. Alternatively, we can use the `requests` module (the library itself) to make HTTP requests. However, this will not keep its state automatically.

Consider the following code:

#### Example of Requests

```python
import requests

resp = requests.get('http://httpbin.org/ip')
print(resp.content.decode())

# Prints:
# {
#   "origin": "X.X.X.X"
# }
```

This is a simple example of how to perform a GET request to obtain our public IP address. Since the `resp.content` variable is a `byte-string`, a string of bytes that may or may not be printable, we have to call `decode()` on the object. Decoding the `byte-string` with the `decode()` function and no parameters tells Python to interpret the bytes as UTF-8 characters. UTF-8 is the default encoding used when no other encoding is specified. However, other encodings can be used and set as parameter arguments to the `decode()` function, for example, `decode(encoding='UTF-16')`. Going back to the `resp` object, this contains useful information such as the `status_code`, the numeric HTTP status code of the request we made, and cookies. We will use this library later on, but for now, let us move on with some more food talk.

<br>

---

<br>

## The BeautifulSoup Package

Another handy package is the BeautifulSoup library (rather `beautifulsoup4`). This library makes working with HTML a lot easier in Python. Before, we learned how to query a website and get output back, which could be the raw HTML. Digging through this HTML can be cumbersome if we have to search through textual output by hand. BeautifulSoup turns the HTML into Python objects that are much easier to work with and allows us to analyze the content better programmatically. Let us install BeautifulSoup.

#### Installing BeautifulSoup

```bash
user@htb[/htb]$ python3 -m pip install beautifulsoup4

Collecting beautifulsoup4
  Downloading beautifulsoup4-4.9.3-py3-none-any.whl (115 kB)
     |████████████████████████████████| 115 kB ...
Collecting soupsieve>1.2
  Downloading soupsieve-2.2-py3-none-any.whl (33 kB)
Installing collected packages: soupsieve, beautifulsoup4
Successfully installed beautifulsoup4-4.9.3 soupsieve-2.2
```

Once installed, let's go through some quick examples of how to use `BeautifulSoup`. For a more in-depth walkthrough, please visit the [documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). For now, please consider the below code:

#### HTML - Ugly Format

```html
<html>
<head><title>Birbs are pretty</title></head>
<body><p class="birb-food"><b>Birbs and their foods</b></p>
<p class="food">Birbs love:<a class="seed" href="http://seeds" id="seed">seed</a>
   and 
   <a class="fruit" href="http://fruit" id="fruit">fruit</a></p>
 </body></html>
```

This HTML looks a little messy. We will assume that this HTML is stored in a variable `html_doc`. We'll then load this into BeautifulSoup and print it in a nicely formatted way, as follows:

#### Example of BeautifulSoup

```python
from bs4 import BeautifulSoup

html_doc = """ html code goes here """
soup = BeautifulSoup(html_doc, 'html.parser')
print(soup.prettify())
```

which then prints:

#### HTML - Pretty Format

```html
<html>
 <head>
  <title>
   Birbs are pretty
  </title>
 </head>
 <body>
  <p class="birb-food">
   <b>
    Birbs and their foods
   </b>
  </p>
  <p class="food">
   Birbs love:
   <a class="seed" href="http://seeds" id="seed">
    seed
   </a>
   and
   <a class="fruit" href="http://fruit" id="fruit">
    fruit
   </a>
  </p>
 </body>
</html>
```

The import statement of BeautifulSoup is worth noticing. Because the class `BeautifulSoup` lies within the module `bs4` we will usually import it this way. What happens in the code is that the class is imported from the module, and then we create a new BeautifulSoup object and set the parser of the class to the HTML parser of BeautifulSoup. We need to set this parser when loading HTML.

Let us not delve too long into thought-up examples and instead move straight to the actual implementation of our final product: the word extractor.