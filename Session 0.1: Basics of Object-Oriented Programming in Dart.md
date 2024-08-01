## Lecture: Basics of Object-Oriented Programming in Dart

### Introduction to Dart

Dart is a client-optimized language designed for fast apps on any platform. It is developed by Google and is particularly used for building mobile, desktop, server, and web applications. Dart is known for its strong support for OOP principles, which allows developers to create robust and maintainable code.

### Object-Oriented Programming (OOP)

OOP is a programming paradigm based on the concept of "objects," which are instances of classes. It allows for the structuring of software in a way that is both modular and reusable.

### Key Concepts in OOP

1. **Class**: A blueprint for creating objects, encapsulating data for the object and methods to manipulate that data.
2. **Object**: An instance of a class.
3. **Instance**: A specific realization of an object.
4. **Method**: Functions defined inside a class that describe the behaviors of the objects created from the class.
5. **Constructor**: A special method that is called when an object is instantiated.

### Class and Object in Dart

A class is defined using the `class` keyword. Here’s how you can define a simple class in Dart:

#### Defining a Class

```dart
class Person {
  String name;
  int age;

  // Constructor
  Person(this.name, this.age);
}
```

#### Creating an Object (Instance) of a Class

```dart
void main() {
  // Creating an instance of the Person class
  Person person = Person('John Doe', 25);
  print('Name: ${person.name}, Age: ${person.age}');
}
```

### Methods in Dart

Methods are functions defined within a class that operate on instances of that class.

#### Adding Methods to a Class

```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  // Method to display person's details
  void displayInfo() {
    print('Name: $name, Age: $age');
  }
}

void main() {
  Person person = Person('John Doe', 25);
  person.displayInfo();
}
```

### Constructors in Dart

Constructors are special methods invoked when an object is created. They initialize the object’s properties.

#### Default Constructor

```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age); // Default constructor
}

void main() {
  Person person = Person('John Doe', 25);
  person.displayInfo();
}
```

#### Named Constructor

```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  // Named constructor
  Person.withName(this.name) : age = 0;
}

void main() {
  Person person = Person.withName('John Doe');
  person.displayInfo();
}
```

#### Factory Constructor

A factory constructor can return an instance of the class or null.

```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age);

  // Factory constructor
  factory Person.fromJson(Map<String, dynamic> json) {
    return Person(json['name'], json['age']);
  }
}

void main() {
  Map<String, dynamic> json = {'name': 'John Doe', 'age': 25};
  Person person = Person.fromJson(json);
  person.displayInfo();
}
```

### Null Safety in Dart

Null safety is a feature in Dart that helps prevent null reference errors, which are a common source of runtime errors. 

#### Key Concepts of Null Safety

- **Non-nullable types**: By default, all types are non-nullable. For example, `int x` cannot be null.
- **Nullable types**: If a variable can be null, you need to explicitly mark it as nullable using the `?` symbol. For example, `int? x` can be null.
- **Late keyword**: Used for variables that will be initialized later but are guaranteed to be non-null by the time they are used.

#### Null Safety Example

```dart
void main() {
  int? a; // Nullable integer
  int b = 5; // Non-nullable integer

  if (a != null) {
    print(a + b); // No error as 'a' is checked for null
  }

  int c = a ?? 0; // Using null-aware operator
  print(c + b); // Output: 5
}
```

### Encapsulation in Dart

Encapsulation is the bundling of data with methods that operate on that data. It is used to restrict access to certain components and can prevent accidental interference.

#### Private Members

In Dart, you can make a member private by prefixing its name with an underscore (`_`).

```dart
class Person {
  String _name;
  int _age;

  Person(this._name, this._age);

  // Getter for name
  String get name => _name;

  // Setter for name
  set name(String newName) {
    _name = newName;
  }
}

void main() {
  Person person = Person('John Doe', 25);
  print(person.name); // Accessing the name through the getter
  person.name = 'Jane Doe'; // Modifying the name through the setter
  print(person.name);
}
```

### Inheritance in Dart

Inheritance is a mechanism wherein a new class inherits properties and behavior (methods) from an existing class. 

#### Implementing Inheritance

```dart
class Animal {
  void eat() {
    print('Animal is eating');
  }
}

class Dog extends Animal {
  void bark() {
    print('Dog is barking');
  }
}

void main() {
  Dog dog = Dog();
  dog.eat(); // Method from the parent class
  dog.bark(); // Method from the child class
}
```

### Polymorphism in Dart

Polymorphism allows objects to be treated as instances of their parent class rather than their actual class. 

#### Method Overriding

```dart
class Animal {
  void makeSound() {
    print('Animal sound');
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print('Bark');
  }
}

void main() {
  Animal animal = Dog();
  animal.makeSound(); // Output: Bark
}
```

### Abstraction in Dart

Abstraction is the concept of hiding the complex implementation details and showing only the necessary features of an object. 

#### Abstract Class and Methods

```dart
abstract class Animal {
  void makeSound(); // Abstract method
}

class Dog extends Animal {
  @override
  void makeSound() {
    print('Bark');
  }
}

void main() {
  Dog dog = Dog();
  dog.makeSound(); // Output: Bark
}
```

### Summary

- **Class and Object**: Classes are blueprints; objects are instances of classes.
- **Methods**: Functions defined within a class.
- **Constructors**: Special methods for creating and initializing objects.
- **Null Safety**: Ensures that non-nullable types cannot be assigned null.
- **Encapsulation**: Bundling data and methods that operate on the data.
- **Inheritance**: Mechanism to create a new class from an existing class.
- **Polymorphism**: Ability to treat objects of different classes through a common interface.
- **Abstraction**: Hiding complex details and exposing only necessary parts.

### Homework

1. Create a `Vehicle` class with properties for `brand`, `model`, and `year`. Add a method to display these details.
2. Implement a named constructor for the `Vehicle` class that only takes `brand` and `model`, and sets a default `year`.
3. Demonstrate the use of null safety by creating nullable and non-nullable variables and using null-aware operators.
4. Create a `Car` class that inherits from the `Vehicle` class and adds a method to display the type of vehicle.
