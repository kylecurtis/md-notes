---
tags: [csharp]
---

Floating-point types in C# are used to represent numbers that have fractional parts. They are essential for representing real-world quantities which can be integral or fractional, such as measurements and other calculations involving real numbers. C# provides three floating-point types: `float`, `double`, and `decimal`.

<br>

---

<br>

## Float

<br>

- **Precision**: 7-digit precision.
- **Size**: 4 bytes (32 bits).
- **Range**: Approximately $\pm 1.5 \times 10^{-45}$ to $\pm 3.4 \times 10^{38}$.
- **Usage**: Suitable for scientific calculations where high precision is not required. Because of its smaller size and faster processing than `double`, it is used when memory and performance are a consideration.

<br>

```csharp
float pi = 3.14159f;
```

<br>

> NOTE: Notice the `f` suffix, which tells the compiler it's a float literal.

<br>

---

<br>

## Double

<br>

- **Precision**: 15-16 digit precision.
- **Size**: 8 bytes (64 bits).
- **Range**: Approximately $\pm 5.0 \times 10^{-324}$ to $\pm 1.7 \times 10^{308}$.
- **Usage**: It is the default type for real numbers in C#. `double` is used when the precision provided by `float` is insufficient, and is commonly used in scientific and financial calculations where precision is more important but the full capability of `decimal` is not required.

<br>

```csharp
double e = 2.718281828459045;
```

<br>

> NOTE: No suffix is required, as 'double' is the default type for real numbers.

<br>

---

<br>

## Decimal

<br>

- **Precision**: 28-29 significant digits.
- **Size**: 16 bytes (128 bits).
- **Range**: Approximately $\pm 1.0 \times 10^{-28}$ to $\pm 7.9 \times 10^{28}$.
- **Usage**: Provides the highest precision and is primarily used in financial applications where precision of calculations like currency is crucial. It is also used where the exactness of the calculation is critical to avoid errors due to rounding.

<br>

```csharp
decimal price = 19.95m;
```

<br>

> NOTE: The `m` suffix indicates a decimal literal.

<br>

---

<br>

## Considerations

<br>

- **Precision and Scale**: Understand the precision and scale that your application requires. `float` and `double` can introduce rounding errors in calculations, so they are not suitable for situations where exact decimal representation is required, such as monetary calculations.
- **Performance**: Operations with `decimal` are slower compared to `float` and `double` due to its higher precision and different internal representation.
- **Choosing the Right Type**: Use `float` for less precise calculations with a smaller memory footprint, `double` for general floating-point operations, and `decimal` for high precision requirements.

<br>

---

<br>

## Handling Precision Issues

<br>

Floating-point arithmetic can lead to precision issues. For instance, summing up large numbers of `float` or `double` values can accumulate significant rounding errors. Here’s an example showing a common pitfall:

<br>

```csharp
double result = 0.1 + 0.2; // Might not exactly equal 0.3 due to precision errors.
Console.WriteLine(result == 0.3); // Outputs: False
```

<br>

To mitigate such issues:
- Use `decimal` for calculations requiring high precision and exactness.
- Be mindful of the operations performed on floating-point numbers, especially in loops or cumulative calculations.