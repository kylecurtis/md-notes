<br>

Arrays in C# are a fundamental data structure that allows you to store a fixed-size sequential collection of elements of the same type. They are used to store collections of data in a single variable, and provide fast access to their elements.

<br>

---

<br>

## Declaration

<br>

Declaration is the stage where you specify the type and name of a variable without necessarily assigning any value to it. This tells the compiler about the existence of the variable and its type, so it can allocate the appropriate amount of memory space when the program runs.

<br>

```csharp
int[] emptyArray;
```

<br>

> NOTE: Here, `emptyArray` is declared as an array of integers, but no memory is allocated for it yet, nor does it hold any specific data.

<br>

---

<br>

## Instantiation

<br>

Instantiation involves allocating memory for the array on the heap. This is when the array object is actually created in memory. Instantiation can be separate from or combined with initialization.

<br>

```csharp
int[] myArray = new int[5];
```

<br>

> NOTE: `myArray` is instantiated with space for 5 integer elements. 
> 
> At this point, `myArray` is a non-null array, but each element is initialized to the default value for integers, which is 0.

<br>

---

<br>

## Inline Initialization

<br>

Initialization refers to the process of assigning initial values to the array. This can be done at the time of declaration, or after instantiation. You can initialize an array inline at the point of declaration, or you can assign values to its elements at a later time.

<br>

Inline initialization using legacy format:

```csharp
int[] myArray = new int[5] { 1, 2, 3, 4, 5 };
```

<br>

Inline initialization using a shorter format:

```csharp
int[] myArray = { 1, 2, 3, 4, 5 };
```

<br>

As of C# 12 (.NET8), you can also initialize inline elements using [Collection Expressions](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/collection-expressions) (recommended):


```csharp
int[] myArray = [ 1, 2, 3, 4, 5 ];
```


<br>

---

<br>


## Index Initialization

<br>

You can initialize all values within an array using their index `[i]`. 

<br>

```csharp
int[] numArray = new int[2];

numArray[0] = 1; // Initializing first element
numArray[1] = 2; // Initializing second element
```

<br>

> NOTE: C# uses 0-based indexing, meaning the first value in the array is always at index `[0]` by default.

<br>

---

<br>

## Accessing Array Elements

<br>

You can also access all values within an array using their index `[i]`.

<br>

```csharp
Console.WriteLine(myArray[0]); // Outputs: 1
Console.WriteLine(myArray[1];) // Outputs: 2
```

<br>

---

<br>

## Multi-Dimensional Arrays

<br>

C# supports multi-dimensional arrays, which are arrays with more than one dimension:

<br>

```csharp
int[,] matrix = new int[3,3]; // A 3x3 matrix

// Initialize the matrix
matrix[0, 0] = 1;
matrix[1, 1] = 2;
matrix[2, 2] = 3;

// Accessing elements
int element = matrix[1, 1]; // 2
```

<br>

---

<br>

## Jagged Arrays

<br>

Jagged arrays are arrays of arrays, and each "inner array" can be of different sizes:

<br>

```csharp
int[][] jaggedArray = new int[3][];
jaggedArray[0] = new int[3] { 1, 2, 3 };
jaggedArray[1] = new int[1] { 4 };
jaggedArray[2] = new int[2] { 5, 6 };

// Accessing a jagged array element
int jaggedElement = jaggedArray[0][1];  // 2
```

<br>

---

<br>

## Array Methods and Properties

<br>

Array methods in C# are built-in functions provided by the .NET Framework that allow developers to perform various operations on arrays, such as sorting, searching, modifying, and querying elements efficiently. 

These methods are part of the `System.Array` class and help facilitate common tasks involving array manipulation and management.

<br>

---

<br>

#### AsReadOnly()

- Namespace: System
- Description: Wraps the original array in a ReadOnlyCollection<T> to prevent any modifications to it.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
var readOnlyPlanets = Array.AsReadOnly(planets);
Console.WriteLine(readOnlyPlanets[2]); // Output: Earth
```

<br>

---

<br>

#### BinarySearch()

- Namespace: System
- Description: Searches for the specified object in a one-dimensional sorted array and returns the index of the object, if found.
- Example:

```csharp
string[] planets = { "Earth", "Jupiter", "Mars", "Mercury", "Neptune", "Saturn", "Uranus", "Venus" };
int index = Array.BinarySearch(planets, "Jupiter");
Console.WriteLine(index); // Output: 1
```

<br>

---

<br>

#### Clear()

- Namespace: System
- Description: Sets a range of elements in the array to zero, to false, or to null, depending on the element type.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
Array.Clear(planets, 1, 2);
Console.WriteLine(String.Join(", ", planets)); // Output: Mercury, , , Mars
```

<br>

---

<br>

#### Clone()

- Namespace: System
- Description: Creates a shallow copy of the array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
string[] planetsClone = (string[])planets.Clone();
Console.WriteLine(String.Join(", ", planetsClone)); // Output: Mercury, Venus, Earth, Mars
```

<br>

---

<br>

#### ConstrainedCopy()

- Namespace: System
- Description: Copies a range of elements from an array starting at a particular index to another array starting at a particular index, ensuring that all changes are reverted if the copy does not succeed completely.
- Example:

```csharp
string[] sourcePlanets = { "Mercury", "Venus", "Earth", "Mars" };
string[] targetPlanets = new string[4];
Array.ConstrainedCopy(sourcePlanets, 0, targetPlanets, 0, 4);
Console.WriteLine(String.Join(", ", targetPlanets)); // Output: Mercury, Venus, Earth, Mars
```

<br>

---

<br>

#### ConvertAll()

- Namespace: System
- Description: Converts an array of one type to an array of another type using the provided Converter<TInput,TOutput> delegate.
- Example:

```csharp
string[] planets = { "1", "2", "3", "4" };
int[] planetNumbers = Array.ConvertAll(planets, int.Parse);
Console.WriteLine(String.Join(", ", planetNumbers)); // Output: 1, 2, 3, 4
```

<br>

---

<br>

#### Copy()

- Namespace: System
- Description: Copies elements from the source array to the destination array, starting at a particular index in both.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
string[] planetsCopy = new string[4];
Array.Copy(planets, planetsCopy, planets.Length);
Console.WriteLine(String.Join(", ", planetsCopy)); // Output: Mercury, Venus, Earth, Mars
```

<br>

---

<br>

#### CopyTo()

- Namespace: System
- Description: Copies all the elements of the current one-dimensional array to the specified one-dimensional array starting at the specified destination array index.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
string[] destinationArray = new string[4];
planets.CopyTo(destinationArray, 0);
Console.WriteLine(String.Join(", ", destinationArray)); // Output: Mercury, Venus, Earth, Mars
```

<br>

---

<br>

#### CreateInstance()

- Namespace: System
- Description: Creates a new instance of an Array, specifying the type of its elements, the length of the Array, and optionally the lower bounds of each dimension.
- Example:

```csharp
Array planetsArray = Array.CreateInstance(typeof(string), 4);
planetsArray.SetValue("Mercury", 0);
planetsArray.SetValue("Venus", 1);
planetsArray.SetValue("Earth", 2);
planetsArray.SetValue("Mars", 3);
Console.WriteLine(String.Join(", ", planetsArray)); // Output: Mercury, Venus, Earth, Mars
```

<br>

---

<br>

#### Empty()

- Namespace: System
- Description: Returns an empty array of the specified type.
- Example:

```csharp
string[] emptyPlanets = Array.Empty<string>();
Console.WriteLine(emptyPlanets.Length); // Output: 0
```

<br>

---

<br>

#### Exists()

- Namespace: System
- Description: Determines whether an element that matches the conditions defined by the specified predicate exists within the array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
bool hasEarth = Array.Exists(planets, planet => planet == "Earth");
Console.WriteLine(hasEarth); // Output: True
```

<br>

---

<br>

#### Fill()

- Namespace: System
- Description: Fills all elements of an array with the same value.
- Example:

```csharp
string[] planets = new string[5];
Array.Fill(planets, "Pluto");
Console.WriteLine(String.Join(", ", planets)); // Output: Pluto, Pluto, Pluto, Pluto, Pluto
```

<br>

---

<br>

#### Find()

- Namespace: System
- Description: Searches for an element that matches the conditions defined by the specified predicate, and returns the first occurrence within the entire one-dimensional array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
string foundPlanet = Array.Find(planets, planet => planet.StartsWith("M"));
Console.WriteLine(foundPlanet); // Output: Mercury
```

<br>

---

<br>

#### FindAll()

- Namespace: System
- Description: Retrieves all the elements that match the conditions defined by the specified predicate.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars", "Jupiter" };
string[] mPlanets = Array.FindAll(planets, planet => planet.StartsWith("M"));
Console.WriteLine(String.Join(", ", mPlanets)); // Output: Mercury, Mars
```

<br>

---

<br>

#### FindIndex()

- Namespace: System
- Description: Searches for an element that matches the conditions defined by a specified predicate and returns the zero-based index of the first occurrence within the range of elements in the one-dimensional array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
int index = Array.FindIndex(planets, planet => planet == "Earth");
Console.WriteLine(index); // Output: 2
```

<br>

---

<br>

#### FindLast()

- Namespace: System
- Description: Searches for an element that matches the conditions defined by the specified predicate and returns the last occurrence within the entire one-dimensional array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars", "Earth" };
string lastEarth = Array.FindLast(planets, planet => planet == "Earth");
Console.WriteLine(lastEarth); // Output: Earth
```

<br>

---

<br>

#### FindLastIndex()

- Namespace: System
- Description: Searches for an element that matches the conditions defined by the specified predicate and returns the zero-based index of the last occurrence within the range of elements in the one-dimensional array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars", "Earth" };
int lastIndex = Array.FindLastIndex(planets, planet => planet == "Earth");
Console.WriteLine(lastIndex); // Output: 4
```

<br>

---

<br>

#### ForEach()

- Namespace: System
- Description: Performs the specified action on each element of the specified array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
Array.ForEach(planets, planet => Console.WriteLine(planet));
```

<br>

---

<br>

#### GetEnumerator()

- Namespace: System
- Description: Returns an IEnumerator for the array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
IEnumerator enumerator = planets.GetEnumerator();
while (enumerator.MoveNext()) {
    Console.WriteLine(enumerator.Current); // Output: Mercury, Venus, Earth, Mars
}
```

<br>

---

<br>

#### GetLength()

- Namespace: System
- Description: Gets a 32-bit integer that represents the number of elements in the specified dimension of the Array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
int length = planets.GetLength(0);
Console.WriteLine(length); // Output: 4
```

<br>

---

<br>

#### GetLongLength()

- Namespace: System
- Description: Gets a 64-bit integer that represents the number of elements in the specified dimension of the Array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
long longLength = planets.GetLongLength(0);
Console.WriteLine(longLength); // Output: 4
```

<br>

---

<br>

#### GetLowerBound()

- Namespace: System
- Description: Gets the lower bound of the specified dimension in the array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
int lowerBound = planets

.GetLowerBound(0);
Console.WriteLine(lowerBound); // Output: 0
```

<br>

---

<br>

#### GetUpperBound()

- Namespace: System
- Description: Gets the upper bound of the specified dimension in the array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
int upperBound = planets.GetUpperBound(0);
Console.WriteLine(upperBound); // Output: 3
```

<br>

---

<br>

#### GetValue()

- Namespace: System
- Description: Gets the value at the specified position in the one-dimensional Array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
object value = planets.GetValue(2);
Console.WriteLine(value); // Output: Earth
```

<br>

---

<br>

#### IndexOf()

- Namespace: System
- Description: Searches for the specified object and returns the index of the first occurrence within the entire one-dimensional array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
int index = Array.IndexOf(planets, "Earth");
Console.WriteLine(index); // Output: 2
```

<br>

---

<br>

#### Initialize()

- Namespace: System
- Description: Initializes every element of the value-type Array by calling the parameterless constructor of the value type.
- Example:

```csharp
int[] numbers = new int[5];
Array.Initialize(numbers);
Console.WriteLine(String.Join(", ", numbers)); // Output: 0, 0, 0, 0, 0
```

<br>

---

<br>

#### LastIndexOf()

- Namespace: System
- Description: Searches for the specified object and returns the index of the last occurrence within the entire one-dimensional array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars", "Earth" };
int lastIndex = Array.LastIndexOf(planets, "Earth");
Console.WriteLine(lastIndex); // Output: 4
```

<br>

---

<br>

#### Resize()

- Namespace: System
- Description: Changes the size of a one-dimensional array to the specified new size.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth" };
Array.Resize(ref planets, 5);
planets[3] = "Mars";
planets[4] = "Jupiter";
Console.WriteLine(String.Join(", ", planets)); // Output: Mercury, Venus, Earth, Mars, Jupiter
```

<br>

---

<br>

#### Reverse()

- Namespace: System
- Description: Reverses the sequence of the elements in the entire one-dimensional array or in the specified range of the array.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
Array.Reverse(planets);
Console.WriteLine(String.Join(", ", planets)); // Output: Mars, Earth, Venus, Mercury
```

<br>

---

<br>

#### SetValue()

- Namespace: System
- Description: Sets a value to the element at the specified position in the one-dimensional Array.
- Example:

```csharp
string[] planets = new string[4];
planets.SetValue("Mercury", 0);
planets.SetValue("Venus", 1);
planets.SetValue("Earth", 2);
planets.SetValue("Mars", 3);
Console.WriteLine(String.Join(", ", planets)); // Output: Mercury, Venus, Earth, Mars
```

<br>

---

<br>

#### Sort()

- Namespace: System
- Description: Sorts the elements in an entire one-dimensional array using the IComparable interface of each element of the Array.
- Example:

```csharp
string[] planets = { "Mars", "Earth", "Venus", "Mercury" };
Array.Sort(planets);
Console.WriteLine(String.Join(", ", planets)); // Output: Earth, Mars, Mercury, Venus
```

<br>

---

<br>

#### TrueForAll()

- Namespace: System
- Description: Determines whether every element in the array matches the conditions defined by the specified predicate.
- Example:

```csharp
string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
bool allStartWithM = Array.TrueForAll(planets, planet => planet.StartsWith("M"));
Console.WriteLine(allStartWithM); // Output: False
```

<br>

---

<br>

## Using ArrayList

<br>

Before generics were introduced with .NET 2.0, the `ArrayList` class was commonly used. It can hold items of any type and automatically expands as you add items.

<br>

```csharp
ArrayList myArrayList = new ArrayList();
myArrayList.Add(1);
myArrayList.Add("Two");
myArrayList.Add(3.0);

// Accessing elements
int firstElement = (int)myArrayList[0]; // Need to cast since ArrayList stores objects
```

<br>

> NOTE: It's generally better to use `List<T>` from the `System.Collections.Generic` namespace because it's type-safe and generally more efficient than `ArrayList`.

<br>

---

<br>

## Best Practices

<br>

- **Use Specific Types**: Prefer `List<T>` over `ArrayList` for type safety and performance.
- **Know Your Needs**: Use multi-dimensional arrays for matrices or tables, and jagged arrays when dealing with data of varying lengths.
- **Initialize Upon Declaration**: When possible, initialize your array upon declaration to make the code cleaner and easier to understand.