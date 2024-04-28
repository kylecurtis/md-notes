---
tags: [csharp]
---

In C#, type conversion is a fundamental concept that involves converting a value of one data type to another. This is particularly important when dealing with basic data types like integers (`int`), floating-point numbers (`float`, `double`), characters (`char`), and booleans (`bool`). Understanding how to perform these conversions correctly is crucial for data manipulation and ensuring code reliability.

<br>

---

<br>

## Implicit Conversions

<br>

Implicit conversions are automatically performed by the C# compiler when there is no risk of data loss. For example, converting from a smaller to a larger numeric type:

<br>

```csharp
int myInt = 12345;
long myLong = myInt; // Implicit conversion from int to long
```

<br>

---

<br>

## Explicit Conversions

<br>

Explicit conversions (also known as casting) are necessary when there might be a loss of data or precision, or when the conversion might not be safe (such as narrowing conversions). The programmer must specify these conversions explicitly in the code:

<br>

```csharp
double myDouble = 1234.7;
int myInt = (int)myDouble; // Explicit conversion, potential loss of data
```

<br>

---

<br>

## Using System.Convert

<br>

The `System.Convert` class provides methods to convert a base data type to another base data type. It is useful when you need to convert types based on runtime information, and it handles a wide range of conversions:

<br>

```csharp
string numberStr = "12345";
int number = Convert.ToInt32(numberStr); // Converts string to integer
```

<br>

---

<br>

## Conversions Between Numeric Types and Booleans

<br>

Direct conversions between numeric types and `bool` are not supported directly in C#. You need to use conditional logic:

```csharp
int myNumber = 1;
bool myBool = myNumber > 0;  // Convert int to bool using comparison
```

<br>

For converting `bool` to numeric types, you might also use conditional logic:

```csharp
bool isActive = true;
int activeNumber = isActive ? 1 : 0;  // Convert bool to int
```

<br>

---

<br>

## Conversions Involving Characters

<br>

Characters (`char`) can be converted to numeric types by using casting or the `Convert` class, which interprets the character as its Unicode code point:

```csharp
char letter = 'A';
int unicode = letter;  // Implicit conversion to Unicode code
int explicitUnicode = (int)letter;  // Explicit casting
```

<br>

To convert a numeric type to `char`, ensure the numeric value falls within the valid Unicode range and use casting:

```csharp
int letterCode = 65;
char letter = (char)letterCode;  // Explicit conversion from int to char
```

<br>

---

<br>

#### Best Practices

- **Type Safety**: Always prefer type-safe conversions to avoid runtime errors.
- **Overflow Checking**: Use checked contexts to detect overflow conditions when converting between numeric types.
- **Understand Data Loss**: Be cautious with conversions that might result in data loss, particularly from floating-point types to integer types.
- **Use Convert Class**: When dealing with input data of uncertain type, use `Convert` methods as they provide additional checks and handle format exceptions.