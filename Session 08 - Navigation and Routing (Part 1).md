### **Session 8: Navigation and Routing - Part 1**

#### **Objective:**
This session introduces navigation and routing in Flutter, focusing on basic navigation techniques, passing data between screens, and understanding the core concepts behind Flutter's navigation system.

---

### **1. Introduction to Navigation and Routing in Flutter**

**a. Overview of Navigation:**

- **Definition:**
  - Navigation refers to the process of moving between different screens or routes in a Flutter application. Flutter uses the `Navigator` widget to manage routes and navigation.

- **Key Concepts:**
  - **Route:** Represents a screen or page in your app.
  - **Navigator:** A widget that manages a stack of routes and provides methods to push and pop routes.

- **References:**
  - [Flutter Navigation Documentation](https://flutter.dev/docs/development/ui/navigation)

**b. Route Management:**

- **Named Routes vs. Anonymous Routes:**
  - **Named Routes:** Routes are registered with a name in the app’s route table and navigated to using that name.
  - **Anonymous Routes:** Routes are defined inline and used immediately.

- **References:**
  - [Named Routes Documentation](https://flutter.dev/docs/development/ui/navigation/named-routes)
  - [Anonymous Routes Documentation](https://flutter.dev/docs/development/ui/navigation/route-arguments)

---

### **2. Implementing Simple Navigation with `Navigator.push` and `Navigator.pop`**

**a. Navigating to a New Screen:**

- **Definition:**
  - Use `Navigator.push` to navigate to a new route and add it to the stack.

- **Syntax Example:**
  ```dart
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => SecondScreen()),
  );
  ```

- **References:**
  - [Navigator Documentation](https://flutter.dev/docs/development/ui/navigation#navigator)

**b. Returning to the Previous Screen:**

- **Definition:**
  - Use `Navigator.pop` to remove the top route from the stack and return to the previous screen.

- **Syntax Example:**
  ```dart
  Navigator.pop(context);
  ```

- **References:**
  - [Navigator.pop Documentation](https://flutter.dev/docs/development/ui/navigation#pop)

---

### **3. Passing Data Between Screens**

**a. Passing Data Using Constructor Parameters:**

- **Definition:**
  - You can pass data to a new screen by including parameters in the constructor of the destination screen.

- **Syntax Example:**
  ```dart
  // FirstScreen.dart
  Navigator.push(
    context,
    MaterialPageRoute(
      builder: (context) => SecondScreen(data: 'Hello from FirstScreen'),
    ),
  );
  
  // SecondScreen.dart
  class SecondScreen extends StatelessWidget {
    final String data;

    SecondScreen({required this.data});

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Second Screen'),
        ),
        body: Center(
          child: Text(data),
        ),
      );
    }
  }
  ```

- **References:**
  - [Passing Data Between Screens Documentation](https://flutter.dev/docs/development/ui/navigation/route-arguments)

**b. Using `Navigator` and `ModalRoute` to Retrieve Data:**

- **Definition:**
  - Use `ModalRoute.of(context)?.settings.arguments` to retrieve arguments passed to a route.

- **Syntax Example:**
  ```dart
  // FirstScreen.dart
  Navigator.pushNamed(
    context,
    '/second',
    arguments: 'Hello from FirstScreen',
  );
  
  // SecondScreen.dart
  class SecondScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      final String data = ModalRoute.of(context)?.settings.arguments as String;

      return Scaffold(
        appBar: AppBar(
          title: Text('Second Screen'),
        ),
        body: Center(
          child: Text(data),
        ),
      );
    }
  }
  ```

- **References:**
  - [Using ModalRoute Documentation](https://flutter.dev/docs/development/ui/navigation/route-arguments)

---

### **Assignments**

#### **Assignment 1: Basic Navigation**

- **Objective:** Implement basic navigation between two screens.
- **Tasks:**
  1. Create two screens: `HomeScreen` and `DetailsScreen`.
  2. Implement a button on `HomeScreen` that navigates to `DetailsScreen` using `Navigator.push`.
  3. Add a button on `DetailsScreen` that returns to `HomeScreen` using `Navigator.pop`.

#### **Assignment 2: Passing Data Between Screens**

- **Objective:** Pass data from one screen to another.
- **Tasks:**
  1. Modify the `DetailsScreen` to accept a string parameter in its constructor.
  2. Pass a string value from `HomeScreen` to `DetailsScreen` when navigating.
  3. Display the passed string on `DetailsScreen`.

---

### **Quiz**

1. **Which method is used to navigate to a new screen in Flutter?**
   - a) Navigator.push
   - b) Navigator.pop
   - c) Navigator.replace
   - d) Navigator.switch

2. **How can you pass data to a new screen using a constructor?**
   - a) Use `Navigator.push` with arguments
   - b) Use `Navigator.pop` with arguments
   - c) Use `Navigator.push` with a `MaterialPageRoute` and pass the data in the constructor
   - d) Use `Navigator.pushNamed` with settings

3. **Which method is used to return to the previous screen?**
   - a) Navigator.push
   - b) Navigator.pop
   - c) Navigator.remove
   - d) Navigator.back

4. **What is the purpose of `ModalRoute.of(context)?.settings.arguments`?**
   - a) To navigate to a new screen
   - b) To retrieve data passed to a route
   - c) To manage navigation history
   - d) To define route names

5. **What is the primary difference between named and anonymous routes in Flutter?**
   - a) Named routes are used for dynamic data, while anonymous routes are static.
   - b) Named routes are registered in the route table, while anonymous routes are defined inline.
   - c) Named routes are for iOS only, while anonymous routes are for Android only.
   - d) Named routes use `Navigator.push`, while anonymous routes use `Navigator.pop`.

---

### **Conclusion**

Session 8 covers the fundamental concepts of navigation and routing in Flutter. It introduces how to navigate between screens, pass data between routes, and understand the basic navigation concepts in Flutter applications. Mastering these techniques is essential for creating multi-screen apps with smooth user experiences.
