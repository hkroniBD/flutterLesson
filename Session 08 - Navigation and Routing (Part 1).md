### **Lecture Notes: Session 8 - Navigation and Routing - Part 1**

---

#### **1. Introduction to Navigation and Routing in Flutter**

**a. Navigation Basics:**

- **Definition:** Navigation in Flutter involves moving between different screens or routes in an app. It is essential for creating multi-screen applications.

- **Navigator Widget:** The `Navigator` widget manages a stack of `Route` objects and provides methods to navigate between them.

- **Routes:** Routes are the screens or pages in a Flutter app. A route can be a simple widget or a more complex page.

**b. Key Concepts:**

- **Stack-based Navigation:** Flutter uses a stack-based model for navigation, where routes are pushed onto and popped off the stack.
- **Initial Route:** The initial route is the first route displayed when the app starts.

---

#### **2. Implementing Simple Navigation with Navigator.push and Navigator.pop**

**a. Navigator.push:**

- **Definition:** `Navigator.push` is used to navigate to a new route and add it to the stack.

- **Usage:**
  ```dart
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => NewScreen()),
  );
  ```

- **Example:**
  ```dart
  ElevatedButton(
    onPressed: () {
      Navigator.push(
        context,
        MaterialPageRoute(builder: (context) => SecondScreen()),
      );
    },
    child: Text('Go to Second Screen'),
  );
  ```

**b. Navigator.pop:**

- **Definition:** `Navigator.pop` is used to remove the current route from the stack and return to the previous route.

- **Usage:**
  ```dart
  Navigator.pop(context);
  ```

- **Example:**
  ```dart
  ElevatedButton(
    onPressed: () {
      Navigator.pop(context);
    },
    child: Text('Back to Previous Screen'),
  );
  ```

**c. Example of Simple Navigation:**

1. **First Screen:**
   ```dart
   class FirstScreen extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(title: Text('First Screen')),
         body: Center(
           child: ElevatedButton(
             onPressed: () {
               Navigator.push(
                 context,
                 MaterialPageRoute(builder: (context) => SecondScreen()),
               );
             },
             child: Text('Go to Second Screen'),
           ),
         ),
       );
     }
   }
   ```

2. **Second Screen:**
   ```dart
   class SecondScreen extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(title: Text('Second Screen')),
         body: Center(
           child: ElevatedButton(
             onPressed: () {
               Navigator.pop(context);
             },
             child: Text('Back to First Screen'),
           ),
         ),
       );
     }
   }
   ```

---

#### **3. Passing Data Between Screens**

**a. Passing Data with Constructor:**

- **Definition:** You can pass data to a new route using its constructor when pushing the route.

- **Example:**

  1. **Second Screen with Data:**
     ```dart
     class SecondScreen extends StatelessWidget {
       final String data;

       SecondScreen({required this.data});

       @override
       Widget build(BuildContext context) {
         return Scaffold(
           appBar: AppBar(title: Text('Second Screen')),
           body: Center(
             child: Text('Data received: $data'),
           ),
         );
       }
     }
     ```

  2. **Passing Data:**
     ```dart
     Navigator.push(
       context,
       MaterialPageRoute(
         builder: (context) => SecondScreen(data: 'Hello from First Screen'),
       ),
     );
     ```

**b. Using `Navigator.pushNamed` and `Navigator.pop` with Arguments:**

- **Definition:** `Navigator.pushNamed` allows navigation using route names and passing arguments.

- **Usage:**

  1. **Define Routes:**
     ```dart
     final Map<String, WidgetBuilder> routes = {
       '/second': (context) => SecondScreen(),
     };

     MaterialApp(
       routes: routes,
       home: FirstScreen(),
     );
     ```

  2. **Passing Data:**
     ```dart
     Navigator.pushNamed(
       context,
       '/second',
       arguments: 'Hello from First Screen',
     );
     ```

  3. **Receiving Data:**
     ```dart
     class SecondScreen extends StatelessWidget {
       @override
       Widget build(BuildContext context) {
         final String data = ModalRoute.of(context)!.settings.arguments as String;

         return Scaffold(
           appBar: AppBar(title: Text('Second Screen')),
           body: Center(
             child: Text('Data received: $data'),
           ),
         );
       }
     }
     ```

**c. Example of Passing Data with Named Routes:**

1. **First Screen:**
   ```dart
   class FirstScreen extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(title: Text('First Screen')),
         body: Center(
           child: ElevatedButton(
             onPressed: () {
               Navigator.pushNamed(
                 context,
                 '/second',
                 arguments: 'Hello from First Screen',
               );
             },
             child: Text('Go to Second Screen'),
           ),
         ),
       );
     }
   }
   ```

2. **Second Screen:**
   ```dart
   class SecondScreen extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       final String data = ModalRoute.of(context)!.settings.arguments as String;

       return Scaffold(
         appBar: AppBar(title: Text('Second Screen')),
         body: Center(
           child: Text('Data received: $data'),
         ),
       );
     }
   }
   ```

---

### **Conclusion**

In this session, we covered the basics of navigation and routing in Flutter, including implementing simple navigation with `Navigator.push` and `Navigator.pop`, and passing data between screens. Understanding these fundamental concepts is crucial for building multi-screen applications and managing user flows effectively in Flutter.
