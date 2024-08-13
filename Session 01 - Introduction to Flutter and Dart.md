### **Session 1: Introduction to Flutter and Dart**

#### **Objective:**
This session will introduce students to Flutter and Dart, covering the advantages of using Flutter, providing an overview of Dart, and guiding students through setting up their development environment. By the end of the session, students will have created their first Flutter app, a simple "Hello World" application.

---

### **1. Overview of Flutter**

**a. What is Flutter?**

   - **Definition:**
     - Flutter is an open-source UI framework developed by Google for building natively compiled applications for mobile, web, and desktop from a single codebase.

   - **Key Features:**
     - **Hot Reload:** Instantly see changes in your app without restarting the whole application.
     - **Widgets:** Rich set of pre-designed and customizable widgets to create responsive UIs.
     - **Performance:** High performance due to direct compilation to native code.
     - **Cross-Platform:** Write once, run anywhere; supports Android, iOS, web, and desktop platforms.

   - **References:**
     - [Flutter Official Website](https://flutter.dev)
     - [Flutter Overview](https://flutter.dev/docs/get-started/flutter-for/)

**b. Advantages of Using Flutter:**

   - **Fast Development:**
     - Rapid development with hot reload and a rich set of pre-designed widgets.

   - **Expressive and Flexible UI:**
     - Create beautiful UIs with highly customizable widgets and advanced UI features.

   - **Single Codebase:**
     - Maintain one codebase for multiple platforms (mobile, web, and desktop).

   - **Performance:**
     - Direct compilation to native code provides high performance and smooth animations.

   - **Strong Community and Ecosystem:**
     - Large and active community with extensive libraries and packages.

---

### **2. Introduction to Dart Programming Language**

**a. What is Dart?**

   - **Definition:**
     - Dart is a programming language developed by Google, designed for building web, server, and mobile applications. It is the language used to develop Flutter applications.

   - **Key Features:**
     - **Strongly Typed Language:** Ensures type safety and improves code quality.
     - **Asynchronous Programming:** Built-in support for async/await and Future classes.
     - **Optimized for UI Development:** Designed to be fast and efficient for building UIs.

   - **References:**
     - [Dart Official Website](https://dart.dev)
     - [Dart Language Tour](https://dart.dev/guides/language/language-tour)

**b. Basic Syntax and Structure:**

   - **Variables and Data Types:**
     - Example: `int number = 10;`, `String greeting = 'Hello';`

   - **Control Flow:**
     - `if-else`, `for`, `while` loops.

   - **Functions:**
     - Example: `void greet() { print('Hello'); }`

   - **Classes and Objects:**
     - Example: 
       ```dart
       class Person {
         String name;
         int age;
         
         Person(this.name, this.age);
         
         void introduce() {
           print('My name is $name and I am $age years old.');
         }
       }
       ```

---

### **3. Setting Up the Development Environment**

**a. Installing Flutter SDK:**

   - **Download Flutter SDK:**
     - Visit the [Flutter Installation Page](https://flutter.dev/docs/get-started/install) and download the appropriate version for your operating system.

   - **Extract and Configure:**
     - Extract the downloaded archive and add the `flutter/bin` directory to your system’s PATH.

   - **Verify Installation:**
     - Run `flutter doctor` in your terminal to check for any missing dependencies and ensure that your setup is correct.

**b. Installing an IDE:**

   - **Recommended IDEs:**
     - **Visual Studio Code (VS Code):**
       - Install the [Flutter Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter) and the [Dart Extension](https://marketplace.visualstudio.com/items?itemName=Dart-Code.dart-code).

     - **Android Studio:**
       - Install the [Flutter Plugin](https://plugins.jetbrains.com/plugin/9212-flutter) and the [Dart Plugin](https://plugins.jetbrains.com/plugin/6351-dart) from the JetBrains Plugin Repository.

**c. Setting Up an Emulator:**

   - **Android Emulator:**
     - Install Android Studio, set up an Android Virtual Device (AVD) through the [AVD Manager](https://developer.android.com/studio/run/managing-avds).

   - **iOS Simulator:**
     - Install [Xcode](https://developer.apple.com/xcode/) and use the Simulator app for testing on iOS devices.

   - **Web and Desktop:**
     - For web, you can use your browser; for desktop, ensure your platform supports Flutter desktop applications.

---

### **4. Creating Your First Flutter App: Hello World**

**a. Creating a New Flutter Project:**

   - **Using Command Line:**
     - Open a terminal and run:
       ```sh
       flutter create hello_world
       ```
     - Navigate to the project directory:
       ```sh
       cd hello_world
       ```

   - **Using IDE:**
     - In VS Code or Android Studio, use the “Create New Project” option and follow the prompts.

**b. Understanding the Project Structure:**

   - **lib/main.dart:**
     - Entry point of the Flutter application. It contains the `main()` function and the root widget of the app.

**c. Writing the "Hello World" App:**

   - **Example Code:**
     ```dart
     import 'package:flutter/material.dart';

     void main() {
       runApp(MyApp());
     }

     class MyApp extends StatelessWidget {
       @override
       Widget build(BuildContext context) {
         return MaterialApp(
           home: Scaffold(
             appBar: AppBar(title: Text('Hello World')),
             body: Center(child: Text('Hello, World!', style: TextStyle(fontSize: 24))),
           ),
         );
       }
     }
     ```

   - **Running the App:**
     - Run the app using the terminal:
       ```sh
       flutter run
       ```
     - Alternatively, use the “Run” button in your IDE.

**d. Exploring the Flutter Hot Reload Feature:**

   - **Making Changes:**
     - Modify the text or UI elements and save the changes.

   - **Hot Reload:**
     - Observe the changes instantly without restarting the app.

---

### **Assignments**

#### **Assignment 1: Setup and Configuration**
- **Objective:** Set up the Flutter development environment and create your first Flutter app.
- **Tasks:**
  1. Install Flutter SDK and set up an IDE.
  2. Create a new Flutter project and run it on an emulator or physical device.
  3. Submit a screenshot of the running app and a brief description of the setup process.

#### **Assignment 2: Modify the "Hello World" App**
- **Objective:** Customize the "Hello World" app with additional features and styles.
- **Tasks:**
  1. Modify the app to include a button that changes the text when pressed.
  2. Submit the updated `main.dart` file and a screenshot of the modified app.

---

### **Quiz**

1. **What is Flutter?**
   - a) A programming language
   - b) A UI framework for building cross-platform applications
   - c) A database management system
   - d) An IDE for coding

2. **Which command is used to create a new Flutter project?**
   - a) `flutter new project`
   - b) `flutter start`
   - c) `flutter create`
   - d) `flutter init`

3. **What does the `flutter doctor` command do?**
   - a) It installs Flutter SDK
   - b) It checks for missing dependencies and verifies your setup
   - c) It runs the Flutter app
   - d) It updates the Flutter SDK

4. **Which widget is used to create a basic app layout in Flutter?**
   - a) Container
   - b) Text
   - c) Scaffold
   - d) Column

5. **What is the purpose of the `hot reload` feature in Flutter?**
   - a) To automatically update the Flutter SDK
   - b) To instantly see changes made to the code without restarting the app
   - c) To deploy the app to the app store
   - d) To generate new Flutter widgets

---

### **Conclusion**

Session 1 provides a comprehensive introduction to Flutter and Dart, setting up the development environment, and creating a simple "Hello World" application. It establishes the foundation for further learning in Flutter development and prepares students to dive deeper into app development concepts in subsequent sessions.
