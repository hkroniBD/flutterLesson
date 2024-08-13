### **Session 14: Introduction to Networking**

#### **Objective:**
This session will introduce the fundamentals of networking in Flutter, focusing on making HTTP requests, parsing JSON data, displaying the data in the UI, and handling potential errors or network exceptions. By the end of this session, students should be able to fetch and display data from a remote server in a Flutter app.

---

### **1. Making HTTP Requests with the `http` Package**

**a. Introduction to the `http` Package:**
   - The `http` package in Flutter is a powerful tool that simplifies making HTTP requests. It supports GET, POST, PUT, DELETE, and other HTTP methods.

**b. Installing the `http` Package:**
   - Add the following dependency in your `pubspec.yaml` file:
     ```yaml
     dependencies:
       http: ^0.13.4
     ```
   - Run `flutter pub get` to install the package.

**c. Making a Simple GET Request:**
   - **Example: Fetching Data from a Public API**
     ```dart
     import 'package:flutter/material.dart';
     import 'package:http/http.dart' as http;
     import 'dart:convert';

     class NetworkingExample extends StatefulWidget {
       @override
       _NetworkingExampleState createState() => _NetworkingExampleState();
     }

     class _NetworkingExampleState extends State<NetworkingExample> {
       String _data = '';

       Future<void> fetchData() async {
         final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

         if (response.statusCode == 200) {
           setState(() {
             _data = jsonDecode(response.body)['title'];
           });
         } else {
           throw Exception('Failed to load data');
         }
       }

       @override
       void initState() {
         super.initState();
         fetchData();
       }

       @override
       Widget build(BuildContext context) {
         return Scaffold(
           appBar: AppBar(
             title: Text('Networking Example'),
           ),
           body: Center(
             child: _data.isEmpty ? CircularProgressIndicator() : Text(_data),
           ),
         );
       }
     }
     ```
   - **Explanation:**
     - The `http.get()` method is used to fetch data from the API.
     - `jsonDecode()` is used to parse the JSON response.
     - The response is displayed in a `Text` widget.

---

### **2. Parsing JSON Data**

**a. Understanding JSON Structure:**
   - JSON (JavaScript Object Notation) is a lightweight data-interchange format that is easy to read and write for humans and machines. In Flutter, JSON data is usually represented as a map.

**b. Parsing JSON in Flutter:**
   - **Example: Converting JSON String to Dart Objects**
     ```dart
     String jsonString = '{"id": 1, "title": "Hello, Flutter!"}';
     Map<String, dynamic> userMap = jsonDecode(jsonString);
     print('Title: ${userMap['title']}');
     ```

**c. Working with Complex JSON Structures:**
   - **Example: Parsing Nested JSON**
     ```dart
     String jsonString = '''
     {
       "user": {
         "id": 1,
         "name": "John Doe",
         "email": "johndoe@example.com"
       }
     }
     ''';

     Map<String, dynamic> userMap = jsonDecode(jsonString);
     print('User Name: ${userMap['user']['name']}');
     ```

**d. Model Class for JSON Parsing:**
   - **Example: Creating a Dart Model for API Data**
     ```dart
     class Post {
       final int id;
       final String title;

       Post({required this.id, required this.title});

       factory Post.fromJson(Map<String, dynamic> json) {
         return Post(
           id: json['id'],
           title: json['title'],
         );
       }
     }

     Future<Post> fetchPost() async {
       final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

       if (response.statusCode == 200) {
         return Post.fromJson(jsonDecode(response.body));
       } else {
         throw Exception('Failed to load post');
       }
     }
     ```

---

### **3. Displaying Fetched Data in the UI**

**a. Using `FutureBuilder` to Handle Asynchronous Data:**
   - **Example: Displaying Data from an API**
     ```dart
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text('Display Data'),
         ),
         body: FutureBuilder<Post>(
           future: fetchPost(),
           builder: (context, snapshot) {
             if (snapshot.connectionState == ConnectionState.waiting) {
               return Center(child: CircularProgressIndicator());
             } else if (snapshot.hasError) {
               return Center(child: Text('Error: ${snapshot.error}'));
             } else if (snapshot.hasData) {
               return Center(child: Text('Title: ${snapshot.data!.title}'));
             } else {
               return Center(child: Text('No data available'));
             }
           },
         ),
       );
     }
     ```

**b. Customizing the UI Based on the Data:**
   - You can style the UI, display images, or show additional data based on the fetched data.

---

### **4. Handling Errors and Network Exceptions**

**a. Common Error Scenarios:**
   - **Network Unavailability:** No internet connection.
   - **Server Errors:** 404 Not Found, 500 Internal Server Error.
   - **Parsing Errors:** Incorrect or unexpected JSON format.

**b. Implementing Error Handling:**
   - **Example: Handling Network Errors**
     ```dart
     Future<void> fetchData() async {
       try {
         final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts/1'));

         if (response.statusCode == 200) {
           // Parse the JSON
         } else {
           throw Exception('Failed to load data');
         }
       } on SocketException {
         // Handle network error
         print('No Internet connection');
       } catch (e) {
         // Handle other exceptions
         print('Error: $e');
       }
     }
     ```

**c. Displaying Error Messages in the UI:**
   - Inform the user of any errors using dialogs, snack bars, or error messages in the UI.

---

### **Assignments**

#### **Assignment 1: Fetch and Display User Data**
- **Objective:** Create an app that fetches user data from an API and displays the user’s name, email, and other details on the screen.
- **Tasks:**
  1. Fetch data from the `https://jsonplaceholder.typicode.com/users` endpoint.
  2. Parse the JSON data to extract user information.
  3. Display the user details in a styled UI.

#### **Assignment 2: Post Request and Error Handling**
- **Objective:** Develop a form that sends data to an API via a POST request. Handle errors like network unavailability and server errors.
- **Tasks:**
  1. Create a form with fields for title and body.
  2. Send the form data as a POST request to the `https://jsonplaceholder.typicode.com/posts` endpoint.
  3. Display the response or an error message based on the outcome.

#### **Assignment 3: Parsing Complex JSON**
- **Objective:** Work with a complex JSON structure that includes nested objects and arrays. Parse the JSON and display it in a structured way.
- **Tasks:**
  1. Fetch data from a nested JSON endpoint.
  2. Parse and display the nested objects and arrays in a structured UI.

#### **Assignment 4: Implementing Offline Support**
- **Objective:** Create an app that can fetch and display data even when offline by storing the data locally using a package like `shared_preferences`.
- **Tasks:**
  1. Fetch data from an API and store it locally.
  2. Implement logic to display the locally stored data when the app is offline.

---

### **Quick MCQ Quizzes**

1. **Which package is commonly used for making HTTP requests in Flutter?**
   - a) flutter_http
   - b) http_request
   - c) http
   - d) network

2. **What is the correct way to parse a JSON string in Dart?**
   - a) `json.parse(jsonString)`
   - b) `JSON.parse(jsonString)`
   - c) `jsonDecode(jsonString)`
   - d) `parseJson(jsonString)`

3. **Which widget is best suited for displaying data fetched from an API asynchronously?**
   - a) `StreamBuilder`
   - b) `FutureBuilder`
   - c) `Builder`
   - d) `Scaffold`

4. **What error might you encounter if there is no internet connection while making an HTTP request?**
   - a) `SocketException`
   - b) `NoSuchMethodError`
   - c) `NullPointerException`
   - d) `TypeError`

5. **Which method is used to send a POST request using the `http` package?**
   - a) `http.send()`
   - b) `http.request()`
   - c) `http.post()`
   - d) `http.push()`

---

### **Conclusion**

This session provides a comprehensive introduction to networking in Flutter, equipping students with the skills to make HTTP requests, parse JSON data, handle errors, and display network data in their apps. The assignments and quizzes reinforce the concepts and give students practical experience with real-world scenarios.
