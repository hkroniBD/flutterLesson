### **Lecture Notes: Session 3 - Dart Basics (Part 2)**

---

#### **1. Introduction to Object-Oriented Programming (OOP) Concepts in Dart**

Object-Oriented Programming (OOP) is a programming paradigm centered around the concept of "objects", which are instances of classes. OOP in Dart focuses on encapsulation, inheritance, and polymorphism, providing a structured approach to software development.

**a. Core Concepts of OOP:**
- **Encapsulation:** Bundling the data (attributes) and methods (functions) that operate on the data into a single unit, or class.
- **Abstraction:** Hiding the complex implementation details and showing only the necessary features.
- **Inheritance:** Mechanism by which one class can inherit properties and methods from another, promoting code reuse.
- **Polymorphism:** Ability to present the same interface for different data types or classes, allowing for flexibility in code execution.

**b. Why OOP?**
- **Modularity:** Code is organized into distinct classes, making it easier to manage and debug.
- **Reusability:** Classes can be reused across different parts of an application or even in other projects.
- **Scalability:** OOP principles make it easier to scale applications by adding new features without disrupting existing functionality.

---

#### **2. Classes, Objects, and Constructors**

In Dart, classes are the blueprint for objects, defining the properties and behaviors that the objects created from the class will have.

**a. Classes and Objects:**
- **Class:** Defines a data type by bundling data and methods that operate on the data.
  ```dart
  class Car {
    String model;
    int year;

    void start() {
      print('Car is starting');
    }
  }
  ```
- **Object:** An instance of a class. Objects are created using the `new` keyword (optional in Dart).
  ```dart
  Car myCar = Car();
  myCar.model = 'Tesla Model S';
  myCar.year = 2020;
  myCar.start(); // Outputs: Car is starting
  ```

**b. Constructors:**
- Constructors are special functions that are automatically called when an object is instantiated. They are used to initialize the object’s properties.

- **Default Constructor:** Dart provides a default constructor if you don't define one.
  ```dart
  class Car {
    String model;
    int year;

    Car() {
      print('A new car has been created!');
    }
  }
  ```

- **Parameterized Constructor:** Allows passing arguments to set properties when an object is created.
  ```dart
  class Car {
    String model;
    int year;

    Car(this.model, this.year);
  }

  Car myCar = Car('Tesla Model 3', 2021);
  ```

- **Named Constructors:** Dart allows you to define multiple constructors for a class by giving them different names.
  ```dart
  class Car {
    String model;
    int year;

    Car(this.model, this.year);

    Car.electricCar(String model) {
      this.model = model;
      this.year = 2021;
    }
  }

  Car tesla = Car.electricCar('Tesla Model S');
  ```

**c. Getters and Setters:**
- **Getters and Setters** are special methods that provide read and write access to an object’s properties. They allow for encapsulation and data validation.

  ```dart
  class Circle {
    double _radius;

    Circle(this._radius);

    double get radius => _radius;

    set radius(double value) {
      if (value > 0) {
        _radius = value;
      }
    }
  }

  Circle circle = Circle(5.0);
  print(circle.radius); // Accessing the radius
  circle.radius = 7.0; // Setting the radius
  ```

---

#### **3. Inheritance and Polymorphism**

Inheritance and polymorphism are two fundamental principles of OOP that allow for extending existing code and creating more dynamic, flexible applications.

**a. Inheritance:**
- Inheritance allows one class (child class) to inherit properties and methods from another class (parent class), promoting code reuse.

- **Syntax:**
  ```dart
  class Vehicle {
    String color;

    void drive() {
      print('Driving the vehicle');
    }
  }

  class Car extends Vehicle {
    int doors;

    void honk() {
      print('Honking the car');
    }
  }

  Car myCar = Car();
  myCar.color = 'Red';
  myCar.drive(); // Inherited method
  myCar.honk(); // Own method
  ```

**b. Polymorphism:**
- Polymorphism means "many forms". In Dart, polymorphism allows one interface to be used for a general class of actions, which can be performed differently by different classes.

- **Method Overriding:** A subclass can provide a specific implementation of a method that is already defined in its superclass.
  ```dart
  class Animal {
    void sound() {
      print('Animal makes a sound');
    }
  }

  class Dog extends Animal {
    @override
    void sound() {
      print('Dog barks');
    }
  }

  Animal myDog = Dog();
  myDog.sound(); // Outputs: Dog barks
  ```

**c. Abstract Classes and Interfaces:**
- **Abstract Classes:** Cannot be instantiated and are meant to be subclassed. They can contain abstract methods, which do not have an implementation and must be overridden by subclasses.
  ```dart
  abstract class Shape {
    void draw(); // Abstract method
  }

  class Circle extends Shape {
    @override
    void draw() {
      print('Drawing a circle');
    }
  }

  Shape shape = Circle();
  shape.draw(); // Outputs: Drawing a circle
  ```

- **Interfaces:** In Dart, every class implicitly defines an interface, which other classes can implement. Unlike abstract classes, a class can implement multiple interfaces.
  ```dart
  class Printer {
    void printDocument() {
      print('Printing document');
    }
  }

  class Scanner {
    void scanDocument() {
      print('Scanning document');
    }
  }

  class AllInOnePrinter implements Printer, Scanner {
    @override
    void printDocument() {
      print('All-in-one printer printing');
    }

    @override
    void scanDocument() {
      print('All-in-one printer scanning');
    }
  }

  AllInOnePrinter device = AllInOnePrinter();
  device.printDocument();
  device.scanDocument();
  ```

---

#### **4. Exception Handling in Dart**

Exception handling in Dart provides a way to handle runtime errors, ensuring that your program can deal with unexpected situations gracefully.

**a. What is an Exception?**
- An exception is an error that occurs during the execution of a program. In Dart, exceptions are objects that represent an error or an unexpected event.

**b. Try-Catch-Finally:**
- Dart uses `try`, `catch`, and `finally` blocks to handle exceptions.
  ```dart
  void main() {
    try {
      int result = 10 ~/ 0; // Throws an exception
    } catch (e) {
      print('Caught an exception: $e');
    } finally {
      print('This block always executes');
    }
  }
  ```

- **Catching Specific Exceptions:**
  - Dart allows catching specific exceptions to handle different types of errors accordingly.
  ```dart
  void main() {
    try {
      int result = 10 ~/ 0;
    } on IntegerDivisionByZeroException {
      print('Cannot divide by zero');
    } catch (e) {
      print('Caught an exception: $e');
    }
  }
  ```

- **Rethrowing Exceptions:**
  - You can rethrow an exception after catching it, to allow it to be handled at a higher level.
  ```dart
  void main() {
    try {
      checkValue(-1);
    } catch (e) {
      print('Caught an exception: $e');
    }
  }

  void checkValue(int value) {
    if (value < 0) {
      throw Exception('Value must be non-negative');
    }
  }
  ```

---

#### **5. Asynchronous Programming with Future and async/await**

Asynchronous programming is essential for performing tasks that take time, such as network requests, file I/O, and timers, without blocking the main thread.

**a. Futures:**
- A `Future` in Dart represents a potential value or error that will be available at some time in the future.

- **Creating a Future:**
  ```dart
  Future<String> fetchData() {
    return Future.delayed(Duration(seconds: 2), () => 'Data loaded');
  }

  void main() {
    fetchData().then((data) {
      print(data); // Outputs: Data loaded
    });
  }
  ```

- **Handling Errors in Futures:**
  ```dart
  fetchData().then((data) {
    print(data);
  }).catchError((error) {
    print('Error: $error');
  });
  ```

**b. async and await:**
- The `async` keyword is used to define an asynchronous function, and `await` is used to wait for a Future to complete.

- **Using async/await:**
  ```dart
  Future<String> fetchData() async {
    await Future.delayed(Duration(seconds: 2)); 
    return 'Data loaded';
  }

  void main() async {
    String data = await fetchData();
    print(data); // Outputs: Data loaded
  }
  ```

- **Error Handling with async/await:**
  ```dart
  void main() async

 {
    try {
      String data = await fetchData();
      print(data);
    } catch (e) {
      print('Caught an exception: $e');
    }
  }
  ```

- **Asynchronous Iteration:**
  - Dart supports asynchronous iteration using `await for`. This is useful when working with streams or handling a sequence of asynchronous events.
  ```dart
  Stream<int> countStream(int to) async* {
    for (int i = 1; i <= to; i++) {
      await Future.delayed(Duration(seconds: 1));
      yield i;
    }
  }

  void main() async {
    await for (int i in countStream(5)) {
      print(i); // Outputs: 1, 2, 3, 4, 5
    }
  }
  ```

---

### **Conclusion**

This session provides an in-depth look into the fundamentals of object-oriented programming in Dart, covering essential concepts such as classes, objects, constructors, inheritance, polymorphism, exception handling, and asynchronous programming. Mastery of these topics is crucial for building robust and scalable Flutter applications.
