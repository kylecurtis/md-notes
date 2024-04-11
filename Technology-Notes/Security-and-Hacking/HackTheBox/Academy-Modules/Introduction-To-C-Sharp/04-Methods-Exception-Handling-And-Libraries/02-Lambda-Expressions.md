A lambda expression is a method without a name that calculates and returns a single value. They are simple methods to represent `anonymous methods` (methods without a name) or `functions` inline.

A lambda expression consists of three main parts: a `parameter list`, the `lambda operator` (`=>`), and an `expression or statement`. The general syntax for a lambda expression looks something like this:

```csharp
(parameters) => expression or statement block
```

- The `parameters` represent the input values to the lambda expression. They can be zero or more, separated by commas. If there is only one parameter, parentheses are optional. For multiple parameters, parentheses are required.
- The `lambda Operator (=>)` separates the parameter list from the body of the expression. It denotes a relationship between the parameters and the code to execute.
- The `expression or statement block` represents the code that is executed when the lambda expression is invoked. For a single expression, the result is implicitly returned. A statement block is enclosed in curly braces `{}` for multiple statements.

Consider the example given in the `LINQ` section.

```csharp
var evenNumbers = numbers.Where(num => num % 2 == 0); // Output: 2, 4, 6, 8, 10
```

The lambda expression `num => num % 2 == 0` specifies the condition for the `Where` method to filter the numbers. Here, `num` is the input parameter, and the condition to the right of the lambda operator is the statement block. This condition is applied to each element of the numbers list.

In plain English, this lambda expression reads, "For each number (num) in numbers, keep it if the remainder when num is divided by 2 equals 0." The % operator is the modulus operator, which gives the remainder of a division operation. Therefore, `num % 2 == 0` checks if a number is evenly divisible by 2, i.e., it's an even number.

## Simple Lambda Expression

Consider the following method.

```csharp
void Greet()
{
    Console.WriteLine("Hello, world!");
}

// Invoke the method
Greet(); // Output: Hello, world!
```

In this example, we merely define a method that prints a message to the console when invoked. However, we can further simplify this code using a lambda function, which essentially condenses it into a single line.

```csharp
// Lambda expression without parameters
var greet = () => Console.WriteLine("Hello, world!");
greet(); // Output: Hello, world!
```

In this instance, we've defined a lambda expression without any parameters. The lambda expression assigns a function to the variable `greet`, which prints "Hello, world!" to the console upon invocation.

While both achieve the same outcome, the lambda expression is far more succinct and can be employed as an inline function where required, contrasted with the method definition that necessitates a separate declaration.

## Lambda Expression with Parameters

A `Lambda Expression with Parameters` is a type of lambda expression in C# that takes one or more input parameters. This type of lambda expression is typically used when you want to perform an operation or evaluate a condition using the input parameters.

```csharp
// Regular method
int Add(int a, int b)
{
    return a + b;
}

// Lambda expression with parameters
var add = (int a, int b) => a + b;
int result = add(5, 3);
Console.WriteLine(result); // Output: 8
```

Here, we define a lambda expression with two parameters `a` and `b`, which adds the values of `a` and `b`. The lambda expression is assigned to the variable `add`, and we invoke it with arguments `5` and `3`, resulting in the sum `8` being assigned to the variable `result`.

## Lambda Expression with Statement Block

A `Lambda Expression with a Statement Block`, often called a `Statement Lambda`, is a type of lambda expression in C# that contains a block of code instead of a single expression on the right side of the lambda operator (`=>`).

```csharp
// Regular method
bool IsEven(int number)
{
    if (number % 2 == 0)
        return true;
    else
        return false;
}

// Lambda expression with statement block
var isEven = (int number) =>
{
    if (number % 2 == 0)
        return true;
    else
        return false;
};

bool even = isEven(6);
Console.WriteLine(even); // Output: True
```

In this example, we define a lambda expression with a parameter `number` and a statement block enclosed in curly braces. The lambda expression checks if the `number` is even and returns `true` or `false` accordingly. We assign the result of invoking the lambda expression with `6` to the variable `even`, which evaluates to `true`.