### **Lecture Notes: Session 9 - Navigation and Routing - Part 2**

---

#### **1. Named Routes and Route Generation**

**a. Named Routes:**

- **Definition:** Named routes are identified by a string name rather than a direct widget reference. This approach simplifies navigation and improves code organization.

- **Defining Named Routes:**

  - **Route Table:**
    Define a map of route names to widgets in your `MaterialApp` or `CupertinoApp`.

    ```dart
    MaterialApp(
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

  - **Passing Arguments:**

    ```dart
    Navigator.pushNamed(
      context,
      '/details',
      arguments: 'Some data',
    );
    ```

  - **Receiving Arguments:**

    ```dart
    class DetailsScreen extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        final String data = ModalRoute.of(context)!.settings.arguments as String;

        return Scaffold(
          appBar: AppBar(title: Text('Details')),
          body: Center(
            child: Text('Received data: $data'),
          ),
        );
      }
    }
    ```

**b. Route Generation:**

- **Definition:** Route generation is a more dynamic way to manage routes using a `RouteFactory`. It provides more flexibility for complex navigation scenarios.

- **Setup:**

  - **Using `onGenerateRoute`:**

    ```dart
    MaterialApp(
      onGenerateRoute: (settings) {
        switch (settings.name) {
          case '/':
            return MaterialPageRoute(builder: (context) => HomeScreen());
          case '/details':
            final String data = settings.arguments as String;
            return MaterialPageRoute(
              builder: (context) => DetailsScreen(data: data),
            );
          default:
            return MaterialPageRoute(builder: (context) => UnknownScreen());
        }
      },
    );
    ```

- **Handling Unknown Routes:**

  ```dart
  MaterialApp(
    onUnknownRoute: (settings) {
      return MaterialPageRoute(builder: (context) => UnknownScreen());
    },
  );
  ```

---

#### **2. Using Drawer and BottomNavigationBar for App Navigation**

**a. Drawer:**

- **Definition:** The `Drawer` widget provides a slide-in menu from the side of the screen, commonly used for app-wide navigation.

- **Implementation:**

  ```dart
  Scaffold(
    appBar: AppBar(title: Text('Home')),
    drawer: Drawer(
      child: ListView(
        padding: EdgeInsets.zero,
        children: <Widget>[
          DrawerHeader(
            decoration: BoxDecoration(color: Colors.blue),
            child: Text('Drawer Header', style: TextStyle(color: Colors.white)),
          ),
          ListTile(
            title: Text('Item 1'),
            onTap: () {
              Navigator.pushNamed(context, '/item1');
            },
          ),
          ListTile(
            title: Text('Item 2'),
            onTap: () {
              Navigator.pushNamed(context, '/item2');
            },
          ),
        ],
      ),
    ),
    body: Center(child: Text('Home Screen')),
  );
  ```

**b. BottomNavigationBar:**

- **Definition:** The `BottomNavigationBar` widget provides a bar at the bottom of the screen for app-wide navigation.

- **Implementation:**

  ```dart
  class MyHomePage extends StatefulWidget {
    @override
    _MyHomePageState createState() => _MyHomePageState();
  }

  class _MyHomePageState extends State<MyHomePage> {
    int _selectedIndex = 0;

    void _onItemTapped(int index) {
      setState(() {
        _selectedIndex = index;
      });
    }

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        body: Center(
          child: Text('Selected Index: $_selectedIndex'),
        ),
        bottomNavigationBar: BottomNavigationBar(
          items: <BottomNavigationBarItem>[
            BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
            BottomNavigationBarItem(icon: Icon(Icons.search), label: 'Search'),
            BottomNavigationBarItem(icon: Icon(Icons.notifications), label: 'Notifications'),
            BottomNavigationBarItem(icon: Icon(Icons.account_circle), label: 'Profile'),
          ],
          currentIndex: _selectedIndex,
          onTap: _onItemTapped,
        ),
      );
    }
  }
  ```

---

#### **3. Deep Linking and Handling Back Button Navigation**

**a. Deep Linking:**

- **Definition:** Deep linking allows users to navigate to specific content or pages within an app via URLs.

- **Setup for Deep Linking:**

  - **Android Setup:**
    Configure intent filters in the `AndroidManifest.xml` to handle deep links.

    ```xml
    <intent-filter>
      <action android:name="android.intent.action.VIEW" />
      <category android:name="android.intent.category.DEFAULT" />
      <category android:name="android.intent.category.BROWSABLE" />
      <data android:scheme="myapp" android:host="details" />
    </intent-filter>
    ```

  - **iOS Setup:**
    Configure URL schemes in the `Info.plist` file.

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
      <dict>
        <key>CFBundleURLSchemes</key>
        <array>
          <string>myapp</string>
        </array>
      </dict>
    </array>
    ```

  - **Handling Deep Links:**

    ```dart
    void _handleDeepLink(Uri uri) {
      if (uri.pathSegments.length == 2 && uri.pathSegments.first == 'details') {
        final String id = uri.pathSegments[1];
        Navigator.pushNamed(context, '/details', arguments: id);
      }
    }
    ```

**b. Handling Back Button Navigation:**

- **Default Behavior:** The back button automatically pops the current route off the stack.

- **Custom Back Navigation:**

  - **Using WillPopScope:**
    Wrap your widget with `WillPopScope` to intercept back button presses.

    ```dart
    WillPopScope(
      onWillPop: () async {
        // Perform custom action before popping
        return true; // Return true to allow the pop
      },
      child: Scaffold(
        // Your widget tree
      ),
    );
    ```

- **Programmatic Back Navigation:**

  ```dart
  Navigator.pop(context);
  ```

---

### **Conclusion**

In this session, we expanded on navigation and routing concepts in Flutter, including using named routes and route generation for dynamic navigation, employing `Drawer` and `BottomNavigationBar` for effective app-wide navigation, and handling deep linking and back button navigation. Mastery of these techniques is crucial for building robust and user-friendly navigation experiences in Flutter applications.
