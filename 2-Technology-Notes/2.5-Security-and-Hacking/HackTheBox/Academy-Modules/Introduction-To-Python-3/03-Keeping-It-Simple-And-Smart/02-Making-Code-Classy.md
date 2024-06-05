In this section, we will talk about classes. And cake. Let us start with the cake. When we have a piece of brownie in front of us, let us, for the sake of argument, say this piece of brownie is an `object` of the food type `Cake`. Our piece of cake has some properties that other pieces of cake might not have. One such property could be the topping which in our case could be chocolate frosting and a cherry. We need to ask ourselves how this piece of cake was produced and what it consists of.

Cooking recipes and classes are much alike because they define how a dish - or some object - is produced. A cake might have a fixed amount of flour and water, but leave it up to the chef to add a chocolate or strawberry frosting. A `class` is a spec of how an object of some type is produced. The result of `instantiating` such a `class` is an object of the class. Let us look at an example:

#### The DreamCake Class

```python
class DreamCake:
    # Measurements are defined in grams or units
    eggs = 4
    sugar = 300 
    milk = 200
    butter = 50
    flour = 250
    baking_soda = 20
    vanilla = 10

    topping = None
    garnish = None

    is_baked = False

    def __init__(self, topping='No topping', garnish='No garnish'):
        self.topping = topping
        self.garnish = garnish
    
    def bake(self):
        self.is_baked = True

    def is_cake_ready(self):
        return self.is_baked
```

Similar to how functions were defined using the `def` keyword, classes are defined using the `class` keyword, followed by the name of the class, in the CapWords naming convention. CapWords means all words used in the name are capitalized and squeezed together, like `CapWordsArePrettyCool`.

Next up come the ingredients that produce a basic (and tasty, by the way) cake, which will never change in this example. The `topping` and `garnish` variables are set to `None` right after space. This suggests that these variables will have concrete values assigned at a later point - in this case, inside the `__init__` function of the class. This function automatically gets called by Python once a new instance of a class is requested. The `__init__` function is a so-called "Magic Method". We will not cover Magic Methods in detail, but a note about them has been included in the optional, advanced part at the bottom.

Getting back to the class, please notice about the `__init__` function, the `self` parameter. This parameter is a `mandatory, first` parameter of `all` class functions. Long story short, classes need a way to refer to their own variables and functions. Python is designed to require a "`self`" parameter in the first position of the function signature. We can then refer to other functions within class functions by calling `self.other_func()` or `self.topping`. Note that we do not need to provide a value for it when calling functions on class objects despite this first' self' parameter. We will see this later.

Another little trick to notice is the default values for function parameters. These allow us to completely commit specifying a value for one or more of the parameters. The parameters will - in that case - then be set to their default values as specified, and `topping` is set to `'No topping'` unless overridden when we create an object.

Lastly, in this example, we have defined a function `inside of the class scope` as dictated by the indentation level. This means that the function `bake` is `only` accessible to code from within the class itself (e.g., code inside one function calling another function) and objects instantiated from the class. Let us create some example objects to illustrate this behavior better.

#### A Plain Cake

The topping and garnish default to "No topping" and "No garnish" for a plain cake, respectively.

```python
plain_cake = DreamCake()
```

#### A Chocolate Cake

We need to add chocolate frosting on top for a chocolate cake, but no garnish (defaults to `"No garnish"`).

```python
chocolate_cake = DreamCake(topping='Chocolate frosting')
```

#### A Luxury Cake

Our luxury cakes have the topping and garnish explicitly set.

```python
luxury_strawberry_cake = DreamCake(topping='Strawberry frosting', garnish='Chocolate bits')
```

This can, of course, also be specified `without` using named parameters for brevity:

```python
luxury_strawberry_cake = DreamCake('Strawberry frosting', 'Chocolate bits')
```

As shown above, classes are instantiated into objects similar to how we call functions: type the name followed by parentheses with possible parameters specified. Now that we have objects of the class `DreamCake` stored in variables, we can call the functions of the class `on` the object variables by appending a `.` and the function.

#### Baking the Cake

```python
chocolate_cake = DreamCake(topping='Chocolate frosting')

chocolate_cake.bake()  # Call the function "bake" on the object.
is_cake_done = chocolate_cake.is_cake_ready()

print(is_cake_done)  # Prints "True" because we called "bake" earlier
```

See the `bake()` function call on the `chocolate_cake`? Even though the `bake` function within the class has a `self` parameter, we do not need to specify its value. We will not dive into the decisions as to why this is, and it is just something to remember. In closing, it is worth mentioning that this code style is a small part of [Object-Oriented Programming (OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming). There is much more to OOP than simply using classes - enough for an entirely separate module - but in its simplest forms, we define classes, create objects (or "instances") of these classes and use them to hold data or call functions.

<br>

---

<br>

## Advanced Notes on Classes

If you are new to programming, do not be disheartened if this sounds a little too complicated. It is. The following are very brief notes on some more advanced usages of classes, which we mostly do not need to worry about at all in our day-to-day programming, but which are pretty cool to know about regardless.

One thing I promised to explain briefly is Magic Methods. Magic Methods are functions - or methods as they are also called in many programming languages - which exist by default and have a default implementation in all classes. This is because of the `class hierarchy` in Python, where all classes inherit from a base class `object` ("object" is the name of the base class - slightly confusing perhaps).

This statement opens a large box of OOP that we will not go through, but feel free to research "Python class inheritance" and similar phrases on your own. In short, "class inheritance" means that one class can inherit the type and its functions and internal variables. This base class gives objects some basic functionality, for example, the ability to compare against one another (is one cake the same as another?) or get a `string representation` of the object.

Say we have a class `Circle`, the object itself is raw data stored in memory that only Python knows how to read, but the `string representation` of a `Circle` object could be `"Circle(r=5)"` for example describing a circle with a radius of 5. The Magic Method responsible for returning a string representation of an object is `__str__`. Calling this function on an object is similar to calling `str(...)` with the object as a parameter. For example, consider the following snippet from my Python IDLE:

#### Overriding Magic Methods (IDLE)

```python
>>> class Circle:
...     def __init__(self, radius):
...         self.radius = radius
...
...     def __str__(self):
...         return f'Circle(r={self.radius})'
...
>>> my_circle = Circle(5)
>>> str(my_circle)
'Circle(r=5)'
```

If we did not override the `__str__` function, the code would still work, but the output would be less meaningful:

```python
'<__main__.Circle object at 0x022FFB98>'
```

This string represents a `Circle` object inside `__main__` (here, the IDLE), located at memory address `0x022FFB98`.

Another two Magic Methods worth mentioning are the `__enter__` and `__exit__` functions, allowing us to create classes that support using the `with` keyword. The `with` keyword will enable us to specify the default functionality of a class for build-up and teardown procedures. For example, the class `C2TcpConnection` which represents a TCP connection to a C2 server. The build-up step could include initiating a socket and attempting to authenticate given input from external sources. The teardown step could include proper error handling and a guarantee of properly closing the socket after use. This is advanced but fun and "Pythonic" coding which I recommend you to research.

Let us briefly consider an example before moving on to the next section of the module.

#### Class Supporting WITH Context Manager

```python
class Foo():

    def __enter__(self):
        print("Enter...")

    def __exit__(self, type, value, traceback):
        print("...and exit.")
```

Here a class `Foo` is defined with a simple `__enter__` and `__exit__` function, which does nothing but print a message. This allows us to use the `with` clause to "wrap" this supposed reused boilerplate code around concrete code, for example:

```python
with Foo():
    print("Hello world!")
```

This prints the following to the console:

```bash
Enter...
Hello world!
...and exit.
```

Furthermore, we can change the with-clause to something like `with Foo() as foo`, which allows us to reference the instantiated object of `Foo` used to wrap around our code. Doing so is useful if, for example, the `Foo` class has functions we want to call from within the with-clause such as `get_connection_status` in the example of creating a `C2TcpConnection` class. More frequent use of the with clause is `with open('/path/to/file.txt', 'w') as wr`, which opens a file for writing. We can then use `wr.write('something')` to write "something" to the file. At the end of the with-clause, we do not need to close the output streams to the file - the teardown functionality in the `open` class takes care of that.