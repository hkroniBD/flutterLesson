## Session 4: State Management and Navigation

### Duration
- **Total Time**: 3 hours

### Objectives
By the end of this session, students should be able to:
1. Understand and implement state management in Flutter.
2. Navigate between different screens using Flutter’s navigation system.
3. Use state management techniques to manage and share state across the app.

### Materials Needed
- Laptops with Flutter SDK installed
- Code editor (Visual Studio Code, Android Studio, or IntelliJ IDEA)
- Projector or screen for demonstrations

### Detailed Material

### **1. Introduction to State Management (60 minutes)**

#### **1.1 What is State Management?**
- **Definition**: State management involves managing the state of an application to reflect user interactions and data changes.
- **Types of State**:
  - **Local State**: State managed within a single widget.
  - **Global State**: State shared across multiple widgets or screens.

- **Reference**:
  - [State Management Overview](https://flutter.dev/docs/development/data-and-backend/state-mgmt)

#### **1.2 Local State Management**
- **Using StatefulWidget**:
  - **Purpose**: Manage state that changes over time.
  - **Example**:
    ```dart
    class CounterApp extends StatefulWidget {
      @override
      _CounterAppState createState() => _CounterAppState();
    }

    class _CounterAppState extends State<CounterApp> {
      int _counter = 0;

      void _incrementCounter() {
        setState(() {
          _counter++;
        });
      }

      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(title: Text('Counter')),
          body: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Text('You have pushed the button this many times:'),
                Text('$_counter', style: Theme.of(context).textTheme.headline4),
                ElevatedButton(
                  onPressed: _incrementCounter,
                  child: Text('Increment'),
                ),
              ],
            ),
          ),
        );
      }
    }
    ```

- **Reference**:
  - [Flutter StatefulWidget](https://flutter.dev/docs/development/ui/interactive)

#### **1.3 Global State Management**
- **Provider Package**:
  - **Purpose**: A popular and simple state management solution.
  - **Setup**:
    - **Add Dependency**:
      ```yaml
      dependencies:
        provider: ^6.0.0
      ```
    - **Example Usage**:
      ```dart
      import 'package:flutter/material.dart';
      import 'package:provider/provider.dart';

      void main() => runApp(MyApp());

      class MyApp extends StatelessWidget {
        @override
        Widget build(BuildContext context) {
          return ChangeNotifierProvider(
            create: (context) => CounterModel(),
            child: MaterialApp(
              home: CounterPage(),
            ),
          );
        }
      }

      class CounterModel with ChangeNotifier {
        int _counter = 0;

        int get counter => _counter;

        void increment() {
          _counter++;
          notifyListeners();
        }
      }

      class CounterPage extends StatelessWidget {
        @override
        Widget build(BuildContext context) {
          final counterModel = Provider.of<CounterModel>(context);

          return Scaffold(
            appBar: AppBar(title: Text('Provider Example')),
            body: Center(
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  Text('Counter value: ${counterModel.counter}'),
                  ElevatedButton(
                    onPressed: () => counterModel.increment(),
                    child: Text('Increment'),
                  ),
                ],
              ),
            ),
          );
        }
      }
      ```

- **Reference**:
  - [Provider Documentation](https://pub.dev/packages/provider)

### **2. Navigation in Flutter (60 minutes)**

#### **2.1 Navigating Between Screens**
- **Navigator Widget**:
  - **Purpose**: Manage the stack of screens (routes) in a Flutter app.
  - **Example**:
    ```dart
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => SecondScreen()),
    );
    ```

- **Named Routes**:
  - **Purpose**: Define and manage routes by name.
  - **Setup**:
    ```dart
    MaterialApp(
      routes: {
        '/': (context) => FirstScreen(),
        '/second': (context) => SecondScreen(),
      },
    )
    ```

  - **Navigation**:
    ```dart
    Navigator.pushNamed(context, '/second');
    ```

- **Reference**:
  - [Flutter Navigation](https://flutter.dev/docs/development/ui/navigation)

#### **2.2 Passing Data Between Screens**
- **Passing Data with Navigator**:
  - **Example**:
    ```dart
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => SecondScreen(data: 'Hello from FirstScreen'),
      ),
    );
    ```

  - **Receiving Data**:
    ```dart
    class SecondScreen extends StatelessWidget {
      final String data;

      SecondScreen({required this.data});

      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(title: Text('Second Screen')),
          body: Center(child: Text('Data received: $data')),
        );
      }
    }
    ```

- **Reference**:
  - [Passing Data](https://flutter.dev/docs/cookbook/navigation/passing-data)

#### **2.3 Handling Navigation and State**
- **Returning Data**:
  - **Example**:
    ```dart
    final result = await Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => SecondScreen()),
    );
    ```

  - **Returning Data from Second Screen**:
    ```dart
    Navigator.pop(context, 'Data from Second Screen');
    ```

- **Reference**:
  - [Return Data](https://flutter.dev/docs/cookbook/navigation/returning-data)

### **3. Hands-On Exercise and Practice (30 minutes)**

#### **3.1 Build a Multi-Screen App with State Management**
- **Objective**: Develop a simple multi-screen application that utilizes state management to share and manage data across screens.
- **Exercise**:
  - Create an app with at least two screens.
  - Implement navigation between screens.
  - Use state management (Provider or StatefulWidget) to manage and display data.

- **Reference**:
  - [Flutter State Management and Navigation Examples](https://flutter.dev/docs/cookbook)

### **4. Q&A and Wrap-Up (30 minutes)**

#### **4.1 Addressing Questions**
- Open floor for students to ask questions related to state management and navigation.

#### **4.2 Recap of the Day**
- Summary of key points covered in the session.

#### **4.3 Homework Assignment**
- **Build a Stateful App**:
  - Create an app that uses `StatefulWidget` and `Provider` to manage state. The app should have multiple screens and demonstrate navigation and data sharing.

- **Reference**:
  - [State Management and Navigation Practices](https://flutter.dev/docs/cookbook/navigation)
