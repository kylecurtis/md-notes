At this point, we have used multiple packages in our projects and even installed third-party packages. These packages physically exist in a predetermined location so that the Python interpreter can locate the packages when we try to import them or elements from inside of them. The default location is the `site-packages` directory. This is true for Windows systems, however on Debian and Debian-based systems such as Kali, Parrot, and Ubuntu, the external libraries are located inside a `dist-packages` location. However, the principle is the same.

The default `site-packages`/`dist-packages` locations are the following:

- Windows 10: `PYTHON_INSTALL_DIR\Lib\site-packages`:

```bash
C:\Program Files\Python38\Lib\site-packages
```

- Linux: `/usr/lib/PYTHON_VERSION/dist-packages/`:

```bash
/usr/lib/python3/dist-packages
```

The reason why packages are located inside a `dist-packages` rather than a `site-packages` directory on Debian-based systems stems from how Debian-based systems handle packages installed with the package manager (`apt`). However, for simplicity's sake, we will use the common name of `site-packages` going forward. If we take a look inside this directory, we will see many packages available for Python. A package in all its simplicity is just a folder with at least an `__init__.py` file inside of it and optionally (although nearly always) other python files and nested folder structures.

<br>

---

<br>

## Directories and Search Paths

Instead of producing a fully functional script for scraping words off a website, we decided to write the script as an API. We could package the script together with an `__init__.py` file (even an empty one is fine) and place the package inside the site-packages directory. Python already knows to check this location when searching for packages. This is not always practical. However, we can tell Python to look in a different directory before searching through the site-packages directory by specifying the `PYTHONPATH` environment variable. As we can see below, without having set a `PYTHONPATH` environment variable, the search path includes only the standard directories:

#### Inspecting the Default Search Path

```bash
user@htb[/htb]$ python3

Python 3.9.2 (default, Feb 28 2021, 17:03:44) 
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.path
['', '/usr/lib/python39.zip', '/usr/lib/python3.9', '/usr/lib/python3.9/lib-dynload', '/usr/local/lib/python3.9/dist-packages', '/usr/lib/python3/dist-packages', '/usr/lib/python3.9/dist-packages']

>>>
```

Now let's specify a `PYTHONPATH` environment variable and see how it affects the search path:

#### Inspecting the default search path

```bash
user@htb[/htb]$ PYTHONPATH=/tmp/ python3

Python 3.9.2 (default, Feb 28 2021, 17:03:44) 
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.path
['', '/tmp/', '/usr/lib/python39.zip', '/usr/lib/python3.9', '/usr/lib/python3.9/lib-dynload', '/usr/local/lib/python3.9/dist-packages', '/usr/lib/python3/dist-packages', '/usr/lib/python3.9/dist-packages']

>>>
```

Since we set the `PYTHONPATH` to the root directory, this has been prepended to the search path. This means two things: first of all, the packages that exist at the `/tmp/` location can now be imported and used in the project or IDLE, and secondly, it means we can highjack other packages, changing the behavior. The latter point is a bonus if we can control the `PYTHONPATH` of a system to include our malicious package. We will mainly use the search path to specify where to find our APIs in everyday development scenarios.

Suppose we wanted to have the packages installed in a specific folder. For example, we wanted to keep all packages related to us inside some `/var/www/packages/` directory. In that case, we can have pip install the package and store the content inside this folder with the `--target` flag, like so:

#### Installing Python Modules at Target Location

```bash
user@htb[/htb]$ python3 -m pip install --target /var/www/packages/ requests

Collecting requests
  Using cached requests-2.25.1-py2.py3-none-any.whl (61 kB)
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.4-py2.py3-none-any.whl (153 kB)
     |████████████████████████████████| 153 kB 8.1 MB/s
...SNIP...
```

<br>

---

<br>

## Virtual Environments

So far, we have looked at installing packages onto the local machine, making packages available to all scripts in our system. If we, for one reason or the other, need to use one specific version of a package for one project and another version of the same package for another project, we will face problems. One solution for this kind of isolation of projects is using `virtual environments` or `venv` for short. The `venv` module allows us to create virtual environments for our projects, consisting of a folder structure for the project environment itself, a copy of the Python binary and files to configure our shell to work with this specific environment. Let us take a look at some examples.

First of all, we will create a virtual environment called `academy`.

#### Preparing the Virtual Environment

```bash
user@htb[/htb]$ python3 -m venv academy
```

Next up, we can source the `activate` script located in `academy/bin/`. This configures our shell by setting up the required environment variables so that when we, for example, run `pip install requests`, we will be using the Python binary that was copied as part of creating the virtual environment, like so:

#### Sourcing the venv and installing a package

```bash
Fugl@htb[/htb]$ source academy/bin/activate
(academy) Fugl@htb[/htb]$ pip install requests

Collecting requests
  Using cached requests-2.25.1-py2.py3-none-any.whl (61 kB)
Collecting idna<3,>=2.5
...SNIP...
Successfully installed certifi-2020.12.5 chardet-4.0.0 idna-2.10 requests-2.25.1 urllib3-1.26.4
```

Notice the `(academy)` prefix after sourcing the `activate` script. This indicates that our terminal is configured to run commands for that particular virtual environment.

For penetration testing, it can be advisable to use virtual environments so that projects and packages related to those projects are kept separate. This will ensure that when we know that a project works as is, it will not break in the future because, for example, an external package was updated when working on another project.

<br>

---

<br>

## In Closing

There are many ways to achieve the same goal. We have looked at some of them, and they will get us very far; however, there are better tools and solutions for larger or more permanent projects. Say we developed a custom `C2` (`Command & Control`) in Python and needed a reliable and separate environment to host the server in. Virtual environments will likely work fine, but an alternative is to use container software such as `Docker` or even a fully isolated Virtual Machine. For larger software projects in Python, virtual environments might be pleasing for parts of the way. Additionally, package- and environment management software such as [Conda](https://docs.conda.io/en/latest/) will allow greater control of the project, especially when collaborating with others. These technologies and methodologies are worthy of their own modules.