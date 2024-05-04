---
tags: [csharp]
---

Lists in C# are part of the `System.Collections.Generic` namespace and provide a flexible way to work with a collection of objects. Unlike arrays, lists do not have a fixed size and can dynamically increase or decrease as needed. They are a powerful tool for managing data where the number of elements can vary dynamically.

<br>

---

<br>

## Declaration

<br>

Declaration involves specifying the type of elements the list will hold. This is done using generics.

<br>

```csharp
List<int> numbers;
```

<br>

> NOTE: Here, `numbers` is declared as a list that will store integers.

<br>

---

<br>

## Instantiation

<br>

To use the list, you must instantiate it using the `new` keyword. This step creates an instance of the list in memory.

```csharp
List<int> numbers = new List<int>();
```

<br>

> NOTE: This instantiation creates an empty list ready to store integer elements.

<br>

---

<br>

## Adding Elements

<br>

Elements can be added to the list using the `Add` method. This method appends the element to the end of the list.

```csharp
numbers.Add(1); // Adds 1 to the list
numbers.Add(2); // Adds 2 to the list
```

<br>

> NOTE: Lists can dynamically resize. Adding elements is efficient, especially when the size increases predictably.

<br>

---

<br>

## Accessing Elements

<br>

Elements in a list can be accessed via their index, similar to arrays.

```csharp
int firstNumber = numbers[0]; // Accesses the first element, 1
Console.WriteLine(firstNumber);
```

<br>

> NOTE: Like arrays, lists are zero-indexed.

<br>

---

<br>

## Removing Elements

<br>

Elements can be removed by their value or index. `Remove` removes the first occurrence of a specific value, while `RemoveAt` removes an element at a specified index.

<br>

```csharp
numbers.Remove(1); // Removes the first occurrence of 1
numbers.RemoveAt(0); // Removes the element at index 0
```

<br>

---

<br>

## Iterating Through Lists

<br>

Lists can be iterated using a `foreach` loop, which provides a simple way to access each element.

<br>

```csharp
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

<br>

---

<br>

## Capacity and Count

<br>

`Capacity` refers to the number of elements the list can store before needing to resize, while `Count` is the number of elements currently in the list.

<br>

```csharp
Console.WriteLine($"Capacity: {numbers.Capacity}");
Console.WriteLine($"Count: {numbers.Count}");
```

<br>

> NOTE: When `Count` exceeds `Capacity`, the capacity automatically increases, typically doubling each time.

<br>

---

<br>

## Sorting and Searching

<br>

Lists can be sorted using the `Sort` method and searched using methods like `Contains`, `IndexOf`, and `Find`.

<br>

```csharp
numbers.Sort(); // Sorts the list
bool containsThree = numbers.Contains(3); // Checks if the list contains 3
int indexOfThree = numbers.IndexOf(3); // Finds the index of 3, returns -1 if not found
```

<br>

> NOTE: Sorting a list is an O(n log n) operation.

<br>

---

<br>

## Converting Arrays to Lists and Vice Versa

<br>

Lists can be easily converted to arrays and vice versa, providing flexibility in how data is managed and utilized.

<br>

```csharp
int[] array = numbers.ToArray(); // Converts list to array
List<int> newList = new List<int>(array); // Creates a list from an array
```