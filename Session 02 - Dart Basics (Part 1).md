### **Session 2: Dart Basics - Part 1**

#### **Objective:**
<details><summary>Expand Section</summary>
In this session, students will learn the fundamentals of the Dart programming language, including its syntax and structure, variables, data types, operators, control flow, and basic functions and methods. This foundational knowledge is essential for developing applications in Flutter.
</details>

---

### **1. Dart Syntax and Structure**
<details><summary>Expand Section</summary>
   
**a. Introduction to Dart:**

   - **Dart Language Overview:**
     - Dart is a client-optimized language for fast apps on any platform. It is used for building Flutter apps and supports both Ahead-of-Time (AOT) and Just-in-Time (JIT) compilation.

   - **Basic Syntax:**
     - Dart uses a C-style syntax, similar to Java, JavaScript, and C#.

   - **Code Structure:**
     - **File Extension:** `.dart`
     - **Main Function:** Entry point of a Dart application.
     - **Comments:**
       - Single-line: `// Comment`
       - Multi-line: `/* Comment */`

   - **References:**
     - [Dart Language Tour](https://dart.dev/guides/language/language-tour)
     - [Dart Syntax Overview](https://dart.dev/guides/language/syntax)

**b. Example Code:**

   ```dart
   // This is a simple Dart program

   void main() {
     print('Hello, Dart!');
   }
   ```
Try at 🌐 https://dartpad.dev/
</details>

---

### **2. Variables, Data Types, and Operators**
<details><summary>Expand Section</summary>
   
**a. Variables:**

   - **Declaration and Initialization:**
     - Dart supports type inference, so you can either specify the type or let Dart infer it.
     - **Syntax:**
       ```dart
       int age = 25; // Explicit type
       var name = 'John'; // Type inferred as String
       ```

   - **Constants:**
     - Use `final` for runtime constants and `const` for compile-time constants.
     - **Syntax:**
       ```dart
       final String userName = 'Alice';
       const double pi = 3.14;
       ```

   - **References:**
     - [Dart Variables and Data Types](https://dart.dev/guides/language/language-tour#variables)

**b. Data Types:**

   - **Primitive Types:**
     - **int:** Integer values, e.g., `42`
     - **double:** Floating-point values, e.g., `3.14`
     - **String:** Text, e.g., `'Hello'`
     - **bool:** Boolean values, `true` or `false`
     - **dynamic:** A variable that can hold any type, e.g., `var anything = 42; anything = 'Now I am a string';`

   - **References:**
     - [Dart Data Types](https://dart.dev/guides/language/language-tour#numbers)

**c. Operators:**

   - **Arithmetic Operators:**
     - `+`, `-`, `*`, `/`, `%`
     - Example: `int sum = 5 + 3;`

   - **Relational Operators:**
     - `==`, `!=`, `>`, `<`, `>=`, `<=`
     - Example: `bool isEqual = (5 == 5);`

   - **Logical Operators:**
     - `&&` (and), `||` (or), `!` (not)
     - Example: `bool result = (5 > 3) && (2 < 4);`

   - **Assignment Operators:**
     - `=`, `+=`, `-=`, `*=`, `/=`
     - Example: `int x = 5; x += 2;`

   - **References:**
     - [Dart Operators](https://dart.dev/guides/language/language-tour#operators)
</details>

---

### **3. Control Flow: if-else, Loops (for, while)**
<details><summary>Expand Section</summary>
   
**a. if-else Statements:**

   - **Syntax:**
     ```dart
     if (condition) {
       // Code to execute if condition is true
     } else if (anotherCondition) {
       // Code to execute if anotherCondition is true
     } else {
       // Code to execute if no conditions are true
     }
     ```

   - **Example:**
     ```dart
     void main() {
       int number = 10;
       if (number > 0) {
         print('Number is positive');
       } else {
         print('Number is non-positive');
       }
     }
     ```

**b. for Loop:**

   - **Syntax:**
     ```dart
     for (initialization; condition; increment) {
       // Code to execute repeatedly
     }
     ```

   - **Example:**
     ```dart
     void main() {
       for (int i = 0; i < 5; i++) {
         print(i);
       }
     }
     ```

**c. while Loop:**

   - **Syntax:**
     ```dart
     while (condition) {
       // Code to execute repeatedly
     }
     ```

   - **Example:**
     ```dart
     void main() {
       int count = 0;
       while (count < 5) {
         print(count);
         count++;
       }
     }
     ```

**d. References:**
   - [Dart Control Flow Statements](https://dart.dev/guides/language/language-tour#control-flow-statements)

---

### **4. Functions and Methods**

**a. Functions:**

   - **Definition and Syntax:**
     ```dart
     returnType functionName(parameters) {
       // Code to execute
       return value; // Optional, depending on returnType
     }
     ```

   - **Example:**
     ```dart
     int add(int a, int b) {
       return a + b;
     }

     void main() {
       int result = add(3, 5);
       print(result); // Output: 8
     }
     ```

**b. Methods:**

   - **Definition and Syntax:**
     - Methods are functions defined within a class.
     - **Example:**
       ```dart
       class Calculator {
         int add(int a, int b) {
           return a + b;
         }
       }

       void main() {
         Calculator calc = Calculator();
         int result = calc.add(5, 7);
         print(result); // Output: 12
       }
       ```

**c. Arrow Functions:**

   - **Syntax:**
     ```dart
     returnType functionName(parameters) => expression;
     ```

   - **Example:**
     ```dart
     int multiply(int a, int b) => a * b;

     void main() {
       int result = multiply(4, 5);
       print(result); // Output: 20
     }
     ```

   - **References:**
     - [Dart Functions](https://dart.dev/guides/language/language-tour#functions)
     - [Dart Methods](https://dart.dev/guides/language/language-tour#methods)
</details>

---

### **Assignments**
<details><summary>Expand Section</summary>

#### **Assignment 1: Basic Dart Syntax**
- **Objective:** Practice Dart syntax, variables, data types, and operators.
- **Tasks:**
  1. Write a Dart program that declares variables of different types and prints their values.
  2. Use arithmetic and relational operators to perform and display calculations.

#### **Assignment 2: Control Flow and Loops**
- **Objective:** Implement control flow statements and loops.
- **Tasks:**
  1. Write a Dart program that uses `if-else` statements to classify a number as positive, negative, or zero.
  2. Implement a `for` loop and a `while` loop to print numbers from 1 to 10.

#### **Assignment 3: Functions and Methods**
- **Objective:** Define and use functions and methods in Dart.
- **Tasks:**
  1. Create a function that takes two integers and returns their sum.
  2. Define a class with methods for basic arithmetic operations and demonstrate their usage.
</details>

---

### **Quiz: Dart Basics - Part 1**
<details><summary>Expand Section</summary>

### **1. Which symbol is used to start a single-line comment in Dart?**

- a) `/*`
- b) `//`
- c) `#`
- d) `--`

<details>
<summary> See solution </summary>
   
**Correct Answer:** b) `//`

**Explanation:** 
In Dart, a single-line comment starts with `//`. This is similar to many other C-style languages like Java, JavaScript, and C#. Multi-line comments start with `/*` and end with `*/`, but `//` is used specifically for single-line comments.
</details>

---

### **2. What will be the output of the following Dart code?**

```dart
int x = 10;
x *= 2;
print(x);
```

- a) `10`
- b) `20`
- c) `40`
- d) `60`

<details>
<summary>See solution</summary>
   
**Correct Answer:** b) `20`

**Explanation:** 
The `*=` operator in Dart multiplies the variable `x` by the value on the right (2) and assigns the result back to `x`. Initially, `x` is 10, so `x *= 2` is equivalent to `x = x * 2`, which results in `x` being 20. The `print(x)` statement then outputs `20`.
</details>

---

### **3. How do you declare a variable with a constant value in Dart?**

- a) `var`
- b) `const`
- c) `final`
- d) `static`

<details>
<summary>See solution</summary>
   
**Correct Answer:** b) `const`

**Explanation:** 
In Dart, `const` is used to declare a compile-time constant, meaning its value is fixed at compile time and cannot be changed later. The `final` keyword can also be used for declaring constants, but its value is determined at runtime, making `const` the correct choice for compile-time constants.
</details>

---

### **4. What does the `for` loop syntax look like in Dart?**

- a) `for (init; condition; increment) { }`
- b) `loop (init; condition; increment) { }`
- c) `for (init; condition; step) { }`
- d) `foreach (init; condition; increment) { }`

<details>
<summary>See solution</summary>
   
**Correct Answer:** a) `for (init; condition; increment) { }`

**Explanation:** 
The correct syntax for a `for` loop in Dart is `for (initialization; condition; increment) { }`. This format is standard in many programming languages and allows for a loop to execute repeatedly as long as the condition evaluates to true.
</details>

---

### **5. How do you define a method inside a Dart class?**

- a) `methodName(parameters) { }`
- b) `def methodName(parameters) { }`
- c) `function methodName(parameters) { }`
- d) `method methodName(parameters) { }`

<details>
<summary>**See solution**</summary>
**Correct Answer:** a) `methodName(parameters) { }`

**Explanation:** 
In Dart, methods are defined inside a class with the syntax `methodName(parameters) { }`. There is no special keyword like `def` or `function`; the method name is followed directly by parentheses (which may include parameters) and the body of the method enclosed in curly braces `{}`.
</details>

---

### **Conclusion**

Session 2 covers fundamental Dart programming concepts necessary for Flutter development

. Understanding Dart's syntax, data types, control flow, and functions will provide a strong foundation for writing effective and efficient Flutter code.
