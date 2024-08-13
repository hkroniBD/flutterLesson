### **Session 20: Intermediate State Management - Part 1**

#### **Objective:**
This session introduces the Provider package for state management in Flutter. Students will learn how to set up Provider for managing app-wide state, use `ChangeNotifier` to notify listeners of state changes, and leverage `Consumer` to rebuild widgets based on state changes.

---

### **1. Introduction to the Provider Package**

**a. What is Provider?**
   - Provider is a state management solution for Flutter that allows you to manage and expose state to your widget tree. It provides a way to easily pass data down the widget tree and notify widgets when data changes.

**b. Why Use Provider?**
   - **Simplicity:** Simplifies state management with a clean API.
   - **Scalability:** Suitable for both small and large applications.
   - **Performance:** Efficiently rebuilds only the widgets that depend on the changed state.

**c. Key Concepts:**
   - **Provider:** The class that makes state available to widgets.
   - **ChangeNotifier:** A class that holds the state and notifies listeners of changes.
   - **Consumer:** A widget that rebuilds when the state changes.

---

### **2. Setting Up Provider for App-Wide State Management**

**a. Adding Dependencies:**
   - Add the `provider` package to your `pubspec.yaml` file:
     ```yaml
     dependencies:
       flutter:
         sdk: flutter
       provider: ^6.1.3
     ```

**b. Setting Up Provider:**
   - Wrap the root widget of your application with `ChangeNotifierProvider` to make the state available app-wide.
   - Example:
     ```dart
     import 'package:flutter/material.dart';
     import 'package:provider/provider.dart';

     void main() {
       runApp(MyApp());
     }

     class MyApp extends StatelessWidget {
       @override
       Widget build(BuildContext context) {
         return ChangeNotifierProvider(
           create: (context) => CounterModel(),
           child: MaterialApp(
             home: CounterScreen(),
           ),
         );
       }
     }
     ```

**c. Example Application:**
   - **Counter Model:**
     ```dart
     import 'package:flutter/material.dart';

     class CounterModel with ChangeNotifier {
       int _counter = 0;

       int get counter => _counter;

       void increment() {
         _counter++;
         notifyListeners();
       }
     }
     ```

   - **Counter Screen:**
     ```dart
     import 'package:flutter/material.dart';
     import 'package:provider/provider.dart';

     class CounterScreen extends StatelessWidget {
       @override
       Widget build(BuildContext context) {
         return Scaffold(
           appBar: AppBar(
             title: Text('Counter App'),
           ),
           body: Center(
             child: Column(
               mainAxisAlignment: MainAxisAlignment.center,
               children: <Widget>[
                 Text('You have pushed the button this many times:'),
                 Consumer<CounterModel>(
                   builder: (context, counterModel, child) {
                     return Text(
                       '${counterModel.counter}',
                       style: Theme.of(context).textTheme.headline4,
                     );
                   },
                 ),
               ],
             ),
           ),
           floatingActionButton: FloatingActionButton(
             onPressed: () {
               Provider.of<CounterModel>(context, listen: false).increment();
             },
             tooltip: 'Increment',
             child: Icon(Icons.add),
           ),
         );
       }
     }
     ```

---

### **3. Using ChangeNotifier and Consumer**

**a. ChangeNotifier:**
   - `ChangeNotifier` is a class that holds state and provides a `notifyListeners()` method to notify listeners when the state changes. It is used as a base class for models that manage state.

**b. Consumer:**
   - `Consumer` is a widget that listens to changes in the model and rebuilds itself when notified. It provides a way to access the state and rebuild parts of the UI.

**c. Example:**

   - **Using ChangeNotifier:**
     ```dart
     import 'package:flutter/material.dart';

     class CounterModel with ChangeNotifier {
       int _counter = 0;

       int get counter => _counter;

       void increment() {
         _counter++;
         notifyListeners();
       }
     }
     ```

   - **Using Consumer:**
     ```dart
     import 'package:flutter/material.dart';
     import 'package:provider/provider.dart';

     class CounterScreen extends StatelessWidget {
       @override
       Widget build(BuildContext context) {
         return Scaffold(
           appBar: AppBar(
             title: Text('Counter App'),
           ),
           body: Center(
             child: Column(
               mainAxisAlignment: MainAxisAlignment.center,
               children: <Widget>[
                 Text('You have pushed the button this many times:'),
                 Consumer<CounterModel>(
                   builder: (context, counterModel, child) {
                     return Text(
                       '${counterModel.counter}',
                       style: Theme.of(context).textTheme.headline4,
                     );
                   },
                 ),
               ],
             ),
           ),
           floatingActionButton: FloatingActionButton(
             onPressed: () {
               Provider.of<CounterModel>(context, listen: false).increment();
             },
             tooltip: 'Increment',
             child: Icon(Icons.add),
           ),
         );
       }
     }
     ```

---

### **4. Example Application: Simple Todo List with Provider**

**Objective:** Build a simple to-do list application that uses Provider for state management.

**Features:**
1. **Add and Remove Tasks:** Users can add and remove tasks from the list.
2. **List Display:** Display the list of tasks.

**Code Example:**

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => TodoModel(),
      child: MaterialApp(
        home: TodoScreen(),
      ),
    );
  }
}

class TodoModel with ChangeNotifier {
  List<String> _tasks = [];

  List<String> get tasks => _tasks;

  void addTask(String task) {
    _tasks.add(task);
    notifyListeners();
  }

  void removeTask(int index) {
    _tasks.removeAt(index);
    notifyListeners();
  }
}

class TodoScreen extends StatelessWidget {
  final TextEditingController _taskController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Todo List'),
      ),
      body: Column(
        children: <Widget>[
          Padding(
            padding: const EdgeInsets.all(16.0),
            child: TextField(
              controller: _taskController,
              decoration: InputDecoration(labelText: 'New Task'),
            ),
          ),
          ElevatedButton(
            onPressed: () {
              final task = _taskController.text;
              if (task.isNotEmpty) {
                Provider.of<TodoModel>(context, listen: false).addTask(task);
                _taskController.clear();
              }
            },
            child: Text('Add Task'),
          ),
          Expanded(
            child: Consumer<TodoModel>(
              builder: (context, todoModel, child) {
                return ListView.builder(
                  itemCount: todoModel.tasks.length,
                  itemBuilder: (context, index) {
                    return ListTile(
                      title: Text(todoModel.tasks[index]),
                      trailing: IconButton(
                        icon: Icon(Icons.delete),
                        onPressed: () {
                          todoModel.removeTask(index);
                        },
                      ),
                    );
                  },
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}
```

---

### **Assignments**

#### **Assignment 1: Simple Counter App with Provider**
- **Objective:** Create a counter application using Provider for state management.
- **Tasks:**
  1. Implement a counter with increment and decrement functionalities.
  2. Use `ChangeNotifier` to manage the counter state.

#### **Assignment 2: Todo List Application with Provider**
- **Objective:** Build a to-do list application using Provider.
- **Tasks:**
  1. Implement add and remove tasks functionality.
  2. Use `Consumer` to rebuild the list when the task list changes.

---

### **Quiz**

1. **What is the purpose of `ChangeNotifier` in Provider?**
   - a) To handle HTTP requests
   - b) To manage state and notify listeners of changes
   - c) To manage navigation
   - d) To handle animations

2. **Which widget is used to rebuild parts of the UI when the state changes?**
   - a) `Provider`
   - b) `ChangeNotifier`
   - c) `Consumer`
   - d) `Builder`

3. **How do you make a model available app-wide using Provider?**
   - a) Wrap the root widget with `ChangeNotifierProvider`
   - b) Use `Provider.of` in every widget
   - c) Initialize the model in the `main()` function
   - d) Pass the model as a constructor parameter

4. **What method is called to notify listeners of a state change in `ChangeNotifier`?**
   - a) `notifyListeners()`
   - b) `updateListeners()`
   - c) `refresh()`
   - d) `notify()`

5. **Which method in `Provider` allows access to the model without listening to changes?**
   - a) `Provider.of(context)`
   - b) `Provider.read(context)`
   - c) `Provider.listen(context)`
   - d) `Provider.get(context)`

---

### **Conclusion**

Session 20 introduces the Provider package for

 state management, covering how to set it up, use `ChangeNotifier`, and `Consumer`. The session provides practical examples and assignments to reinforce the concepts. The quiz assesses understanding of Provider’s key functionalities and usage.
