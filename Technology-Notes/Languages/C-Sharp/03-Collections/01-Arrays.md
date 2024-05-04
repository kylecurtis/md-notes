---
tags: [csharp]
---

Arrays in C# are a fundamental data structure used to store a fixed-size sequential collection of elements of the same type. They allow efficient indexed access to elements and are an essential part of data management in software development.

<br>

---

<br>

## Declaration

<br>

Declaration involves specifying the type and name of an array without assigning it a value. This informs the compiler about the array's existence and type, enabling it to allocate memory during execution.

<br>

```csharp
int[] emptyArray;
```

<br>

> NOTE: Here, `emptyArray` is declared as an array of integers. No memory is allocated, and it contains no elements until instantiated.

<br>

---

<br>

## Instantiation

<br>

Instantiation is the process of allocating memory on the heap for the array, effectively creating the array object.

<br>

```csharp
int[] myArray = new int[5];
```

<br>

> NOTE: `myArray` allocates memory for five integer elements, each initialized to the default integer value of 0.

<br>

---

<br>

## Inline Initialization

<br>

Initialization can occur at the point of declaration (inline) or after instantiation. Inline initialization directly assigns values to the array.

<br>

Legacy format:

```csharp
int[] myArray = new int[5] { 1, 2, 3, 4, 5 };
```

<br>

Shorter format:

```csharp
int[] myArray = { 1, 2, 3, 4, 5 };
```

<br>

With C# 12 (.NET8) or higher, use [Collection Expressions](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/collection-expressions):

```csharp
int[] myArray = [ 1, 2, 3, 4, 5 ];
```

<br>

---

<br>

## Index Initialization

<br>

Arrays can also be initialized using indices:

```csharp
int[] numArray = new int[2];
numArray[0] = 1; // First element
numArray[1] = 2; // Second element
```

<br>

> NOTE: C# arrays are zero-indexed, the first element is at index `0`.

<br>

---

<br>

## Accessing Array Elements

<br>

Elements can be accessed using their index:

```csharp
Console.WriteLine(myArray[0]); // 1
Console.WriteLine(myArray[1]); // 2
```

<br>

---

<br>

## Multi-Dimensional Arrays

<br>

Multi-dimensional arrays allow storing data in a matrix form:

```csharp
int[,] matrix = new int[3,3];  // A 3x3 matrix

matrix[0, 0] = 1;
matrix[1, 1] = 2;
matrix[2, 2] = 3;

int element = matrix[1, 1]; // Accessing the middle element, 2
```

<br>

---

<br>

## Jagged Arrays

<br>

Jagged arrays are arrays of arrays, with each "inner array" potentially differing in size:

```csharp
int[][] jaggedArray = new int[3][];
jaggedArray[0] = [ 1, 2, 3 ];
jaggedArray[1] = [ 4 ];
jaggedArray[2] = [ 5, 6 ];

int jaggedElement = jaggedArray[0][1]; // Accesses the second element of the first array
Console.WriteLine(jaggedElement); // 2
```

<br>

---

<br>


## Array Methods

<br>

Array methods provide a wide range of functionalities, allowing manipulation, querying, and transformation of arrays. 

Here's a detailed overview of some essential array methods:

<br>

---

<br>

#### AsReadOnly()

- **Namespace**: `System`
- **Description**: Wraps the original array in a `ReadOnlyCollection<T>` to prevent any modifications.
- **Example**:

	```csharp
	string[] planets = [ "Mercury", "Venus", "Earth", "Mars" ];
	var readOnlyPlanets = Array.AsReadOnly(planets);
  
	Console.WriteLine(readOnlyPlanets[2]); // Earth
	```

<br>

---

<br>

#### BinarySearch()

- **Namespace**: `System`
- **Description**: Searches for a specific object in a sorted one-dimensional array and returns the index of the object if found.
- **Example**:

	```csharp
	string[] planets = [ "Earth", "Jupiter", "Mars", "Mercury", "Neptune", "Saturn", "Uranus", "Venus" ];
	int index = Array.BinarySearch(planets, "Jupiter");
  
	Console.WriteLine(index); // 1
	```

<br>

---

<br>

#### Clear()

- **Namespace**: `System`
- **Description**: Sets a range of elements in the array to zero, false, or null, depending on the element type.
- **Example**:

	```csharp
	string[] planets = [ "Mercury", "Venus", "Earth", "Mars" ];
	Array.Clear(planets, 1, 2);
  
	Console.WriteLine(string.Join(", ", planets)); // Mercury, , , Mars
	```

<br>

---

<br>

#### Clone()

- **Namespace**: `System`
- **Description**: Creates a shallow copy of the array.
- **Example**:

	```csharp
	string[] planets = [ "Mercury", "Venus", "Earth", "Mars" ];
	string[] planetsClone = (string[])planets.Clone();
  
	Console.WriteLine(string.Join(", ", planetsClone)); // Mercury, Venus, Earth, Mars
	```

<br>

---

<br>

#### ConstrainedCopy()

- **Namespace**: `System`
- **Description**: Copies a range of elements from one array to another, ensuring that all changes are reverted if the copy does not complete successfully.
- **Example**:

	```csharp
	string[] sourcePlanets = { "Mercury", "Venus", "Earth", "Mars" };
	string[] targetPlanets = new string[4];
	Array.ConstrainedCopy(sourcePlanets, 0, targetPlanets, 0, 4);

	Console.WriteLine(string.Join(", ", targetPlanets)); // Mercury, Venus, Earth, Mars
	```

<br>

---

<br>

#### ConvertAll()

- **Namespace**: `System`
- **Description**: Converts an array of one type to another type using the provided `Converter<TInput,TOutput>` delegate.
- **Example**:

	```csharp
	string[] planets = [ "1", "2", "3", "4" ];
	int[] planetNumbers = Array.ConvertAll(planets, int.Parse);
	
	Console.WriteLine(string.Join(", ", planetNumbers)); // 1, 2, 3, 4
	```

<br>

---

<br>

#### Copy()

- **Namespace**: `System`
- **Description**: Copies elements from the source array to the destination array starting at a specified index.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	string[] planetsCopy = new string[4];
	Array.Copy(planets, planetsCopy, planets.Length);
	
	Console.WriteLine(string.Join(", ", planetsCopy)); // Mercury, Venus, Earth, Mars
	```

<br>

---

<br>

#### CopyTo()

- **Namespace**: `System`
- **Description**: Copies all elements of the current one-dimensional array to a specified array starting at the specified destination index.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	string[] destinationArray = new string[4];
	planets.CopyTo(destinationArray, 0);
  
	Console.WriteLine(string.Join(", ", destinationArray)); // Mercury, Venus, Earth, Mars
	```

<br>

---

<br>

#### CreateInstance()

- **Namespace**: `System`
- **Description**: Creates a new instance of an Array, specifying the type of its elements and the length of the Array, with optional lower bounds for each dimension.
- **Example**:

	```csharp
	Array planetsArray = Array.CreateInstance(typeof(string), 4);
	planetsArray.SetValue("Mercury", 0);
	planetsArray.SetValue("Venus", 1);
	planetsArray.SetValue("Earth", 2);
	planetsArray.SetValue("Mars", 3);
  
	Console.WriteLine(string.Join(", ", planetsArray)); // Mercury, Venus, Earth, Mars
	```

<br>

---

<br>

#### Empty()

- **Namespace**: `System`
- **Description**: Returns an empty array of the specified type.
- **Example**:

	```csharp
	string[] emptyPlanets = Array.Empty<string>();
	Console.WriteLine(emptyPlanets.Length); // 0
	```

<br>

---

<br>

#### Exists()

- **Namespace**: `System`
- **Description**: Determines if any element in the array satisfies a condition defined by the specified predicate.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	bool hasEarth = Array.Exists(planets, planet => planet == "Earth");
	
	Console.WriteLine(hasEarth); // True
	```

<br>

---

<br>

#### Fill()

- **Namespace**: `System`
- **Description**: Fills all elements of an array with a specified value.
- **Example**:

	```csharp
	string[] planets = new string[5];
	Array.Fill(planets, "Pluto");
	
	Console.WriteLine(string.Join(", ", planets)); // Pluto, Pluto, Pluto, Pluto, Pluto
	```

<br>

---

<br>

#### Find()

- **Namespace**: `System`
- **Description**: Searches for an element that meets the conditions defined by a specified predicate, returning the first occurrence within the entire one-dimensional array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	string foundPlanet = Array.Find(planets, planet => planet.StartsWith("M"));
	
	Console.WriteLine(foundPlanet); // Mercury
	```

<br>

---

<br>

#### FindAll()

- **Namespace**: `System`
- **Description**: Retrieves all elements that meet the conditions defined by the specified predicate.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars", "Jupiter" };
	string[] mPlanets = Array.FindAll(planets, planet => planet.StartsWith("M"));
  
	Console.WriteLine(string.Join(", ", mPlanets)); // Mercury, Mars
	```

<br>

---

<br>

#### FindIndex()

- **Namespace**: `System`
- **Description**: Searches for an element that matches the conditions defined by a specified predicate and returns the zero-based index of the first occurrence within the range of elements in the array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	int index = Array.FindIndex(planets, planet => planet == "Earth");
	
	Console.WriteLine(index); // 2
	```

<br>

---

<br>

#### FindLast()

- **Namespace**: `System`
- **Description**: Searches for the last element that matches the conditions defined by a specified predicate within the array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars", "Earth" };
	string lastEarth = Array.FindLast(planets, planet => planet == "Earth");
	
	Console.WriteLine(lastEarth); // Earth
	```

<br>

---

<br>

#### FindLastIndex()

- **Namespace**: `System`
- **Description**: Searches for an element that matches the conditions defined by a specified predicate and returns the zero-based index of the last occurrence within the range of elements in the array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars", "Earth" };
	int lastIndex = Array.FindLastIndex(planets, planet => planet == "Earth");
	
	Console.WriteLine(lastIndex); // 4
	```

<br>

---

<br>

#### ForEach()

- **Namespace**: `System`
- **Description**: Executes a specified action on each element of the array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	Array.ForEach(planets, planet => Console.WriteLine(planet));
	```

<br>

---

<br>

#### GetEnumerator()

- **Namespace**: `System`
- **Description**: Returns an `IEnumerator` for the array, allowing iteration over the array's elements.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	IEnumerator enumerator = planets.GetEnumerator();
	
	while (enumerator.MoveNext()) {
		Console.WriteLine(enumerator.Current); // Mercury, Venus, Earth, Mars
	}
	```

<br>

---

<br>

#### GetLength()

- **Namespace**: `System`
- **Description**: Retrieves the number of elements in a specified dimension of the array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	int length = planets.GetLength(0);
	
	Console.WriteLine(length); // 4
	```

<br>

---

<br>

#### GetLongLength()

- **Namespace**: `System`
- **Description**: Gets a 64-bit integer representing the number of elements in a specified dimension of the Array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	long longLength = planets.GetLongLength(0);
	
	Console.WriteLine(longLength); // 4
	```

<br>

---

<br>

#### GetLowerBound()

- **Namespace**: `System`
- **Description**: Retrieves the lower bound of the specified dimension in the array, typically zero for zero-based indexing.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	int lowerBound = planets.GetLowerBound(0);
	
	Console.WriteLine(lowerBound); // 0
	```

<br>

---

<br>

#### GetUpperBound()

- **Namespace**: `System`
- **Description**: Returns the upper bound (maximum index) of the specified dimension in the array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	int upperBound = planets.GetUpperBound(0);
	
	Console.WriteLine(upperBound); // 3
	```

<br>

---

<br>

#### GetValue()

- **Namespace**: `System`
- **Description**: Retrieves the value at the specified position in the one-dimensional array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	object value = planets.GetValue(2);
	
	Console.WriteLine(value); // Earth
	```

<br>

---

<br>

#### IndexOf()

- **Namespace**: `System`
- **Description**: Searches for the specified object and returns the index of its first occurrence within the entire one-dimensional array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	int index = Array.IndexOf(planets, "Earth");
	
	Console.WriteLine(index); // 2
	```

<br>

---

<br>

#### Initialize()

- **Namespace**: `System`
- **Description**: Initializes every element of a value-type array by calling the parameterless constructor of the value type.
- **Example**:

	```csharp
	int[] numbers = new int[5];
	Array.Initialize(numbers);
	
	Console.WriteLine(string.Join(", ", numbers)); // 0, 0, 0, 0, 0
	```

<br>

---

<br>

#### LastIndexOf()

- **Namespace**: `System`
- **Description**: Searches for the specified object and returns the index of its last occurrence within the entire one-dimensional array.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars", "Earth" };
	int lastIndex = Array.LastIndexOf(planets, "Earth");
	
	Console.WriteLine(lastIndex); // 4
	```

<br>

---

<br>

#### Resize()

- **Namespace**: `System`
- **Description**: Resizes a one-dimensional array to the specified new size.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth" };
	Array.Resize(ref planets, 5);
	planets[3] = "Mars";
	planets[4] = "Jupiter";
	
	Console.WriteLine(string.Join(", ", planets)); // Mercury, Venus, Earth, Mars, Jupiter
	```

<br>

---

<br>

#### Reverse()

- **Namespace**: `System`
- **Description**: Reverses the sequence of elements in the entire one-dimensional array or a portion of it.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	Array.Reverse(planets);
	
	Console.WriteLine(string.Join(", ", planets)); // Mars, Earth, Venus, Mercury
	```

<br>

---

<br>

#### SetValue()

- **Namespace**: `System`
- **Description**: Assigns a specified value to the element at the indicated position in a one-dimensional array.
- **Example**:

	```csharp
	string[] planets = new string[4];
	planets.SetValue("Mercury", 0);
	planets.SetValue("Venus", 1);
	planets.SetValue("Earth", 2);
	planets.SetValue("Mars", 3);
	
	Console.WriteLine(string.Join(", ", planets)); // Mercury, Venus, Earth, Mars
	```

<br>

---

<br>

#### Sort()

- **Namespace**: `System`
- **Description**: Sorts the elements in an entire one-dimensional array using the `IComparable` interface of each element of the array.
- **Example**:

	```csharp
	string[] planets = { "Mars", "Earth", "Venus", "Mercury" };
	Array.Sort(planets);
	
	Console.WriteLine(string.Join(", ", planets)); // Earth, Mars, Mercury, Venus
	```

<br>

---

<br>

#### TrueForAll()

- **Namespace**: `System`
- **Description**: Determines whether every element of the array matches the conditions defined by the specified predicate.
- **Example**:

	```csharp
	string[] planets = { "Mercury", "Venus", "Earth", "Mars" };
	bool allStartWithM = Array.TrueForAll(planets, planet => planet.StartsWith("M"));
	
	Console.WriteLine(allStartWithM); // False
	```

<br>

---

<br>


