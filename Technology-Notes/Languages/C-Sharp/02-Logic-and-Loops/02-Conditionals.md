<br>

Conditional statements are fundamental to programming, allowing you to control the flow of execution based on certain conditions. In C#, the primary constructs for conditional logic are `if` statements, `else` and `else if` clauses, and `switch` statements.

<br>

---

<br>

## If Statements

<br>

The `if` statement evaluates a boolean expression and executes a block of code if the expression is `true`. It's the most basic form of decision-making in C#.

```csharp
if (condition)
{
    // Code to execute if the condition is true
}
```

<br>

You can extend this logic with `else` and `else if` to handle multiple conditions:

```csharp
if (condition1)
{
    // Code executes if condition1 is true
}
else if (condition2)
{
    // Code executes if condition2 is true
}
else
{
    // Code executes if neither condition1 nor condition2 is true
}
```

<br>

---

<br>

## Switch Statements

<br>

The `switch` statement allows you to execute different parts of code based on the value of an expression. It is particularly useful when you have multiple possible conditions that could trigger different actions.

```csharp
switch (expression)
{
    case value1:
        // Code to execute if expression == value1
        break;
    case value2:
        // Code to execute if expression == value2
        break;
    default:
        // Code to execute if expression doesn't match any case
        break;
}
```

<br>

In C# 8.0 and later, switch expressions provide a more concise syntax for cases that simply return a value:

```csharp
var result = expression switch
{
    value1 => result1,
    value2 => result2,
    _ => defaultResult
};
```

<br>

---

<br>

## Conditional Operator

<br>

Also known as the ternary operator, this provides a shorthand way of executing expressions based on a condition. It's useful for simple conditions that assign a value based on whether the condition is `true` or `false`.

<br>

```csharp
var result = condition ? valueIfTrue : valueIfFalse;
```

<br>

---

<br>

## Pattern Matching in Switch

<br>

Starting with C# 7.0, switch statements support pattern matching which allows for more complex conditions and neater code.

<br>

```csharp
switch (object)
{
    case int i when i >= 0:
        // Execute logic for non-negative integers
        break;
    case string s:
        // Execute logic for strings
        break;
    default:
        // Execute if none of the patterns match
        break;
}
```

<br>

---

<br>

## Best Practices for Using Conditionals

<br>

- **Clarity and Maintainability**: Use the simplest form of conditional logic that achieves the functionality you need. Overly complex nested conditionals can be hard to read and maintain.
- **Use Braces**: Always use braces `{}` for blocks under `if`, `else`, `else if`, and `switch` statements, even if the block contains only one statement. This improves readability and reduces the risk of errors when modifications are made.
- **Avoid Deep Nesting**: Deeply nested conditionals can be very difficult to follow. Consider refactoring complex conditionals into separate methods or using pattern matching to simplify the logic.
- **Expression Bodied Members**: For simple conditionals that assign values or return results, consider using expression-bodied members or switch expressions to make the code more concise.

<br>

---

<br>

## Operators in Conditional Statements

<br>

In C#, operators play a crucial role in conditional logic, determining the flow of execution based on specific conditions.

<br>

#### Relational Operators

Relational operators compare two values and return a boolean result (`true` or `false`). These are foundational in `if` and `else if` conditions:

```csharp
int a = 10, b = 20;
if (a < b)
{
    Console.WriteLine("a is less than b");
}
```

<br>

#### Logical Operators

Logical operators (`&&`, `||`, `!`) are used to combine multiple boolean expressions or to negate a boolean condition. They are essential for forming complex conditional statements:

```csharp
bool hasHighTemperature = true, hasSoreThroat = false;
if (hasHighTemperature && !hasSoreThroat)
{
    Console.WriteLine("Might just be a fever without other symptoms.");
}
```

<br>

#### Bitwise Operators

While not commonly used in high-level application logic, bitwise operators (`&`, `|`, `^`) can be used in conditions where you need to manipulate individual bits of integral types, useful in lower-level programming:

```csharp
int mask = 0b_1000;
int flags = 0b_1010;
if ((flags & mask) != 0)
{
    Console.WriteLine("The bit is set.");
}
```

<br>

#### Use of Conditional Operator

The conditional (ternary) operator provides a compact syntax for assigning values based on a condition, ideal for simplifying code inside assignments:

```csharp
int score = 75;
string grade = score > 60 ? "Pass" : "Fail";
Console.WriteLine(grade);
```

<br>

#### Pattern Matching with Switch

C# 7.0 introduced pattern matching capabilities that extend the versatility of switch statements, allowing conditions based on type and properties:

```csharp
object value = 34;
switch (value)
{
    case int n when n > 0:
        Console.WriteLine("Positive integer");
        break;
    case string s:
        Console.WriteLine("It's a string");
        break;
    default:
        Console.WriteLine("Unknown type");
        break;
}
```

