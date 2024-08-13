### **Session 15: Working with RESTful APIs**

#### **Objective:**
This session will delve into the intricacies of working with RESTful APIs in Flutter. Students will learn how to send various HTTP requests (POST, PUT, DELETE), work with query parameters and headers, and consume third-party APIs effectively.

---

### **1. Implementing RESTful APIs in Flutter**

**a. What are RESTful APIs?**
   - REST (Representational State Transfer) is an architectural style for designing networked applications. It relies on stateless communication, usually over HTTP, and allows clients to interact with resources identified by URLs.

**b. Understanding CRUD Operations:**
   - **Create (POST):** Add a new resource.
   - **Read (GET):** Retrieve a resource.
   - **Update (PUT/PATCH):** Modify an existing resource.
   - **Delete (DELETE):** Remove a resource.

**c. Setting Up the `http` Package:**
   - Add the `http` package to your `pubspec.yaml` file:
     ```yaml
     dependencies:
       http: ^0.13.4
     ```
   - Run `flutter pub get` to install the package.

**d. Making RESTful API Calls:**
   - **Example: Setting Up a Basic API Client**
     ```dart
     import 'package:http/http.dart' as http;

     class ApiClient {
       final String baseUrl = "https://jsonplaceholder.typicode.com";

       Future<http.Response> getRequest(String endpoint) async {
         return await http.get(Uri.parse('$baseUrl/$endpoint'));
       }

       Future<http.Response> postRequest(String endpoint, Map<String, dynamic> data) async {
         return await http.post(Uri.parse('$baseUrl/$endpoint'), body: data);
       }

       Future<http.Response> putRequest(String endpoint, Map<String, dynamic> data) async {
         return await http.put(Uri.parse('$baseUrl/$endpoint'), body: data);
       }

       Future<http.Response> deleteRequest(String endpoint) async {
         return await http.delete(Uri.parse('$baseUrl/$endpoint'));
       }
     }
     ```

---

### **2. Sending POST, PUT, and DELETE Requests**

**a. Sending POST Requests:**
   - **Example: Creating a New Resource**
     ```dart
     Future<void> createPost() async {
       final response = await ApiClient().postRequest('posts', {
         'title': 'New Post',
         'body': 'This is the body of the post',
         'userId': 1,
       });

       if (response.statusCode == 201) {
         print('Post created successfully: ${response.body}');
       } else {
         throw Exception('Failed to create post');
       }
     }
     ```

**b. Sending PUT Requests:**
   - **Example: Updating an Existing Resource**
     ```dart
     Future<void> updatePost(int id) async {
       final response = await ApiClient().putRequest('posts/$id', {
         'title': 'Updated Post',
         'body': 'This is the updated body of the post',
         'userId': 1,
       });

       if (response.statusCode == 200) {
         print('Post updated successfully: ${response.body}');
       } else {
         throw Exception('Failed to update post');
       }
     }
     ```

**c. Sending DELETE Requests:**
   - **Example: Deleting a Resource**
     ```dart
     Future<void> deletePost(int id) async {
       final response = await ApiClient().deleteRequest('posts/$id');

       if (response.statusCode == 200) {
         print('Post deleted successfully');
       } else {
         throw Exception('Failed to delete post');
       }
     }
     ```

---

### **3. Working with Query Parameters and Headers**

**a. Adding Query Parameters:**
   - Query parameters allow you to pass additional data to the server through the URL.
   - **Example: Fetching Data with Query Parameters**
     ```dart
     Future<void> fetchPosts({int userId = 1}) async {
       final response = await ApiClient().getRequest('posts?userId=$userId');

       if (response.statusCode == 200) {
         print('Posts fetched successfully: ${response.body}');
       } else {
         throw Exception('Failed to fetch posts');
       }
     }
     ```

**b. Setting HTTP Headers:**
   - Headers provide additional information about the request, such as content type, authentication tokens, etc.
   - **Example: Adding Custom Headers**
     ```dart
     Future<void> fetchPostsWithHeaders() async {
       final response = await http.get(
         Uri.parse('https://jsonplaceholder.typicode.com/posts'),
         headers: {
           'Authorization': 'Bearer YOUR_TOKEN',
           'Accept': 'application/json',
         },
       );

       if (response.statusCode == 200) {
         print('Posts fetched with headers: ${response.body}');
       } else {
         throw Exception('Failed to fetch posts');
       }
     }
     ```

---

### **4. Consuming Third-Party APIs**

**a. Finding and Using Public APIs:**
   - Numerous public APIs are available for consumption, providing data such as weather information, news, stock prices, etc.

**b. Example: Consuming a Third-Party Weather API:**
   - **Step 1: Get an API Key**
     - Sign up for an API key from a weather service provider like OpenWeatherMap.
   - **Step 2: Make API Calls**
     ```dart
     Future<void> fetchWeather(String city) async {
       final apiKey = 'YOUR_API_KEY';
       final response = await http.get(
         Uri.parse('https://api.openweathermap.org/data/2.5/weather?q=$city&appid=$apiKey'),
       );

       if (response.statusCode == 200) {
         print('Weather data: ${response.body}');
       } else {
         throw Exception('Failed to fetch weather data');
       }
     }
     ```

**c. Handling Authentication with APIs:**
   - Some APIs require authentication via API keys, OAuth tokens, etc. Ensure your requests include the necessary credentials.

**d. Displaying Third-Party Data in Your App:**
   - After fetching data from an API, parse it and display it in your app using widgets like `ListView`, `GridView`, or custom UI components.

---

### **Assignments**

#### **Assignment 1: Create a To-Do App with RESTful API Integration**
- **Objective:** Develop a simple To-Do app that interacts with a RESTful API to create, read, update, and delete tasks.
- **Tasks:**
  1. Set up API calls for CRUD operations using the `http` package.
  2. Display tasks in a list, allowing the user to add, edit, and delete tasks.
  3. Implement error handling and feedback (e.g., showing a snackbar on success/failure).

#### **Assignment 2: User Authentication with RESTful API**
- **Objective:** Implement a user authentication system in your app, allowing users to sign up, log in, and log out using a RESTful API.
- **Tasks:**
  1. Create forms for user registration and login.
  2. Send POST requests to the API to register and log in users.
  3. Store the authentication token securely and use it for authorized requests.

#### **Assignment 3: Fetch and Display News Articles**
- **Objective:** Consume a third-party news API to fetch and display the latest news articles.
- **Tasks:**
  1. Make a GET request to fetch news articles from a public API.
  2. Parse the JSON response and display the articles in a list.
  3. Implement search functionality to filter articles based on keywords.

#### **Assignment 4: Weather App with API Integration**
- **Objective:** Create a weather app that fetches and displays weather information for a user-specified city.
- **Tasks:**
  1. Use a weather API to fetch data based on the city entered by the user.
  2. Display current weather conditions and a forecast.
  3. Handle errors such as invalid city names or network issues.

---

### **Quick MCQ Quizzes**

1. **Which HTTP method is used to update an existing resource?**
   - a) GET
   - b) POST
   - c) PUT
   - d) DELETE

2. **What is the purpose of query parameters in a URL?**
   - a) To provide additional data to the server.
   - b) To authenticate the request.
   - c) To specify the HTTP method.
   - d) To encrypt the request.

3. **Which of the following is a valid HTTP status code for a successful POST request?**
   - a) 200
   - b) 201
   - c) 404
   - d) 500

4. **What package is commonly used in Flutter for making HTTP requests?**
   - a) flutter_http
   - b) dio
   - c) http
   - d) flutter_network

5. **Which of the following is an example of a third-party API?**
   - a) JSONPlaceholder
   - b) RESTful
   - c) HTTP
   - d) API Client

---

### **Conclusion**

This session equips students with the essential skills needed to work with RESTful APIs in Flutter. By understanding how to send various HTTP requests, handle query parameters and headers, and consume third-party APIs, students will be prepared to integrate backend services into their Flutter applications effectively. The assignments and quizzes provide practical experience and reinforce key concepts.
