File Input/Output (I/O) is a critical aspect of many applications and is well supported in C# through the `System.IO` namespace. This namespace provides numerous classes that enable reading from and writing to files, creating new files and directories, and performing operations such as moving, copying, or deleting files.

## FileStream

The `FileStream` class, part of the `System.IO` namespace, provides a powerful and flexible interface for reading from and writing to files. As a core component of C#'s I/O library, `FileStream` supports both sequential and random file access, allowing you to interact with a file's content anywhere, not just at its beginning or end.

A `FileStream` object can be seen as a cursor into the contents of a file, much like a text cursor that you move when editing a document. You can place this cursor at any position within the file and perform read or write operations.

### Creating a FileStream

There are several ways to create a `FileStream`. One common approach is using its constructor directly, as shown in the following code snippet:

```csharp
FileStream fs = new FileStream("test.dat", FileMode.OpenOrCreate, FileAccess.ReadWrite);
```

In this example, the `FileStream` constructor takes three arguments:

1. The first argument is a string specifying the path to the file.
    
2. The second argument is an enumeration of the type `FileMode`, which determines how the operating system should open the file. In this case, `FileMode.OpenOrCreate` means that the file should be opened if it exists; otherwise, a new file should be created.
    
3. The third argument is an enumeration of the type `FileAccess`, which indicates the type of access you want to the file. Here, `FileAccess.ReadWrite` grants the rights to read from and write to the file.
    

### Reading and Writing with FileStream

To write data to a file, you use the `Write` method of the `FileStream` class.

```csharp
byte[] data = new byte[] { 1, 2, 3, 4, 5 };
fs.Write(data, 0, data.Length);
```

In this example, `Write` is called on the `FileStream` object `fs` to write the byte array `data` to the file. The second and third arguments to `Write` are the starting point in the array and the number of bytes to write, respectively.

To read data from a file, you can use the `Read` method of the `FileStream` class, as shown in the following example:

```csharp
byte[] data = new byte[1024];
int bytesRead = fs.Read(data, 0, data.Length);
```

In this case, `Read` is called on the `FileStream` object `fs` to read bytes into the `data` array. The second and third arguments to `Read` are the starting point in the array and the maximum number of bytes to read, respectively. `Read` returns the actual number of bytes read, which may be less than the requested number if the end of the file is reached.

### Manipulating the File Position

An important feature of `FileStream` is the ability to get or set the position within the file, represented by the `Position` property. For example, you can move to the start of the file with the following code:

```csharp
fs.Position = 0;
```

Or, you can move to a specific position within the file:

```csharp
fs.Position = 50; // Moves to the 51st byte in the file.
```

This feature of random access is particularly useful when dealing with large files or when you need to jump to specific sections of a file.

### Closing the FileStream

Finally, when you're done with a `FileStream`, it's essential to close it to free up the resources it's using. You can do this with the `Close` method:

```csharp
fs.Close();
```

Alternatively, since `FileStream` implements `IDisposable`, you can take advantage of the `using` statement to automatically close the stream:

```csharp
using (FileStream fs = new FileStream("test.dat", FileMode.OpenOrCreate, FileAccess.ReadWrite))
{
    // perform file operations...
}
```

When the `using` block is exited (either after normal execution or an exception), the `Dispose` method is called on `fs`, which in turn calls `Close`, ensuring that the file is properly closed.

## StreamReader and StreamWriter

`StreamReader` and `StreamWriter` are powerful classes within the `System.IO` namespace for reading and writing character data. As high-level abstractions, they provide a more convenient interface for dealing with text files than the `FileStream` class.

### StreamReader

A `StreamReader` reads characters from a byte stream in a particular encoding (such as UTF-8). It's ideal for reading text files.

#### Creating a StreamReader

A `StreamReader` is typically instantiated with a `FileStream` or a file path. For example:

```csharp
StreamReader sr = new StreamReader("test.txt");
```

This code creates a `StreamReader` to read from the file `test.txt`.

#### Reading Data with StreamReader

`StreamReader` provides several methods to read data from the stream. For instance, you can read one line at a time with `ReadLine`:

```csharp
string line = sr.ReadLine();
```

To read the entire content of the file at once, you can use the `ReadToEnd` method:

```csharp
string content = sr.ReadToEnd();
```

Remember to close the `StreamReader` when you're done with it:

```csharp
sr.Close();
```

### StreamWriter

While `StreamReader` is used for reading text data, `StreamWriter` is used for writing text data. It's an efficient way to write text to a file or a stream.

#### Creating a StreamWriter

A `StreamWriter` can be instantiated in a similar way to `StreamReader`. You can pass a `FileStream` or a file path to the constructor:

```csharp
StreamWriter sw = new StreamWriter("test.txt");
```

This code creates a `StreamWriter` that writes to the file "test.txt".

#### Writing Data with StreamWriter

`StreamWriter` provides several methods for writing data to the stream. You can write a string with the `Write` method:

```csharp
sw.Write("Hello, World!");
```

To write a string and then immediately follow it with a newline, use `WriteLine`:

```csharp
sw.WriteLine("Hello, World!");
```

Remember to close the `StreamWriter` when you're done with it:

```csharp
sw.Close();
```

In StreamReader and StreamWriter, you can use the `using` statement, which automatically closes the stream when the `using` block is exited. This ensures that resources are correctly disposed of, even if an exception is thrown within the block:

```csharp
using (StreamWriter sw = new StreamWriter("test.txt"))
{
    sw.WriteLine("Hello, World!");
}
```

## File and Directory

The `File` and `Directory` classes in the `System.IO` namespace contain static methods for creating, copying, deleting, moving, and opening files and directories and performing various other file and directory operations.

### File

The `File` class allows you to work with files. It provides static methods, so you don't need to instantiate the class to use these methods.

#### Creating and Writing to a File

The `WriteAllText` method writes a specified string to a file. If the file already exists, it will be overwritten. If it doesn't exist, the method will create it:

```csharp
File.WriteAllText("test.txt", "Hello, World!");
```

#### Reading from a File

The `ReadAllText` method reads all text from a file and returns it as a string:

```csharp
string content = File.ReadAllText("test.txt");
Console.WriteLine(content);
```

#### Checking if a File Exists

You can check whether a file exists using the `Exists` method:

```csharp
if (File.Exists("test.txt"))
{
    Console.WriteLine("The file exists.");
}
```

### Directory

The `Directory` class provides static methods for manipulating directories.

#### Creating a Directory

You can create a directory using the `CreateDirectory` method:

```csharp
Directory.CreateDirectory("TestDirectory");
```

This code creates a new directory named `TestDirectory`. If the directory already exists, this method does not create a new directory but doesn’t return an error.

#### Checking if a Directory Exists

You can check whether a directory exists using the `Exists` method:

```csharp
if (Directory.Exists("TestDirectory"))
{
    Console.WriteLine("The directory exists.");
}
```

#### Getting Files and Subdirectories

The `GetFiles` method returns the names of files in a directory, and the `GetDirectories` method returns the names of subdirectories:

```csharp
string[] files = Directory.GetFiles("TestDirectory");
string[] subdirectories = Directory.GetDirectories("TestDirectory");
```