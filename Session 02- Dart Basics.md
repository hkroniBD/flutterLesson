## Session 2: Dart Basics

### Duration
- **Total Time**: 3 hours

### Objectives
By the end of this session, students should be able to:
1. Understand and use Dart’s basic syntax and constructs.
2. Write and execute simple Dart programs.
3. Utilize Dart for basic programming tasks such as control flow, loops, and functions.

### Materials Needed
- Laptops with Dart SDK installed
- Code editor (Visual Studio Code, Android Studio, or IntelliJ IDEA)
- Projector or screen for demonstrations
- Access to DartPad or similar online Dart compiler

### Detailed Material

### **1. Variables, Data Types, and Operators (60 minutes)**

#### **1.1 Variables**
- **Definition**: Variables store data that can be used and manipulated in a program.
- **Declaration and Initialization**:
  ```dart
  int age = 25;
  String name = 'John Doe';
  double height = 5.9;
  bool isStudent = true;
  ```
- **Type Inference**: Dart can infer types based on the assigned value.
  ```dart
  var city = 'Dhaka'; // Dart infers city as String
  ```

- **Reference**:
  - [Dart Variables and Types](https://dart.dev/guides/language/language-tour#variables)

#### **1.2 Data Types**
- **Primitive Data Types**:
  - **int**: Integer values.
    ```dart
    int score = 100;
    ```
  - **double**: Floating-point numbers.
    ```dart
    double temperature = 36.6;
    ```
  - **String**: Textual data.
    ```dart
    String greeting = 'Hello, World!';
    ```
  - **bool**: Boolean values (true/false).
    ```dart
    bool isFinished = false;
    ```

- **Reference**:
  - [Dart Data Types](https://dart.dev/guides/language/language-tour#numbers)

#### **1.3 Operators**
- **Arithmetic Operators**:
  - Addition `+`, Subtraction `-`, Multiplication `*`, Division `/`, Modulus `%`
  - Examples:
    ```dart
    int a = 10;
    int b = 5;
    print(a + b); // 15
    print(a * b); // 50
    ```

- **Relational Operators**:
  - Equal `==`, Not equal `!=`, Greater than `>`, Less than `<`, Greater than or equal `>=`, Less than or equal `<=`
  - Examples:
    ```dart
    print(a > b); // true
    print(a == b); // false
    ```

- **Logical Operators**:
  - AND `&&`, OR `||`, NOT `!`
  - Examples:
    ```dart
    bool x = true;
    bool y = false;
    print(x && y); // false
    print(x || y); // true
    ```

- **Reference**:
  - [Dart Operators](https://dart.dev/guides/language/language-tour#operators)

### **2. Control Flow Statements (60 minutes)**

#### **2.1 If-Else Statements**
- **Purpose**: Make decisions in code based on conditions.
- **Syntax**:
  ```dart
  if (age >= 18) {
    print('Adult');
  } else {
    print('Minor');
  }
  ```

- **Reference**:
  - [Dart Control Flow Statements](https://dart.dev/guides/language/language-tour#control-flow-statements)

#### **2.2 Switch-Case Statements**
- **Purpose**: Handle multiple conditions based on a single variable.
- **Syntax**:
  ```dart
  switch (day) {
    case 'Monday':
      print('Start of the week');
      break;
    case 'Friday':
      print('End of the work week');
      break;
    default:
      print('Weekend');
  }
  ```

- **Reference**:
  - [Dart Switch-Case](https://dart.dev/guides/language/language-tour#switch)

### **3. Loops (60 minutes)**

#### **3.1 For Loop**
- **Purpose**: Repeat a block of code a fixed number of times.
- **Syntax**:
  ```dart
  for (int i = 0; i < 5; i++) {
    print(i); // Prints 0 to 4
  }
  ```

- **Reference**:
  - [Dart For Loop](https://dart.dev/guides/language/language-tour#for)

#### **3.2 While Loop**
- **Purpose**: Repeat a block of code as long as a condition is true.
- **Syntax**:
  ```dart
  int i = 0;
  while (i < 5) {
    print(i); // Prints 0 to 4
    i++;
  }
  ```

- **Reference**:
  - [Dart While Loop](https://dart.dev/guides/language/language-tour#while)

#### **3.3 Do-While Loop**
- **Purpose**: Execute a block of code at least once and then repeat as long as a condition is true.
- **Syntax**:
  ```dart
  int i = 0;
  do {
    print(i); // Prints 0 to 4
    i++;
  } while (i < 5);
  ```

- **Reference**:
  - [Dart Do-While Loop](https://dart.dev/guides/language/language-tour#do-while)

### **4. Functions and Methods (30 minutes)**

#### **4.1 Functions**
- **Purpose**: Encapsulate code into reusable blocks.
- **Syntax**:
  ```dart
  int add(int a, int b) {
    return a + b;
  }
  ```

- **Reference**:
  - [Dart Functions](https://dart.dev/guides/language/language-tour#functions)

#### **4.2 Methods in Classes**
- **Purpose**: Functions that belong to a class and operate on class data.
- **Syntax**:
  ```dart
  class Calculator {
    int add(int a, int b) {
      return a + b;
    }
  }

  void main() {
    var calc = Calculator();
    print(calc.add(5, 3)); // 8
  }
  ```

- **Reference**:
  - [Dart Classes and Objects](https://dart.dev/guides/language/language-tour#classes)

### **5. Hands-On Exercises and Practice (30 minutes)**

#### **5.1 DartPad Exercises**
- **Objective**: Apply concepts learned in DartPad to solve simple problems.
- **Exercises**:
  - Write a Dart program that calculates the factorial of a number.
  - Implement a Dart program using `if-else` and `switch-case` statements to categorize user input.
  - Create a Dart function that finds the largest number in a list.

- **Reference**:
  - [DartPad](https://dartpad.dev/)

### **6. Q&A and Wrap-Up (30 minutes)**

#### **6.1 Addressing Questions**
- Open floor for students to ask questions related to Dart basics.

#### **6.2 Recap of the Day**
- Summary of key points covered in the session.

#### **6.3 Homework Assignment**
- **Create a Dart Program**: Develop a Dart program that demonstrates usage of variables, control flow, loops, and functions. For example, a simple calculator or a number guessing game.

- **Reference**:
  - [Dart Language Tour](https://dart.dev/guides/language/language-tour)
