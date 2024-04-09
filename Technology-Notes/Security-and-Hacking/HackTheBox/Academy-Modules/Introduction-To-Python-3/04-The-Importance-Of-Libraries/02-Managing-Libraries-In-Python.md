The most popular way of installing external packages in Python is by using [pip](https://pip.pypa.io/en/stable/). According to the author, `pip` is short for ["pip installs packages"](https://ianbicking.org/blog/2008/10/pyinstall-is-dead-long-live-pip.html), a recursive abbreviation (meaning the definition refers to the abbreviation, and thus circles itself). Very funny indeed. Regardless, `pip` is the name of the Python module that manages external Python packages. With `pip`, we can install, uninstall and upgrade Python packages. Unlike downloading and installing plugins for a browser or text editor, it is not common to "go shopping" for Python packages.

Programming is all about using the right tool for the job, so do not worry about finding packages to install. The right approach, and probably also the one most common, is finding out `how to do something` and getting package recommendations along the way. The documentation of these packages - their websites most of the time - will typically show examples of installing the package for first-time users. Let us look at how to manage packages as well.

Some valuable arguments for `pip` that we will look at are `install` and`--upgrade` flag, `uninstall` and `freeze`. The `install` argument lets users install new packages or upgrade existing packages to the latest version (if the `--upgrade` parameter is provided). The `uninstall` argument will, as its name suggests, remove the package from the system. Surprisingly the `freeze` command has nothing to do with halting anything or cheesy police movies. This prints a list of all the installed (via pip) packages and their dependencies. We can call the commands either using `pip` directly or as a Python module. Below are some examples of how this might look.

#### Installing "flask" with Pip

```bash
user@htb[/htb]$ # Syntax: python3 -m pip install [package]
user@htb[/htb]$ python3 -m pip install flask

Collecting flask
  Using cached Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting Werkzeug>=0.15
  Using cached Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting itsdangerous>=0.24
  Using cached itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting click>=5.1
  Using cached click-7.1.2-py2.py3-none-any.whl (82 kB)
Collecting Jinja2>=2.10.1
  Downloading Jinja2-2.11.3-py2.py3-none-any.whl (125 kB)
     |████████████████████████████████| 125 kB 7.0 MB/s 
Collecting MarkupSafe>=0.23
  Downloading MarkupSafe-1.1.1-cp39-cp39-macosx_10_9_x86_64.whl (16 kB)
Installing collected packages: Werkzeug, itsdangerous, click, MarkupSafe, Jinja2, flask
Successfully installed Jinja2-2.11.3 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.2 flask-1.1.2 itsdangerous-1.1.0
```

As can be seen, even though we only asked to install `flask`, a brilliant package for running Python-based web servers (as is `bottle` - same-same, but different), we get a multitude of other packages as well, which are all requirements of `flask`. We could try to upgrade it, but we are already told that we are already running the latest version.

#### Upgrading Packages

```bash
user@htb[/htb]$ python3 -m pip install --upgrade flask

Requirement already up-to-date: flask in /usr/local/lib/python3.9/site-packages (1.1.2)
Requirement already satisfied, skipping upgrade: itsdangerous>=0.24 in /usr/local/lib/python3.9/site-packages (from flask) (1.1.0)
Requirement already satisfied, skipping upg...
<SNIP>
```

If we wanted to uninstall a particular package, we could do so by calling:

#### Uninstalling Packages

```bash
user@htb[/htb]$ pip uninstall [package]
```

Let us see what is currently installed by running `pip` with the `freeze` argument. As some of them are dependencies of `flask`, we will leave the uninstallation itself as "extras." Please note that if we choose to uninstall a dependency package, the primary package likely will not work. Also, note that `freeze` may produce different outputs from machine to machine and Python version to Python version.

#### Listing the Installed Packages

```bash
user@htb[/htb]$ # Syntax: python3 -m pip freeze [package]
user@htb[/htb]$ python3 -m pip freeze

click==7.1.2
Flask==1.1.2
itsdangerous==1.1.0
Jinja2==2.11.3
MarkupSafe==1.1.1
protobuf==3.13.0
pynput==1.7.3
pyobjc-core==7.1
pyobjc-framework-Cocoa==7.1
pyobjc-framework-Quartz==7.1
six==1.15.0
Werkzeug==1.0.1
```

This list of installed packages would be nice to be given to another person to either use our scripts or help with development. This way, they will know which packages need to be installed (and which versions even).

It just so happens to be the case that `pip` supports maintaining packages from a requirements file. This file, often called literally `requirements.txt`, contains a list of all the required packages needed to run the script successfully. The format is quite simple. We would copy the above `freeze` output and save it as a requirements file. However, it is a little bloated, and we do not need to know or even list the dependencies of the packages we need.

For the sake of an example, let us suppose that we would like to use `flask` and `click` (we will return to `click` later). If we do not know the version requirements or do not mind, either way, we could list the packages one after the other and save them, like so:

#### Example requirements.txt

```bash
user@htb[/htb]$ cat requirements.txt

flask
click
```

Then, to install all the packages in the requirements file, we would type:

#### Install from requirements.txt

```bash
user@htb[/htb]$ python3 -m pip install -r requirements.txt
```

This will then go through each of the requirements and install them by selecting the latest available and permitted version. Say we explicitly wanted `flask` version 1.1.2. All we had to do was replace `flask` with `flask==1.1.2` in the requirements file, just like the `pip freeze` command output. Below is a list of common version comparison operators that we are highly likely to come across in larger Python projects (read more at [PEP 440](https://www.python.org/dev/peps/pep-0440/#version-specifiers)).

|**Comparison Operator**|**Description**|
|---|---|
|`==`|Version matching clause|
|`<=` / `>=`|Inclusive ordered comparison clause|
|`<` / `>`|Exclusive ordered comparison clause|

They let us specify, in the requirements file, our exact requirements to versions. For example, if we know that some package `xyz` is vulnerable to exploitation at versions 1.0.4 and lower, we can specify in our requirements file that we need `xyz>=1.0.5`. It is also pretty common for new updates of a package to break the current code (e.g., packages that rely on other third-party systems like the Discord bot API for Python). In these cases, we can force an older version of a package. At the same time, the needed changes were being worked on with the `<` or `<=` operator.

To not dig too deep into it right from the start, we will return to this topic later in the module. For now, let us move on with some pre-requisites for our first project.