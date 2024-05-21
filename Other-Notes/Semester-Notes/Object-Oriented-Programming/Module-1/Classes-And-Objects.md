
## Class

- A class in Java is like a blueprint.
- It defines ta type of object, describing what attributes (or fields) the object will have and what actions (or methods) it can perform.
- Think of it as a template.

<br>

Attributes of the class should be private (- sign when using UML), so that it can only be accessed by the methods of the particular class.

<br>

## Object

- An object is an instance of a class.
- When we create an object, we're using the blueprint provided by the class to make something concrete.

<br>

## Method

- A method is a block of code within a class that performs a specific task.
- It's like a function, but it belongs to a class.

Methods of the class should be public (+ sign when using UML), so that it can be accessed by other classes.

<br>

---

<br>

## Key Definitions

- *Instantiation*: This is the process of creating a new object from a class.
- *Attribute (Or Field)*: Attributes are the properties that objects of a class have.
- *UML Diagram*: This is a visual representation of a class, showing it's attributes and methods. It's a great way to understand the structure of a class at a glance.
- *Constructor*: Allows you to set initial values when you instantiate a class.

<br>

---

<br>

## Get and Set Methods

- *Get Methods*: Returns the value of the attribute.
- *Set Methods*: Allows you to change the values of the attributes.

<br>

---

<br>

## Code Examples

<br>

Person Class

```java
public class Person {
	private String name; // name attribute
	private int age; // age attribute

	// Default Constructor
	public Person() {
		this.name = "Unknown";
		this.age = 0;
	}

	// Parameterized Constructor
	public Person (String name, int age) {
		this.name = name;
		this.age = age;
	}

	// Getter Method (name)
	public String getName() {
		return name;
	}

	// Setter Method (name)
	public String setName(String name) {
		this.name = name;
	}

	// Getter Method (age)
	public int getAge() {
		return age;
	}

	public int setAge(int age) {
		this.age = age;
	}

	// Method To Display Details
	public void displayPerson() {
		System.out.println("Name: " + name + ", Age: " + age);
	}
}
```

#### Key Notes

- Getter methods return the value.
- Setter methods take the value as input and set the value to the input.

<br>

MainApp

```java
public class MainApp {
	public static void main(String[] args) {
		// Default Constructor
		Person person1 = new Persion(); // "Unknown", 0

		// Parameterized Constructor
		Person person2 = new Person("Bob", 30);

		// Getter & Setter Methods
		person1.setName("Jack"); // Set
		person1.setAge("32"); // Set
		System.out.println(person1.getName() + " " + person1.getAge()); // Get

		// Method
		person1.displayPerson();
	}
}
```