<br>

Integral types in C# are a category of data types that represent whole numbers, which can be either positive or negative. They are a fundamental aspect of the language, allowing you to perform a variety of mathematical and logical operations.

<br>

---

<br>

## Types of Integral Data Types

<br>

C# provides several integral types, which vary in size and whether they support signed (both positive and negative values) or unsigned (only non-negative values) numbers.

<br>

1. **Signed Integral Types**
   - `sbyte`: 8-bit signed integer. Range from -128 to 127.
   - `short`: 16-bit signed integer. Range from -32,768 to 32,767.
   - `int`: 32-bit signed integer. Range from -2,147,483,648 to 2,147,483,647.
   - `long`: 64-bit signed integer. Range from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.

2. **Unsigned Integral Types**
   - `byte`: 8-bit unsigned integer. Range from 0 to 255.
   - `ushort`: 16-bit unsigned integer. Range from 0 to 65,535.
   - `uint`: 32-bit unsigned integer. Range from 0 to 4,294,967,295.
   - `ulong`: 64-bit unsigned integer. Range from 0 to 18,446,744,073,709,551,615.

<br>

> NOTE: The default value of each integral type is zero, `0`.

<br>

---

<br>

## Integer Table

|C# type/keyword|Range|Size|.NET type|
|---|---|---|---|
|`sbyte`|-128 to 127|Signed 8-bit integer|[System.SByte](https://learn.microsoft.com/en-us/dotnet/api/system.sbyte)|
|`byte`|0 to 255|Unsigned 8-bit integer|[System.Byte](https://learn.microsoft.com/en-us/dotnet/api/system.byte)|
|`short`|-32,768 to 32,767|Signed 16-bit integer|[System.Int16](https://learn.microsoft.com/en-us/dotnet/api/system.int16)|
|`ushort`|0 to 65,535|Unsigned 16-bit integer|[System.UInt16](https://learn.microsoft.com/en-us/dotnet/api/system.uint16)|
|`int`|-2,147,483,648 to 2,147,483,647|Signed 32-bit integer|[System.Int32](https://learn.microsoft.com/en-us/dotnet/api/system.int32)|
|`uint`|0 to 4,294,967,295|Unsigned 32-bit integer|[System.UInt32](https://learn.microsoft.com/en-us/dotnet/api/system.uint32)|
|`long`|-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|Signed 64-bit integer|[System.Int64](https://learn.microsoft.com/en-us/dotnet/api/system.int64)|
|`ulong`|0 to 18,446,744,073,709,551,615|Unsigned 64-bit integer|[System.UInt64](https://learn.microsoft.com/en-us/dotnet/api/system.uint64)|
|`nint`|Depends on platform (computed at runtime)|Signed 32-bit or 64-bit integer|[System.IntPtr](https://learn.microsoft.com/en-us/dotnet/api/system.intptr)|
|`nuint`|Depends on platform (computed at runtime)|Unsigned 32-bit or 64-bit integer|[System.UIntPtr](https://learn.microsoft.com/en-us/dotnet/api/system.uintptr)|

<br>

---

<br>

## Integer Examples

<br>

Here is how you can declare and use integral types in C#:

```csharp
sbyte a = -128; // Signed Byte
byte b = 255; // Unsigned Byte

short c = -32_768; // Signed Short
ushort d = 65_535; // Unsigned Short

int e = -2_147_483_648; // Signed Integer
uint f = 2_147_483_647; // Unsigned Integer

long g = -9_223_372_036_854_775_808; // Signed Integer
ulong h = 18_446_744_073_709_551_615; // Unsigned Integer
```

<br>

> NOTE: Integer values can be separated with underscores (`_`) for readability.

<br>

---

<br>

## BigInteger

In addition to the standard integral types, C# provides the `BigInteger` type, which is part of the `System.Numerics` namespace. Unlike the fixed-size integral types (`int`, `long`, etc.), `BigInteger` can store arbitrarily large integers, limited only by available system memory.

#### Key Features of BigInteger

- **Arbitrary Precision**: `BigInteger` can handle very large numbers that exceed the limits of other data types.
- **Flexible**: It supports all standard arithmetic operations, including those that can produce very large results that would otherwise overflow standard integral types.

#### Usage of BigInteger

To use `BigInteger`, you must add a reference to `System.Numerics` and include it at the top of your code file:

```csharp
using System.Numerics;
```

<br>

Here’s how you can declare and manipulate `BigInteger` values:

```csharp
BigInteger bigInt1 = BigInteger.Parse("123456789012345678901234567890"); 
BigInteger bigInt2 = BigInteger.Add(bigInt1, 1);  // Adding 1 to bigInt1
Console.WriteLine(bigInt2);  // Outputs 123456789012345678901234567891
```

<br>

---

<br>

## Integer Literals

<br>

Integer literals can be

- _decimal_: without any prefix
- _hexadecimal_: with the `0x` or `0X` prefix
- _binary_: with the `0b` or `0B` prefix

<br>

```csharp
var decimalLiteral = 42;
var hexLiteral = 0x2A;
var binaryLiteral = 0b_0010_1010;
```

<br>

---

<br>

## Operations with Integral Types

<br>

Integral types support standard arithmetic operations such as addition, subtraction, multiplication, and division. Be mindful of overflow and underflow conditions, which occur when operations exceed the range of the type.

<br>

```csharp
int maxInt = int.MaxValue;  // 2,147,483,647
int overflowExample = maxInt + 1;  // This will cause overflow
Console.WriteLine(overflowExample);  // Output: -2,147,483,648 due to overflow
```

<br>

To safely handle overflow and underflow, C# provides checked and unchecked contexts. In a `checked` context, the overflow throws an exception, while in an `unchecked` context, it wraps around to the minimum value.