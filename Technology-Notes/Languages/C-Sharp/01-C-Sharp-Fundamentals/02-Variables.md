
<br>

Variables are fundamental building blocks in C#. They act as containers for storing data values. In C#, each variable is defined with a specific type, which determines the size and layout of the variable's memory, the range of values that can be stored, and the set of operations that can be applied to the variable.

<br>

---

<br>

## Defining Variables

<br>

To define a variable in C#, you specify the type followed by the variable name. You can also initialize the variable with a value.

<br>

```csharp
int age = 30; // Declaring an integer variable initialized with 30
string name = "Alice"; // Declaring a string variable initialized with "Alice"
bool isActive = true; // Declaring a boolean variable initialized with true
```

<br>

---

<br>

## Variable Naming Conventions

<br>

Variable names in C# can include letters, digits, and underscores. However, they must start with a letter or an underscore. It's crucial to choose meaningful names for variables to make the code more readable and maintainable.

<br>

```csharp
double salary; // Good practice for naming
int _cacheSize; // Starts with an underscore, valid but less common
```

<br>

---

<br>

## Scope of Variables

<br>

The scope of a variable determines where the variable can be accessed within the code. It is defined by the location where the variable is declared:

<br>

- **Local Variables**: Declared inside a method or block and can only be accessed within that method or block.
- **Member Variables (Fields)**: Declared inside a class but outside any method. They can be accessed by any method within the class, depending on their access modifiers.

<br>

```csharp
public class Employee
{
    int employeeId; // Field accessible within the class

    void DisplayId()
    {
        int localId = 10; // Local variable accessible only within this method
        Console.WriteLine(employeeId); // Accessing the class field
        Console.WriteLine(localId); // Accessing the local variable
    }
}
```

<br>

---

<br>

## Dynamic vs. Static Typing

<br>

C# is primarily a statically typed language, meaning the type of a variable is known at compile-time. However, C# also supports dynamic typing using the `dynamic` keyword, where the type is resolved at runtime.

<br>

```csharp
dynamic data = 10; // Initially an integer
data = "Hello"; // Now a string
```

<br>

---

<br>

## Immutable Variables

<br>

C# allows declaring variables whose values cannot be changed after initialization, using the `readonly` or `const` keyword. `readonly` variables can be assigned in the declaration or in a constructor, while `const` variables must be assigned at declaration and their values must be known at compile-time.

<br>

```csharp
public class MathConstants
{
    public const double PI = 3.14159; // Constant value
    public readonly int data; // Read-only, can be set only in constructor

    public MathConstants(int initialData)
    {
        data = initialData; // Setting read-only variable
    }
}
```
