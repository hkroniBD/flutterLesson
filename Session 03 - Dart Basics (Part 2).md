### **Session 3: Dart Basics - Part 2**

#### **Objective:**
This session delves into advanced Dart programming concepts, focusing on object-oriented programming (OOP), including classes, objects, inheritance, polymorphism, exception handling, and asynchronous programming. Understanding these concepts is crucial for creating scalable and maintainable applications in Flutter.

---

### **1. Introduction to Object-Oriented Programming (OOP) Concepts in Dart**

**a. Object-Oriented Programming Basics:**

   - **Definition:** OOP is a programming paradigm based on the concept of "objects," which can contain data (attributes) and code (methods).
   - **Core Principles:**
     - **Encapsulation:** Bundling data with methods that operate on the data.
     - **Abstraction:** Hiding complex implementation details and exposing only essential features.
     - **Inheritance:** Creating a new class based on an existing class.
     - **Polymorphism:** Using a single interface to represent different underlying forms (data types).

   - **References:**
     - [Dart Object-Oriented Programming](https://dart.dev/guides/language/language-tour#object-oriented-programming)

---

### **2. Classes, Objects, Constructors**

**a. Classes and Objects:**

   - **Definition of Class:**
     - A class is a blueprint for creating objects. It defines the data and behavior of the objects.
     - **Syntax:**
       ```dart
       class Person {
         String name;
         int age;

         void greet() {
           print('Hello, my name is $name and I am $age years old.');
         }
       }
       ```

   - **Creating Objects:**
     - Objects are instances of a class.
     - **Syntax:**
       ```dart
       void main() {
         Person person1 = Person();
         person1.name = 'Alice';
         person1.age = 30;
         person1.greet();
       }
       ```

   - **Constructors:**
     - Constructors are special methods used to initialize objects.
     - **Syntax:**
       ```dart
       class Person {
         String name;
         int age;

         // Default constructor
         Person(this.name, this.age);

         void greet() {
           print('Hello, my name is $name and I am $age years old.');
         }
       }
       ```

   - **References:**
     - [Dart Classes](https://dart.dev/guides/language/language-tour#classes)
     - [Dart Constructors](https://dart.dev/guides/language/language-tour#constructors)

---

### **3. Inheritance and Polymorphism**

**a. Inheritance:**

   - **Definition:**
     - Inheritance allows one class to inherit the properties and methods of another class.
   - **Syntax:**
     ```dart
     class Animal {
       void eat() {
         print('This animal is eating.');
       }
     }

     class Dog extends Animal {
       void bark() {
         print('The dog is barking.');
       }
     }

     void main() {
       Dog myDog = Dog();
       myDog.eat();
       myDog.bark();
     }
     ```

   - **References:**
     - [Dart Inheritance](https://dart.dev/guides/language/language-tour#inheritance)

**b. Polymorphism:**

   - **Definition:**
     - Polymorphism allows methods to do different things based on the object it is acting upon.
   - **Example:**
     ```dart
     class Shape {
       void draw() {
         print('Drawing a shape');
       }
     }

     class Circle extends Shape {
       @override
       void draw() {
         print('Drawing a circle');
       }
     }

     class Square extends Shape {
       @override
       void draw() {
         print('Drawing a square');
       }
     }

     void main() {
       Shape myShape = Circle();
       myShape.draw(); // Output: Drawing a circle

       myShape = Square();
       myShape.draw(); // Output: Drawing a square
     }
     ```

   - **References:**
     - [Dart Polymorphism](https://dart.dev/guides/language/language-tour#polymorphism)

---

### **4. Exception Handling and Asynchronous Programming with Future and async/await**

**a. Exception Handling:**

   - **Definition:**
     - Exception handling is used to handle runtime errors and prevent the application from crashing.
   - **Syntax:**
     ```dart
     void main() {
       try {
         int result = 12 ~/ 0; // This will cause an exception
       } catch (e) {
         print('An error occurred: $e');
       } finally {
         print('This block is executed regardless of an exception.');
       }
     }
     ```

   - **References:**
     - [Dart Exception Handling](https://dart.dev/guides/language/language-tour#exception-handling)

**b. Asynchronous Programming with Future and async/await:**

   - **Future:**
     - A `Future` represents a value that will be available in the future.
   - **Syntax:**
     ```dart
     Future<void> fetchData() async {
       await Future.delayed(Duration(seconds: 2));
       print('Data fetched');
     }

     void main() {
       fetchData();
       print('Waiting for data...');
     }
     ```

   - **async/await:**
     - `async` and `await` keywords are used to write asynchronous code more readable.
   - **Syntax:**
     ```dart
     Future<String> fetchData() async {
       await Future.delayed(Duration(seconds: 2));
       return 'Data fetched';
     }

     void main() async {
       String data = await fetchData();
       print(data);
     }
     ```

   - **References:**
     - [Dart Future](https://dart.dev/guides/libraries/futures)
     - [Dart Async/Await](https://dart.dev/guides/libraries/async)

---

### **Assignments**

#### **Assignment 1: OOP Concepts**
- **Objective:** Practice creating classes, objects, and using constructors.
- **Tasks:**
  1. Define a `Book` class with attributes like `title`, `author`, and `yearPublished`. Include a constructor and a method to display the book details.
  2. Create an instance of the `Book` class and call its method to display the details.

#### **Assignment 2: Inheritance and Polymorphism**
- **Objective:** Implement inheritance and polymorphism.
- **Tasks:**
  1. Create a base class `Vehicle` with a method `start()`. Extend this class to `Car` and `Motorcycle` with overridden methods.
  2. Demonstrate polymorphism by creating a list of `Vehicle` objects and calling the `start()` method on each.

#### **Assignment 3: Exception Handling and Async Programming**
- **Objective:** Implement exception handling and asynchronous programming.
- **Tasks:**
  1. Write a Dart function that simulates data fetching and uses a `Future` to handle asynchronous operations.
  2. Implement exception handling in a function that divides two numbers and handles division by zero.

---

### **Quiz**

1. **What is the purpose of constructors in Dart?**
   - a) To initialize objects
   - b) To define methods
   - c) To handle exceptions
   - d) To create new classes

2. **Which keyword is used to handle exceptions in Dart?**
   - a) `throw`
   - b) `try`
   - c) `catch`
   - d) `finally`

3. **What does polymorphism allow you to do in Dart?**
   - a) Create new classes
   - b) Handle multiple exceptions
   - c) Use a single method name for different implementations
   - d) Manage asynchronous tasks

4. **How do you mark a function as asynchronous in Dart?**
   - a) Using the `future` keyword
   - b) Using the `async` keyword
   - c) Using the `await` keyword
   - d) Using the `await` keyword

5. **What is the output of the following Dart code?**
   ```dart
   void main() {
     print('Start');
     Future.delayed(Duration(seconds: 1), () {
       print('Delayed');
     });
     print('End');
   }
   ```
   - a) `Start`, `Delayed`, `End`
   - b) `Start`, `End`, `Delayed`
   - c) `Delayed`, `Start`, `End`
   - d) `Start`, `Delayed`

---

### **Conclusion**

Session 3 expands on Dart programming fundamentals by introducing OOP concepts, including classes, objects, inheritance, and polymorphism. It also covers exception handling and asynchronous programming, which are essential for managing complex applications and ensuring responsive user experiences.
