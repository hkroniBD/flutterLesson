### **Session 16: Handling Asynchronous Data**

#### **Objective:**
This session will focus on handling asynchronous data in Flutter applications. Students will learn about asynchronous programming concepts, and how to use `FutureBuilder` and `StreamBuilder` to manage and display data in real-time. 

---

### **1. Understanding Asynchronous Programming in Flutter**

**a. What is Asynchronous Programming?**
   - Asynchronous programming allows tasks to run in the background without blocking the main thread. This is crucial for tasks that take time to complete, such as network requests or file I/O.

**b. Key Concepts:**
   - **Future:** Represents a value that may be available now or in the future.
   - **Async/Await:** Syntax for writing asynchronous code that looks synchronous.
   - **Stream:** Represents a sequence of asynchronous events.

**c. Importance in Flutter:**
   - Flutter apps are often I/O-bound, requiring asynchronous operations for network calls, database access, and more. Understanding how to handle asynchronous data is essential for building responsive apps.

**d. Basic Example of Asynchronous Code:**
   - **Using Future and Async/Await:**
     ```dart
     Future<String> fetchData() async {
       await Future.delayed(Duration(seconds: 2)); // Simulate network delay
       return 'Fetched Data';
     }

     void main() async {
       print('Fetching data...');
       String data = await fetchData();
       print('Data: $data');
     }
     ```

---

### **2. Using `FutureBuilder`**

**a. What is `FutureBuilder`?**
   - `FutureBuilder` is a Flutter widget that builds itself based on the latest snapshot of asynchronous interaction with a `Future`.

**b. Basic Syntax and Usage:**
   - **Example: Using `FutureBuilder` to Fetch and Display Data**
     ```dart
     import 'package:flutter/material.dart';

     class FutureBuilderExample extends StatelessWidget {
       Future<String> fetchData() async {
         await Future.delayed(Duration(seconds: 2)); // Simulate network delay
         return 'Fetched Data';
       }

       @override
       Widget build(BuildContext context) {
         return Scaffold(
           appBar: AppBar(
             title: Text('FutureBuilder Example'),
           ),
           body: Center(
             child: FutureBuilder<String>(
               future: fetchData(),
               builder: (BuildContext context, AsyncSnapshot<String> snapshot) {
                 if (snapshot.connectionState == ConnectionState.waiting) {
                   return CircularProgressIndicator();
                 } else if (snapshot.hasError) {
                   return Text('Error: ${snapshot.error}');
                 } else {
                   return Text('Data: ${snapshot.data}');
                 }
               },
             ),
           ),
         );
       }
     }
     ```

**c. Handling Different States:**
   - **ConnectionState:** `none`, `waiting`, `active`, `done`.
   - **Snapshot:** Contains data, error, or connection state information.

---

### **3. Using `StreamBuilder`**

**a. What is `StreamBuilder`?**
   - `StreamBuilder` is a Flutter widget that builds itself based on the latest snapshot of interaction with a `Stream`.

**b. Basic Syntax and Usage:**
   - **Example: Using `StreamBuilder` to Display a Data Stream**
     ```dart
     import 'package:flutter/material.dart';

     class StreamBuilderExample extends StatelessWidget {
       Stream<int> numberStream() async* {
         for (int i = 1; i <= 10; i++) {
           await Future.delayed(Duration(seconds: 1)); // Simulate delay
           yield i; // Send new data
         }
       }

       @override
       Widget build(BuildContext context) {
         return Scaffold(
           appBar: AppBar(
             title: Text('StreamBuilder Example'),
           ),
           body: Center(
             child: StreamBuilder<int>(
               stream: numberStream(),
               builder: (BuildContext context, AsyncSnapshot<int> snapshot) {
                 if (snapshot.connectionState == ConnectionState.waiting) {
                   return CircularProgressIndicator();
                 } else if (snapshot.hasError) {
                   return Text('Error: ${snapshot.error}');
                 } else {
                   return Text('Number: ${snapshot.data}');
                 }
               },
             ),
           ),
         );
       }
     }
     ```

**c. Managing Streams:**
   - **StreamController:** Create and manage custom streams.
   - **StreamTransformer:** Apply transformations to the stream's data.

---

### **4. Managing Data Streams and Updating the UI in Real-Time**

**a. Using `StreamController`:**
   - **Example: Creating and Using a `StreamController`**
     ```dart
     import 'dart:async';

     class DataProvider {
       final StreamController<int> _controller = StreamController<int>();

       Stream<int> get stream => _controller.stream;

       void addData(int data) {
         _controller.add(data);
       }

       void dispose() {
         _controller.close();
       }
     }
     ```

**b. Real-Time Data Updates:**
   - **Example: Displaying Real-Time Data with `StreamBuilder`**
     ```dart
     import 'package:flutter/material.dart';

     class RealTimeDataExample extends StatefulWidget {
       @override
       _RealTimeDataExampleState createState() => _RealTimeDataExampleState();
     }

     class _RealTimeDataExampleState extends State<RealTimeDataExample> {
       final DataProvider _dataProvider = DataProvider();

       @override
       void initState() {
         super.initState();
         // Simulate real-time data updates
         Future.periodic(Duration(seconds: 1), (timer) {
           _dataProvider.addData(timer.tick);
         });
       }

       @override
       Widget build(BuildContext context) {
         return Scaffold(
           appBar: AppBar(
             title: Text('Real-Time Data Example'),
           ),
           body: Center(
             child: StreamBuilder<int>(
               stream: _dataProvider.stream,
               builder: (BuildContext context, AsyncSnapshot<int> snapshot) {
                 if (snapshot.connectionState == ConnectionState.waiting) {
                   return CircularProgressIndicator();
                 } else if (snapshot.hasError) {
                   return Text('Error: ${snapshot.error}');
                 } else {
                   return Text('Real-Time Data: ${snapshot.data}');
                 }
               },
             ),
           ),
         );
       }

       @override
       void dispose() {
         _dataProvider.dispose();
         super.dispose();
       }
     }
     ```

**c. Best Practices:**
   - **Resource Management:** Ensure `StreamController` and other resources are properly disposed of.
   - **Error Handling:** Handle potential errors in streams and futures gracefully.
   - **Performance Optimization:** Minimize the number of rebuilds and handle large data efficiently.

---

### **Assignments**

#### **Assignment 1: Real-Time Stock Price Tracker**
- **Objective:** Build an app that streams and displays real-time stock prices.
- **Tasks:**
  1. Create a `StreamController` to manage stock price data.
  2. Use `StreamBuilder` to display real-time updates on the UI.
  3. Implement error handling and display appropriate messages.

#### **Assignment 2: Asynchronous Data Fetching**
- **Objective:** Develop a weather app that fetches weather data asynchronously.
- **Tasks:**
  1. Use `FutureBuilder` to fetch and display current weather conditions.
  2. Handle different states (loading, error, data) appropriately.
  3. Implement a search feature to allow users to get weather updates for different cities.

#### **Assignment 3: Chat Application with Streams**
- **Objective:** Create a basic chat application that uses streams to display messages in real-time.
- **Tasks:**
  1. Use `StreamController` to manage and stream chat messages.
  2. Display messages in a list using `StreamBuilder`.
  3. Implement a simple UI for sending messages and updating the chat view.

#### **Assignment 4: Task Tracker with Future and Stream Builders**
- **Objective:** Develop a task tracker app that uses both `FutureBuilder` and `StreamBuilder`.
- **Tasks:**
  1. Use `FutureBuilder` to fetch initial task data.
  2. Use `StreamBuilder` to display ongoing updates (e.g., tasks being added or completed).
  3. Implement UI for managing and viewing tasks.

---

### **Quick MCQ Quizzes**

1. **What is the purpose of the `FutureBuilder` widget in Flutter?**
   - a) To manage real-time data streams.
   - b) To build widgets based on the latest snapshot of a `Future`.
   - c) To handle synchronous data.
   - d) To display static data.

2. **Which method is used to create a new `Future` in Dart?**
   - a) `Future.create()`
   - b) `Future.delayed()`
   - c) `Future.run()`
   - d) `Future.new()`

3. **What is a `StreamController` used for in Flutter?**
   - a) To manage and control the display of widgets.
   - b) To create and manage streams of asynchronous data.
   - c) To handle HTTP requests.
   - d) To store data persistently.

4. **What widget would you use to handle real-time data updates in Flutter?**
   - a) `FutureBuilder`
   - b) `StreamBuilder`
   - c) `Builder`
   - d) `AsyncSnapshot`

5. **Which method in `StreamBuilder` is used to handle asynchronous data updates?**
   - a) `onData()`
   - b) `onError()`
   - c) `onDone()`
   - d) `

builder()`

---

### **Conclusion**

This session equips students with essential skills for handling asynchronous data in Flutter. By understanding asynchronous programming concepts and mastering the use of `FutureBuilder` and `StreamBuilder`, students can build responsive and dynamic applications that handle real-time data effectively. The assignments and quizzes reinforce practical skills and theoretical knowledge.
