Console applications run in a console window (also known as a command line interface) instead of a graphical user interface (GUI). In a console application, users interact with the program by entering commands as text, and the program responds with text-based output. The `Console` class provides methods and properties to interact with the console. These include functionalities such as reading from and writing to the console, changing the colour of the console text and background, changing the title of the console window, and altering the size and position of the console window, among others.

## Console.Read

The `Console.Read` method is a member of the `Console` class and is utilised for reading a single character from the standard input stream, which is typically the keyboard. The primary feature of this method is that it blocks the current thread of execution until a character is available. This effectively pauses the program, awaiting user input.

When the user inputs a character and presses the enter key, `Console.Read` retrieves the ASCII value of the character and returns it as an integer. If the end of the input stream has been reached, this method will return -1.

```csharp
Console.Write("Please press a key: ");
int input = Console.Read();
Console.WriteLine("You pressed: " + (char)input);
```

In this code, the `Console.Read` method is used to capture the user's key press, and the ASCII value returned is converted back into a character for display.

## Console.ReadLine

The `Console.ReadLine` method, another member of the `Console` class, is designed to read an entire line of input from the standard input stream. Unlike `Console.Read`, which reads a single character, `Console.ReadLine` captures all characters input by the user until they press the enter key.

Upon pressing the enter key, `Console.ReadLine` returns the captured input as a string. If no further lines are available (i.e., the end of the input stream is reached), the method will return null.

```csharp
Console.Write("Please enter your name: ");
string name = Console.ReadLine();
Console.WriteLine("Hello, " + name);
```

In this example, `Console.ReadLine` captures the user's name as a string. The program then greets the user using the provided name.

## Console.Write

The `Console.Write` method is a fundamental mechanism for displaying output to the console in C#. It is designed to write the specified string value to the standard output stream, typically the console window. This method does not append a trailing newline character to the output. As a consequence, any subsequent calls to `Console.Write` or `Console.WriteLine` will continue on the same line in the console.

It's important to note that `Console.Write` can handle other data types in addition to strings. It accomplishes this by automatically invoking the `ToString` method on the provided argument, converting it to a string before output.

```csharp
Console.Write("Pi is approximately ");
Console.Write(3.14159);
```

In this example, the first `Console.Write` call outputs a string, while the second outputs a floating-point number. The `ToString` method is implicitly called to convert the number into a string for display.

## Console.WriteLine

The `Console.WriteLine` method behaves very similarly to `Console.Write`, with one key distinction: it automatically appends a newline character (`\n`) after the output. This has the effect of moving the cursor to the beginning of the next line in the console. Therefore, any subsequent `Console.Write` or `Console.WriteLine` calls will start outputting on a new line.

```csharp
Console.WriteLine("Hello, World!");
Console.WriteLine("Today's date is " + DateTime.Now.ToShortDateString());
```

In this example, the first `Console.WriteLine` call outputs a greeting and moves the cursor to the next line. The second call outputs a string concatenated with today's date, obtained via `DateTime.Now.ToShortDateString()` and converted to a string via implicit use of `ToString`.