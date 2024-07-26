## Session 6: Networking and API Integration

### Duration
- **Total Time**: 3 hours

### Objectives
By the end of this session, students should be able to:
1. Understand and implement basic networking in Flutter.
2. Fetch and display data from a RESTful API.
3. Handle JSON data and integrate with Flutter apps.

### Materials Needed
- Laptops with Flutter SDK installed
- Code editor (Visual Studio Code, Android Studio, or IntelliJ IDEA)
- Projector or screen for demonstrations
- Access to a RESTful API (or a mock API for practice)

### Detailed Material

### **1. Introduction to Networking in Flutter (60 minutes)**

#### **1.1 Overview of HTTP Requests**
- **Definition**: HTTP requests are used to communicate with web services and APIs to fetch or send data.
- **Common Methods**:
  - **GET**: Retrieve data from the server.
  - **POST**: Send data to the server.
  - **PUT/PATCH**: Update data on the server.
  - **DELETE**: Remove data from the server.

- **Reference**:
  - [HTTP Requests Overview](https://flutter.dev/docs/cookbook/networking/fetch-data)

#### **1.2 Using the HTTP Package**
- **Adding Dependency**:
  - **Setup**:
    ```yaml
    dependencies:
      http: ^0.14.0
    ```

- **Basic GET Request**:
  - **Example**:
    ```dart
    import 'package:http/http.dart' as http;

    Future<void> fetchData() async {
      final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

      if (response.statusCode == 200) {
        print('Response data: ${response.body}');
      } else {
        print('Failed to load data');
      }
    }
    ```

- **Reference**:
  - [HTTP Package Documentation](https://pub.dev/packages/http)

#### **1.3 Error Handling in Networking**
- **Handling HTTP Errors**:
  - **Example**:
    ```dart
    Future<void> fetchData() async {
      try {
        final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

        if (response.statusCode == 200) {
          print('Response data: ${response.body}');
        } else {
          print('Error: ${response.statusCode}');
        }
      } catch (e) {
        print('Exception: $e');
      }
    }
    ```

- **Reference**:
  - [Handling Errors](https://flutter.dev/docs/cookbook/networking/errors)

### **2. Fetching and Displaying Data (60 minutes)**

#### **2.1 Parsing JSON Data**
- **Parsing JSON**:
  - **Example**:
    ```dart
    import 'dart:convert';

    Future<void> fetchData() async {
      final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

      if (response.statusCode == 200) {
        final jsonData = jsonDecode(response.body);
        print('Post Title: ${jsonData['title']}');
      } else {
        print('Failed to load data');
      }
    }
    ```

- **Reference**:
  - [Dart JSON Support](https://dart.dev/guides/json)

#### **2.2 Displaying Data in Flutter**
- **Using FutureBuilder**:
  - **Example**:
    ```dart
    import 'package:flutter/material.dart';
    import 'package:http/http.dart' as http;
    import 'dart:convert';

    class MyHomePage extends StatelessWidget {
      Future<Map<String, dynamic>> fetchPost() async {
        final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

        if (response.statusCode == 200) {
          return jsonDecode(response.body);
        } else {
          throw Exception('Failed to load post');
        }
      }

      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(title: Text('Fetch Data Example')),
          body: Center(
            child: FutureBuilder<Map<String, dynamic>>(
              future: fetchPost(),
              builder: (context, snapshot) {
                if (snapshot.connectionState == ConnectionState.waiting) {
                  return CircularProgressIndicator();
                } else if (snapshot.hasError) {
                  return Text('Error: ${snapshot.error}');
                } else {
                  final data = snapshot.data!;
                  return Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: <Widget>[
                      Text('Title: ${data['title']}'),
                      Text('Body: ${data['body']}'),
                    ],
                  );
                }
              },
            ),
          ),
        );
      }
    }
    ```

- **Reference**:
  - [FutureBuilder Documentation](https://flutter.dev/docs/cookbook/networking/fetch-data)

#### **2.3 Handling Network Responses**
- **Different Response States**:
  - **Example**:
    ```dart
    FutureBuilder(
      future: fetchPost(),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return CircularProgressIndicator();
        } else if (snapshot.hasError) {
          return Text('Error: ${snapshot.error}');
        } else {
          return Text('Data: ${snapshot.data}');
        }
      },
    )
    ```

- **Reference**:
  - [Handling Network Responses](https://flutter.dev/docs/cookbook/networking/fetch-data)

### **3. Hands-On Exercise and Practice (30 minutes)**

#### **3.1 Build a Data Fetching App**
- **Objective**: Develop an app that fetches data from a public API and displays it.
- **Exercise**:
  - Create an app that retrieves a list of items from an API and displays them in a `ListView`.
  - Implement error handling and display a message in case of a network error.

- **Reference**:
  - [Fetching and Displaying Data Example](https://flutter.dev/docs/cookbook/networking/fetch-data)

### **4. Q&A and Wrap-Up (30 minutes)**

#### **4.1 Addressing Questions**
- Open floor for students to ask questions related to networking and API integration.

#### **4.2 Recap of the Day**
- Summary of key points covered in the session.

#### **4.3 Homework Assignment**
- **Create an API Integration App**:
  - Build an app that integrates with a RESTful API to perform CRUD operations (Create, Read, Update, Delete). Use appropriate Flutter widgets to handle user input and display data.

- **Reference**:
  - [Advanced Networking Examples](https://flutter.dev/docs/cookbook/networking)
