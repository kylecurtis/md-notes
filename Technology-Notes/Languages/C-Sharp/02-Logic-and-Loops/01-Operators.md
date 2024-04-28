---
tags: [csharp]
---

In C#, operators are special symbols that specify what type of operation to perform on one or more operands. Understanding and using these operators effectively is essential for writing concise and efficient C# code. Operators in C# can be classified into several categories: arithmetic, relational, logical, bitwise, assignment, and others.

<br>

---

<br>

## Arithmetic Operators

<br>

Arithmetic operators perform mathematical operations on numeric operands and include:

<br>

- `+` (Addition)
- `-` (Subtraction)
- `*` (Multiplication)
- `/` (Division)
- `%` (Modulus)

<br>

```csharp
int a = 10;
int b = 3;

int sum = a + b; // sum is 13
int diff = a - b; // diff is 7
int product = a * b; // product is 30
int quotient = a / b; // quotient is 3
int remainder = a % b; // remainder is 1
```

<br>

---

<br>

## Relational Operators

<br>

Relational operators compare two operands and return a Boolean value (`true` or `false`):

<br>

- `==` (Equal to)
- `!=` (Not equal to)
- `>` (Greater than)
- `<` (Less than)
- `>=` (Greater than or equal to)
- `<=` (Less than or equal to)

<br>

```csharp
int a = 10; 
int b = 3;

bool isEqual = (a == b); // false
bool isNotEqual = (a != b); // true

bool isGreaterThan = (a > b); // true
bool isLessThan = (a < b); // false

bool isGreaterThanOrEqual = (a >= b); // true
bool isLessThanOrEqual = (a <= b); // false
```

<br>

---

<br>

## Logical Operators

<br>

Logical operators are used to combine multiple Boolean expressions:

<br>

- `&&` (Logical AND)
- `||` (Logical OR)
- `!` (Logical NOT)

<br>

```csharp
int a = 10; 
int b = 3;

bool result = (a > b) && (b > 0); // true
bool alternative = (a > b) || (b < 0); // true
bool negation = !(a == b); // true
```

<br>

---

<br>

## Bitwise Operators

<br>

Bitwise operators perform operations on the binary representations of numbers:

<br>

- `&` (Bitwise AND)
- `|` (Bitwise OR)
- `^` (Bitwise XOR)
- `~` (Bitwise NOT)
- `<<` (Left shift)
- `>>` (Right shift)

<br>

```csharp
int a = 10; 
int b = 3;

int c = a & b; // Bitwise AND
int d = a | b; // Bitwise OR
int e = a ^ b; // Bitwise XOR
int leftShift = a << 2; // Multiplies a by 4
int rightShift = a >> 2; // Divides a by 4
```

<br>

---

<br>

## Assignment Operators

<br>

Assignment operators assign values to variables with optional modification:

<br>

- `=` (Simple assignment)
- `+=` (Add and assign)
- `-=` (Subtract and assign)
- `*=` (Multiply and assign)
- `/=` (Divide and assign)
- `%=` (Modulus and assign)

<br>

```csharp
// Simple assignment
int a = 10; 

// Add and assign
a += 5; // a = a + 5

// Subtract and assign
a -= 5; // a = a - 5

// Multiply and assign
a *= 5; // a = a * 5

// Divide and assign
a /= 5; a = a / 5;

// Modulus and assign
b %= 3; // b = b % 3
```

<br>

---

<br>

## Other Operators

<br>

- **Ternary Operator (`?:`)**: Provides a shorthand way to do simple conditions.
- **Null Coalescing Operator (`??`)**: Returns the left-hand operand if it is not `null`, otherwise it returns the right operand.
- **Null Conditional Operator (`?.`)**: Safely access members and elements.

<br>

```csharp
int x = a > b ? a : b; // Ternary operator
string name = userName ?? "Guest"; // Null coalescing operator
int? length = array?.Length; // Null conditional operator
```