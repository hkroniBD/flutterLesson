### **Lecture Notes: Session 2 - Dart Basics (Part 1)**

---

#### **1. Dart Syntax and Structure**

Dart is an object-oriented programming language developed by Google. It's used to build mobile, web, and server applications, particularly with the Flutter framework. Understanding Dart's syntax and structure is essential for writing clean, efficient code.

**a. Basic Program Structure:**
- **Main Function:** The entry point of every Dart application is the `main()` function.
  ```dart
  void main() {
    print('Hello, Dart!');
  }
  ```
- **Statements:** Dart programs consist of statements ending with a semicolon (`;`).
- **Comments:** 
  - Single-line comment: `// This is a comment`
  - Multi-line comment: `/* This is a comment */`
  - Documentation comment: `/// This is a documentation comment`

**b. Identifiers:**
- Names used for variables, functions, classes, etc.
- Must begin with a letter or an underscore (`_`), followed by letters, digits, or underscores.
- Dart is case-sensitive.

**c. Data Types:**
- Dart is a statically typed language, meaning variables must be declared with a specific type or inferred by the compiler.
  - **Primitive Types:** 
    - `int`: Integer values (e.g., `int a = 10;`)
    - `double`: Floating-point numbers (e.g., `double b = 3.14;`)
    - `String`: Sequence of characters (e.g., `String s = 'Hello';`)
    - `bool`: Boolean values (`true` or `false`)
  - **Other Types:**
    - `List`: Ordered collection (e.g., `List<int> numbers = [1, 2, 3];`)
    - `Map`: Key-value pairs (e.g., `Map<String, int> scores = {'John': 90, 'Jane': 85};`)

---

#### **2. Variables, Data Types, and Operators**

**a. Declaring Variables:**
- **Explicit Declaration:** Define a variable with its type.
  ```dart
  int age = 25;
  String name = 'Alice';
  ```
- **Type Inference:** Use `var` or `final` to let Dart infer the type.
  ```dart
  var height = 5.9; // Inferred as double
  final String city = 'New York'; // city is immutable
  ```

**b. Data Types:**
- **Numbers:** 
  - `int` for integers, `double` for floating-point numbers.
  ```dart
  int count = 10;
  double temperature = 36.6;
  ```
- **Strings:**
  - Represented by `String`, enclosed in single or double quotes.
  ```dart
  String greeting = 'Hello, World!';
  ```
- **Booleans:**
  - Represented by `bool`, with values `true` or `false`.
  ```dart
  bool isLoggedIn = true;
  ```

**c. Operators:**
- **Arithmetic Operators:**
  - `+`, `-`, `*`, `/`, `%`
  ```dart
  int sum = 10 + 5; // 15
  int product = 10 * 2; // 20
  ```
- **Relational Operators:**
  - `==`, `!=`, `<`, `>`, `<=`, `>=`
  ```dart
  bool isEqual = (5 == 5); // true
  ```
- **Logical Operators:**
  - `&&` (and), `||` (or), `!` (not)
  ```dart
  bool result = (true && false); // false
  ```
- **Assignment Operators:**
  - `=`, `+=`, `-=`, `*=`, `/=`
  ```dart
  int x = 5;
  x += 3; // x = 8
  ```
- **Conditional (Ternary) Operator:**
  - Syntax: `condition ? expr1 : expr2`
  ```dart
  String message = (age >= 18) ? 'Adult' : 'Minor';
  ```

---

#### **3. Control Flow: If-Else Statements and Loops**

Control flow statements determine the order in which code executes.

**a. If-Else Statements:**
- Used for conditional execution of code blocks.
  ```dart
  int age = 20;
  if (age >= 18) {
    print('Adult');
  } else {
    print('Minor');
  }
  ```
- **Else-If Ladder:**
  ```dart
  if (marks >= 90) {
    print('Grade A');
  } else if (marks >= 80) {
    print('Grade B');
  } else {
    print('Grade C');
  }
  ```

**b. Loops:**

- **For Loop:**
  ```dart
  for (int i = 0; i < 5; i++) {
    print(i);
  }
  ```
- **While Loop:**
  ```dart
  int count = 0;
  while (count < 5) {
    print(count);
    count++;
  }
  ```
- **Do-While Loop:**
  - Executes the loop body at least once, then checks the condition.
  ```dart
  int n = 0;
  do {
    print(n);
    n++;
  } while (n < 5);
  ```

---

#### **4. Functions and Methods**

Functions are reusable blocks of code that perform specific tasks.

**a. Defining Functions:**
- Functions can be defined using the `returnType functionName(parameters) {}` syntax.
  ```dart
  int add(int a, int b) {
    return a + b;
  }
  ```

**b. Optional Parameters:**
- Dart supports both optional named and positional parameters.
  ```dart
  void greet(String name, [String? greeting = 'Hello']) {
    print('$greeting $name');
  }
  greet('Alice'); // Output: Hello Alice
  ```
- **Named Parameters:**
  ```dart
  void displayInfo({required String name, int age = 0}) {
    print('Name: $name, Age: $age');
  }
  displayInfo(name: 'Bob', age: 25);
  ```

**c. Arrow Functions:**
- Short syntax for functions that contain a single expression.
  ```dart
  int square(int x) => x * x;
  ```

**d. Methods in Classes:**
- Methods are functions defined inside a class.
  ```dart
  class Car {
    String model;
    Car(this.model);

    void showModel() {
      print('Model: $model');
    }
  }
  ```

---

### **Conclusion**
This session provided an in-depth introduction to Dart's syntax and structure, including variables, data types, operators, control flow, and functions/methods. Understanding these basics is crucial for building more complex Flutter applications in future sessions. 

**Next Session Preview:**
In the next session, we'll dive deeper into Dart's object-oriented features, exploring classes, constructors, inheritance, and more advanced control flow structures.
