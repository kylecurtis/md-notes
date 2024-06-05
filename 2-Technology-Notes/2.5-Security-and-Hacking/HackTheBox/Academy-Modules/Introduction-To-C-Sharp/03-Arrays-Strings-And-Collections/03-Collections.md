In C#, a collection is used to group related objects. Collections provide a more flexible way to work with groups of objects, as unlike arrays, the group of objects you work with can grow and shrink dynamically as the demands of the application change. Collections are defined in the `System.Collections` namespace.

## Iterating through a collection

The `foreach` loop is an efficient and straightforward way to iterate through any collection. It automatically moves to the next item in the collection at the end of each loop iteration, making it an excellent choice for reading collections. Suppose you want to modify the collection while iterating over it. In that case, you might need to use a different looping construct, like a `for` loop, as `foreach` does not support collection modification during iteration.

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

for (int i = 0; i < numbers.Count; i++)
{
    // Modify the element at index i
    numbers[i] *= 2;
}

foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

We use a `for` loop to iterate over the numbers list in this example. The loop variable `i` represents the index of each element in the list. Within the loop, we can modify the element at the current index by performing the desired operation, in this case, multiplying it by 2. After the `for` loop completes, we use a `foreach` loop to iterate over the modified `numbers` list and print each number to the console.

## List

A `List<T>` is one of the most commonly used types in .NET, especially when we need a resizable array-like collection. This type is found in the `System.Collections.Generic` namespace is a generic class which supports storing values of any type. However, all `List<T>` elements must be the same type.

```csharp
List<string> namesList = new List<string>();

// Adding elements to the list
namesList.Add("John");
namesList.Add("Jane");
namesList.Add("Alice");

// Accessing elements by index
string firstElement = namesList[0]; // O(1) indexed access

// Modifying an element
namesList[1] = "Emily";

// Checking if an element exists
bool hasAlice = namesList.Contains("Alice");

// Removing an element
namesList.Remove("John");

// Iterating over the elements
foreach (string name in namesList)
{
    Console.WriteLine(name);
}
```

A `List<T>` provides the advantage of dynamic resizing compared to an array. However, this also means that a `List<T>` generally uses more memory than an array, as it allocates extra space to allow for potential growth. If the size of your collection is fixed, using an array could be more memory-efficient.

However, the flexibility and utility of the `List<T>` class methods often outweigh the minor performance and memory usage benefits of arrays in many scenarios. This is especially true in applications where the exact count of elements may change over time.

## Dictionary

A `Dictionary<TKey, TValue>` is a collection that stores and retrieves data using a key-value relationship. It is part of the `System.Collections.Generic` namespace in C#.

To use a `Dictionary<TKey, TValue>`, specify the key type (`TKey`) and the value (`TValue`) in the angle brackets. For example, `Dictionary<int, string>` indicates a dictionary where the keys are integers and the values are strings.

```csharp
Dictionary<string, int> studentGrades = new Dictionary<string, int>();

// Adding key-value pairs to the dictionary
studentGrades.Add("John", 85);
studentGrades.Add("Jane", 92);
studentGrades.Add("Alice", 78);

// Accessing values by key
int johnGrade = studentGrades["John"]; // O(1) lookup by key

// Modifying an existing value
studentGrades["Jane"] = 95;

// Checking if a key exists
bool hasAlice = studentGrades.ContainsKey("Alice");

// Removing a key-value pair
studentGrades.Remove("John");

// Iterating over the key-value pairs
foreach (KeyValuePair<string, int> pair in studentGrades)
{
    Console.WriteLine($"Name: {pair.Key}, Grade: {pair.Value}");
}
```

## HashSet

A `HashSet<T>` collection stores an unordered set of unique elements. The primary characteristic of a `HashSet` is its ability to store unique elements, completely disallowing duplication. Adding elements to a `HashSet` will check if the element already exists before adding it. This makes `HashSet` an optimal choice when you need to store a collection of items without any duplicates and do not require a specific order.

To use a `HashSet`, specify the type of elements (`T`) within the angle brackets. For example, `HashSet<int>` indicates a set of integers.

```csharp
HashSet<string> namesHashSet = new HashSet<string>();

// Adding elements to the set
namesHashSet.Add("John");
namesHashSet.Add("Jane");
namesHashSet.Add("Alice");

// Checking if an element exists
bool hasAlice = namesHashSet.Contains("Alice"); // O(1) membership check

// Removing an element
namesHashSet.Remove("John");

// Iterating over the elements
foreach (string name in namesHashSet)
{
    Console.WriteLine(name);
}
```

## List vs Dictionary vs HashSet

Each collection type has its unique characteristics, behaviours, and use cases.

||List|Dictionary|HashSet|
|---|---|---|---|
|Data Structure|Ordered|Key-Value Pairs|Unordered, Unique Elements|
|Duplication|Allows duplicates|Keys must be unique|Ensures uniqueness|
|Access and Lookup|Indexed access by index|Fast lookup by unique key|Membership checks|
|Ordering|Maintains order|No specific order|No specific order|
|Element Removal|By index or value|By key|By value|
|Memory Overhead|Consumes memory based on elements|Memory for keys and values|Memory for unique elements|
|Use Cases|Ordered collection, indexed access|Associating values with keys, key-based lookup|Unordered collection, uniqueness and membership checks|

## Collection Performance

Performance considerations vary for each collection type based on the operations performed and the specific use case.

`Big-O notation` is a notation used in computer science to describe the performance characteristics of an algorithm, specifically its time complexity and space complexity.

In terms of time complexity, `Big-O notation` quantifies the worst-case scenario of an algorithm as the size of the input data approaches infinity. For instance, if an algorithm has a time complexity of `O(n)`, it indicates that the time it takes to execute the algorithm grows linearly with the input data size. On the other hand, an algorithm with a time complexity of `O(n^2)` would suggest that the execution time increases quadratically with the input size.

While analysed less frequently, `Big-O` notation can also describe space complexity by measuring the amount of memory an algorithm needs relative to the input size. For example, an algorithm with a space complexity of `O(1)` uses a constant amount of memory regardless of the input size.

Here are some general performance considerations for `List`, `Dictionary`, and `HashSet`:

||List|Dictionary|HashSet|
|---|---|---|---|
|Access Speed|Very fast, O(1)|Average: O(1), Worst: O(n)|Average: O(1), Worst: O(n)|
|Insertion/Removal|Insertion and removal at ends: O(1)|Average: O(1), Worst: O(n)|Average: O(1), Worst: O(n)|
|Searching|Unsorted: O(n)  <br>Sorted (Binary Search): O(log n)|Key-based lookup: Average O(1), Worst O(n)|Membership check: Average O(1), Worst O(n)|
|Memory Overhead|Relatively low|Keys and values, additional structure fields|Unique elements, additional structure fields|

Please note that the access speed represents the time complexity of accessing elements in the collection, whether it's by index (for List) or by key (for Dictionary) or membership check (for HashSet). The performance characteristics in this table are general guidelines and may vary based on the specific implementation and use case.