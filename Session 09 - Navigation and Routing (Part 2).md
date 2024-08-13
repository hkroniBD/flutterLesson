### **Session 9: Navigation and Routing - Part 2**

#### **Objective:**
This session builds on the basics of navigation and routing, introducing named routes, route generation, advanced navigation widgets such as `Drawer` and `BottomNavigationBar`, and handling deep linking and back button navigation in Flutter.

---

### **1. Named Routes and Route Generation**

**a. Named Routes:**

- **Definition:**
  - Named routes are a way to manage navigation by defining routes with unique names in your app’s route table. This allows for easier navigation and management of routes.

- **Setting Up Named Routes:**
  - **Define Routes:**
    ```dart
    MaterialApp(
      title: 'My App',
      initialRoute: '/',
      routes: {
        '/': (context) => HomeScreen(),
        '/details': (context) => DetailsScreen(),
      },
    );
    ```
  - **Navigating to Named Routes:**
    ```dart
    Navigator.pushNamed(context, '/details');
    ```

- **References:**
  - [Flutter Named Routes Documentation](https://flutter.dev/docs/development/ui/navigation/named-routes)

**b. Route Generation:**

- **Definition:**
  - Route generation allows for more dynamic route creation by using a callback function that generates routes based on the `RouteSettings`.

- **Implementing Route Generation:**
  - **Setup:**
    ```dart
    MaterialApp(
      title: 'My App',
      onGenerateRoute: (settings) {
        switch (settings.name) {
          case '/':
            return MaterialPageRoute(builder: (context) => HomeScreen());
          case '/details':
            return MaterialPageRoute(builder: (context) => DetailsScreen());
          default:
            return MaterialPageRoute(builder: (context) => NotFoundScreen());
        }
      },
    );
    ```

- **References:**
  - [Flutter Route Generation Documentation](https://flutter.dev/docs/development/ui/navigation/generate-routes)

---

### **2. Using Drawer and BottomNavigationBar for App Navigation**

**a. Drawer:**

- **Definition:**
  - A `Drawer` provides a side menu that slides out from the left of the screen. It is typically used for app-wide navigation.

- **Implementation:**
  - **Basic Example:**
    ```dart
    Scaffold(
      appBar: AppBar(title: Text('My App')),
      drawer: Drawer(
        child: ListView(
          padding: EdgeInsets.zero,
          children: <Widget>[
            DrawerHeader(child: Text('Menu')),
            ListTile(title: Text('Home'), onTap: () { Navigator.pushNamed(context, '/'); }),
            ListTile(title: Text('Details'), onTap: () { Navigator.pushNamed(context, '/details'); }),
          ],
        ),
      ),
      body: Center(child: Text('Content')),
    );
    ```

- **References:**
  - [Flutter Drawer Documentation](https://flutter.dev/docs/development/ui/widgets/material#drawer)

**b. BottomNavigationBar:**

- **Definition:**
  - A `BottomNavigationBar` provides a navigation bar at the bottom of the screen, often used to switch between major sections of an app.

- **Implementation:**
  - **Basic Example:**
    ```dart
    Scaffold(
      appBar: AppBar(title: Text('My App')),
      body: Center(child: Text('Content')),
      bottomNavigationBar: BottomNavigationBar(
        items: const <BottomNavigationBarItem>[
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
          BottomNavigationBarItem(icon: Icon(Icons.search), label: 'Search'),
        ],
        currentIndex: _selectedIndex,
        onTap: _onItemTapped,
      ),
    );
    
    void _onItemTapped(int index) {
      setState(() {
        _selectedIndex = index;
      });
    }
    ```

- **References:**
  - [Flutter BottomNavigationBar Documentation](https://flutter.dev/docs/development/ui/widgets/material#bottomnavigationbar)

---

### **3. Deep Linking and Handling Back Button Navigation**

**a. Deep Linking:**

- **Definition:**
  - Deep linking allows users to navigate to specific content within the app using URLs.

- **Implementation:**
  - **Setup for Android:**
    - Add intent filters in `AndroidManifest.xml`.
  - **Setup for iOS:**
    - Configure URL schemes in Xcode.

- **References:**
  - [Flutter Deep Linking Documentation](https://flutter.dev/docs/development/ui/navigation/deep-linking)

**b. Handling Back Button Navigation:**

- **Definition:**
  - Managing the behavior of the back button in Flutter to ensure users navigate correctly between screens.

- **Implementation:**
  - **Using `WillPopScope`:**
    ```dart
    WillPopScope(
      onWillPop: () async {
        // Handle back button press
        return true; // Return true to allow back navigation
      },
      child: Scaffold(
        appBar: AppBar(title: Text('My App')),
        body: Center(child: Text('Content')),
      ),
    );
    ```

- **References:**
  - [Flutter WillPopScope Documentation](https://flutter.dev/docs/development/ui/widgets/async#willpopscope)

---

### **Assignments**

#### **Assignment 1: Named Routes and Route Generation**

- **Objective:** Implement and utilize named routes and route generation.
- **Tasks:**
  1. Define named routes for your app and navigate between them.
  2. Implement route generation to handle dynamic routes.

#### **Assignment 2: Navigation Widgets**

- **Objective:** Use `Drawer` and `BottomNavigationBar` in a Flutter app.
- **Tasks:**
  1. Create a `Drawer` with navigation options for at least three screens.
  2. Implement a `BottomNavigationBar` with at least two tabs, each displaying different content.

#### **Assignment 3: Deep Linking**

- **Objective:** Configure deep linking in a Flutter app.
- **Tasks:**
  1. Set up deep linking for both Android and iOS platforms.
  2. Create a link that navigates to a specific screen within the app.

---

### **Quiz**

1. **What is the purpose of named routes in Flutter?**
   - a) To manage app-wide state
   - b) To provide unique identifiers for routes
   - c) To handle asynchronous operations
   - d) To manage app themes

2. **Which widget provides a side menu for app-wide navigation?**
   - a) BottomNavigationBar
   - b) Drawer
   - c) TabBar
   - d) AppBar

3. **How can you handle back button navigation in Flutter?**
   - a) Using `Navigator.push`
   - b) Using `WillPopScope`
   - c) Using `Drawer`
   - d) Using `BottomNavigationBar`

4. **What is deep linking used for in Flutter apps?**
   - a) Navigating between screens within the app using URLs
   - b) Managing app-wide state
   - c) Implementing animations
   - d) Handling user input

5. **What method is used to navigate to a named route?**
   - a) Navigator.pop
   - b) Navigator.pushNamed
   - c) Navigator.replace
   - d) Navigator.switch

---

### **Conclusion**

Session 9 covers advanced navigation techniques in Flutter, including named routes, route generation, and using `Drawer` and `BottomNavigationBar` for app navigation. It also introduces deep linking and handling back button navigation, essential for creating complex navigation structures in Flutter apps. Understanding these concepts will enhance your ability to build well-structured and user-friendly applications.
