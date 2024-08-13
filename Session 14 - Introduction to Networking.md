### **Session 14: Introduction to Networking**

#### **Objective:**
This session focuses on networking in Flutter, including making HTTP requests, parsing JSON data, displaying fetched data in the UI, and handling errors and network exceptions.

---

### **1. Making HTTP Requests with the `http` Package**

**a. Overview**

- The `http` package provides a simple way to make network requests and handle responses in Flutter.

**b. Setup**

- Add the `http` package to your `pubspec.yaml` file:

  ```yaml
  dependencies:
    flutter:
      sdk: flutter
    http: ^0.14.0
  ```

- Install the package:

  ```bash
  flutter pub get
  ```

**c. Making a GET Request**

- **Example:**

  ```dart
  import 'package:flutter/material.dart';
  import 'package:http/http.dart' as http;
  import 'dart:convert';

  void main() => runApp(MyApp());

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          appBar: AppBar(title: Text('Networking Example')),
          body: DataFetcher(),
        ),
      );
    }
  }

  class DataFetcher extends StatefulWidget {
    @override
    _DataFetcherState createState() => _DataFetcherState();
  }

  class _DataFetcherState extends State<DataFetcher> {
    late Future<List<String>> data;

    @override
    void initState() {
      super.initState();
      data = fetchData();
    }

    Future<List<String>> fetchData() async {
      final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));

      if (response.statusCode == 200) {
        List<dynamic> jsonResponse = json.decode(response.body);
        return jsonResponse.map((post) => post['title'] as String).toList();
      } else {
        throw Exception('Failed to load data');
      }
    }

    @override
    Widget build(BuildContext context) {
      return FutureBuilder<List<String>>(
        future: data,
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return Center(child: CircularProgressIndicator());
          } else if (snapshot.hasError) {
            return Center(child: Text('Error: ${snapshot.error}'));
          } else if (snapshot.hasData) {
            return ListView(
              children: snapshot.data!.map((title) => ListTile(title: Text(title))).toList(),
            );
          } else {
            return Center(child: Text('No data found'));
          }
        },
      );
    }
  }
  ```

- **References:**
  - [http package documentation](https://pub.dev/packages/http)

---

### **2. Parsing JSON Data**

**a. Overview**

- JSON data is parsed using the `dart:convert` package, which provides the `json.decode()` method.

**b. Example**

- **JSON Parsing:**

  ```dart
  import 'dart:convert';

  String jsonResponse = '''
  [
    {"title": "Post 1"},
    {"title": "Post 2"}
  ]
  ''';

  List<dynamic> parsedJson = json.decode(jsonResponse);
  List<String> titles = parsedJson.map((post) => post['title'] as String).toList();
  ```

- **References:**
  - [Dart JSON Documentation](https://dart.dev/guides/json)

---

### **3. Displaying Fetched Data in the UI**

**a. Overview**

- Displaying data fetched from the network typically involves using widgets like `ListView` or `GridView` in combination with `FutureBuilder`.

**b. Example**

- **Using `FutureBuilder`:**

  ```dart
  @override
  Widget build(BuildContext context) {
    return FutureBuilder<List<String>>(
      future: data,
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return Center(child: CircularProgressIndicator());
        } else if (snapshot.hasError) {
          return Center(child: Text('Error: ${snapshot.error}'));
        } else if (snapshot.hasData) {
          return ListView(
            children: snapshot.data!.map((title) => ListTile(title: Text(title))).toList(),
          );
        } else {
          return Center(child: Text('No data found'));
        }
      },
    );
  }
  ```

- **References:**
  - [Flutter ListView Documentation](https://flutter.dev/docs/development/ui/widgets/scrolling#listview)
  - [Flutter FutureBuilder Documentation](https://flutter.dev/docs/development/data-and-backend/futures)

---

### **4. Handling Errors and Network Exceptions**

**a. Overview**

- Proper error handling ensures that users receive meaningful feedback when network requests fail or data is invalid.

**b. Example**

- **Error Handling in HTTP Requests:**

  ```dart
  Future<List<String>> fetchData() async {
    try {
      final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));

      if (response.statusCode == 200) {
        List<dynamic> jsonResponse = json.decode(response.body);
        return jsonResponse.map((post) => post['title'] as String).toList();
      } else {
        throw Exception('Failed to load data');
      }
    } catch (e) {
      throw Exception('Failed to fetch data: $e');
    }
  }
  ```

- **Displaying Errors:**

  ```dart
  @override
  Widget build(BuildContext context) {
    return FutureBuilder<List<String>>(
      future: data,
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return Center(child: CircularProgressIndicator());
        } else if (snapshot.hasError) {
          return Center(child: Text('Error: ${snapshot.error}'));
        } else if (snapshot.hasData) {
          return ListView(
            children: snapshot.data!.map((title) => ListTile(title: Text(title))).toList(),
          );
        } else {
          return Center(child: Text('No data found'));
        }
      },
    );
  }
  ```

- **References:**
  - [Error Handling in Flutter](https://flutter.dev/docs/cookbook/networking/fetch-data)

---

### **Assignments**

#### **Assignment 1: Fetch and Display Data**

- **Objective:** Create a Flutter app that fetches data from a public API and displays it in a `ListView`.
- **Tasks:**
  1. Use the `http` package to make a GET request to a public API (e.g., JSONPlaceholder).
  2. Parse the JSON response and display it in a `ListView`.
  3. Handle network errors and display appropriate error messages.

#### **Assignment 2: Handle API Errors**

- **Objective:** Enhance the previous assignment to handle different types of errors and provide user feedback.
- **Tasks:**
  1. Modify the app to handle HTTP errors and exceptions.
  2. Display error messages in the UI using appropriate widgets.
  3. Implement a retry mechanism for failed network requests.

---

### **Quiz**

1. **Which method is used to decode JSON data in Dart?**
   - a) `json.decode()`
   - b) `json.encode()`
   - c) `json.parse()`
   - d) `json.load()`

2. **What is the purpose of `FutureBuilder` in Flutter?**
   - a) To build UI elements based on future data
   - b) To handle form validation
   - c) To manage state
   - d) To perform synchronous operations

3. **How do you handle HTTP errors in Flutter?**
   - a) By catching exceptions and displaying error messages
   - b) By using `http.get()` with error handling
   - c) By using the `Future` class
   - d) By ignoring errors

4. **What is a common use case for the `ListView` widget in Flutter?**
   - a) Displaying a scrollable list of items
   - b) Showing a single item
   - c) Implementing animations
   - d) Handling form submissions

5. **What should you do if a network request fails?**
   - a) Display a generic error message to the user
   - b) Retry the request automatically
   - c) Show an appropriate error message and provide retry options
   - d) Ignore the error and continue

---

### **Conclusion**

Session 14 introduces essential networking concepts in Flutter, including making HTTP requests, parsing JSON data, and handling errors. Mastery of these concepts allows developers to build apps that can interact with remote services, display dynamic data, and handle network-related issues gracefully.
