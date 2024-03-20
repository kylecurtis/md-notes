<br>

> In Python, numbers are an essential data type used to store numerical values. 
> <br>
> They are immutable data types, meaning once a number is created, it cannot be modified.

<br>

---

<br>

## Number Types

<br>

Python supports three distinct numeric types:

<br>

> -**Integers (`int`)**: These are whole numbers, which can be positive, negative, or zero. There is no limit to how long an integer can be.
><br>
> -**Floating-point numbers (`float`)**: These represent real numbers and are written with a decimal point.
> <br>
> -**Complex numbers (`complex`)**: These are written in the form of `a + bj`, where `a` and `b` are floats and represent the real and imaginary parts, respectively.

<br>

---

<br>

## Basic Operations

<br>

Python allows you to perform a variety of arithmetic operations with numbers:

<br>

Addition
```python
print(3 + 5)  # Output: 8
```

<br>

Subtraction
```python
print(10 - 2)  # Output: 8
```

<br>

Multiplication
```python
print(4 * 2)  # Output: 8
```

<br>

Division
```python
print(16 / 2)  # Output: 8.0
```

<br>

Floor Division
```python
print(17 // 2)  # Output: 8
```

<br>

Modulus
```python
print(18 % 10)  # Output: 8
```

<br>

Exponent
```python
print(2 ** 3)  # Output: 8
```

<br>

---

<br>

## Converting Between Number Types

<br>

You can convert between different number types using the `int()`, `float()`, and `complex()` functions:

<br>

Converting float to int
```python
print(int(10.6))  # Output: 10
```

<br>

Converting int to float
```python
print(float(20))  # Output: 20.0
```

<br>

Creating complex number
```python
print(complex(3, 5))  # Output: (3+5j)
```

<br>

---

<br>

## Working with Floating-Point Numbers

<br>

#### Floating-Point Inconsistencies

Due to their internal representation, floating-point numbers can introduce small errors in calculations:

```python
print(0.1 + 0.2 == 0.3)  # Output: False
```

<br>

#### The `Decimal` Module

To handle these inconsistencies, you can use the `Decimal` class from the `decimal` module.

<br>

> **NOTE:** It offers precise arithmetic and can be configured to meet various requirements for precision and rounding.

<br>

```python
from decimal import Decimal

# Using Decimal for precise arithmetic
result = Decimal('0.1') + Decimal('0.2')
print(result == Decimal('0.3'))  # Output: True
```

<br>

---

<br>

## Number Methods / Functions

<br>

`abs()`: Returns the absolute value of a number.

```python
print(abs(-7)) # Output: 7
```

<br>

`divmod()`: Returns the quotient and remainder when dividing two numbers.

```python
print(divmod(10, 3)) # Output: (3, 1)
```

<br>

`pow()`: Returns the value of x raised to the power y.

```python
print(pow(2, 3)) # Output: 8
```

<br>

`round()`: Rounds a floating-point number to a specified number of digits.

```python
print(round(3.14159, 2)) # Output: 3.14
```

<br>

---

<br>

## Math Module Functions

<br>

The `math` module extends the list of mathematical functions:

- `math.floor()`: Returns the largest integer less than or equal to x.
<br>
- `math.ceil()`: Returns the smallest integer greater than or equal to x.
<br>
- `math.sqrt()`: Returns the square root of x.
<br>
```python
import math

print(math.floor(4.7))  # Output: 4
print(math.ceil(4.2))   # Output: 5
print(math.sqrt(16))    # Output: 4.0
```
