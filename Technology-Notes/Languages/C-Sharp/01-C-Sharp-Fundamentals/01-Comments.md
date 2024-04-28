---
tags: [csharp]
---

In C#, comments are used to annotate the source code with explanations, making the code easier to understand for anyone reading it later, including the original author. Comments are non-executable parts of the code and are completely ignored by the compiler.

<br>

---

<br>

## Types of Comments in C

<br>

C# supports several types of comments:

1. **Single-Line Comments**
2. **Multi-Line Comments**
3. **XML Documentation Comments**

<br>

---

<br>

#### Single-Line Comments

Single-line comments begin with two forward slashes (`//`). Anything following `//` on the same line is treated as a comment.

```csharp
// This is a single-line comment.
Console.WriteLine("Hello, World!");  // This is a comment after code.
```

<br>

#### Multi-Line Comments

Multi-line comments start with `/*` and end with `*/`. Everything between these markers is considered a comment, regardless of the number of lines.

```csharp
/* This is a multi-line comment that can span multiple lines.
   You can use this type of comment to explain complex code structures
   or to temporarily comment out blocks of code during testing. */
Console.WriteLine("Hello, World!");
```

<br>

#### XML Documentation Comments

XML documentation comments are special and begin with `///`. These comments are used to generate XML documentation for the code and can be processed by tools to automatically produce documentation. They are often placed above definitions for functions, properties, classes, etc., and can include additional tags to describe parameters, return values, and exceptions.

```csharp
/// <summary>
/// This is a description for the Main method.
/// </summary>
/// <param name="args">An array of command-line arguments.</param>
static void Main(string[] args)
{
    Console.WriteLine("Hello, World!");
}
```