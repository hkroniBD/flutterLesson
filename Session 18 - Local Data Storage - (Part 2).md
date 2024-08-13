### **Session 18: Local Data Storage - Part 2**

#### **Objective:**
This session introduces the Hive database for local data storage in Flutter. Students will learn how to set up Hive, perform basic CRUD operations, and manage data efficiently.

---

### **1. Introduction to Hive Database**

**a. What is Hive?**
   - Hive is a lightweight and fast key-value database written in Dart. It is designed for Flutter and Dart applications to provide a NoSQL storage solution.

**b. Why Use Hive?**
   - Fast performance due to its efficient binary format.
   - Simple and intuitive API.
   - Suitable for storing structured and unstructured data.
   - No need for a network connection.

**c. When to Use Hive:**
   - Ideal for applications that require offline data storage, such as user settings, app state, or data caching.

---

### **2. Setting Up Hive in a Flutter Project**

**a. Adding Dependencies:**
   - Add Hive and Hive Flutter dependencies to your `pubspec.yaml` file:
     ```yaml
     dependencies:
       flutter:
         sdk: flutter
       hive: ^2.2.1
       hive_flutter: ^1.1.0
     dev_dependencies:
       hive_generator: ^1.1.1
       build_runner: ^2.1.8
     ```

**b. Initial Setup:**
   - **1. Initialize Hive:**
     - Hive must be initialized before using it. This is usually done in the `main()` method of your app.
     ```dart
     import 'package:flutter/material.dart';
     import 'package:hive_flutter/hive_flutter.dart';

     void main() async {
       WidgetsFlutterBinding.ensureInitialized();
       await Hive.initFlutter();
       runApp(MyApp());
     }
     ```

**c. Create a Hive Box:**
   - **1. Opening a Box:**
     - A box is a collection of key-value pairs. Open a box before using it.
     ```dart
     var box = await Hive.openBox('myBox');
     ```

   - **2. Adding Data:**
     - **Example: Storing Data**
       ```dart
       await box.put('key', 'value');
       ```

   - **3. Retrieving Data:**
     - **Example: Reading Data**
       ```dart
       var value = await box.get('key');
       ```

   - **4. Updating Data:**
     - **Example: Updating a Value**
       ```dart
       await box.put('key', 'newValue');
       ```

   - **5. Deleting Data:**
     - **Example: Removing a Value**
       ```dart
       await box.delete('key');
       ```

   - **6. Closing a Box:**
     - **Example: Closing the Box**
       ```dart
       await box.close();
       ```

---

### **3. Implementing Basic CRUD Operations with Hive**

**a. Create Operation:**
   - **Example: Storing User Information**
     ```dart
     Future<void> saveUserInfo(String name, int age) async {
       var box = await Hive.openBox('userBox');
       await box.put('name', name);
       await box.put('age', age);
     }
     ```

**b. Read Operation:**
   - **Example: Fetching User Information**
     ```dart
     Future<Map<String, dynamic>> getUserInfo() async {
       var box = await Hive.openBox('userBox');
       var name = await box.get('name');
       var age = await box.get('age');
       return {'name': name, 'age': age};
     }
     ```

**c. Update Operation:**
   - **Example: Updating User Information**
     ```dart
     Future<void> updateUserInfo(String name, int age) async {
       var box = await Hive.openBox('userBox');
       await box.put('name', name);
       await box.put('age', age);
     }
     ```

**d. Delete Operation:**
   - **Example: Deleting User Information**
     ```dart
     Future<void> deleteUserInfo() async {
       var box = await Hive.openBox('userBox');
       await box.delete('name');
       await box.delete('age');
     }
     ```

---

### **Example Application: User Profile Manager with Hive**

**Objective:** Build a simple application to manage user profiles using Hive.

**Features:**
1. **Save User Profile:** Input fields to save user name and age.
2. **Read User Profile:** Display saved user name and age.
3. **Update User Profile:** Allow users to update their information.
4. **Delete User Profile:** Provide a way to clear stored profile details.

**Code Example:**

```dart
import 'package:flutter/material.dart';
import 'package:hive_flutter/hive_flutter.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Hive.initFlutter();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ProfileScreen(),
    );
  }
}

class ProfileScreen extends StatefulWidget {
  @override
  _ProfileScreenState createState() => _ProfileScreenState();
}

class _ProfileScreenState extends State<ProfileScreen> {
  final TextEditingController _nameController = TextEditingController();
  final TextEditingController _ageController = TextEditingController();

  String _name = '';
  int _age = 0;

  @override
  void initState() {
    super.initState();
    _loadProfile();
  }

  Future<void> _loadProfile() async {
    var box = await Hive.openBox('userBox');
    setState(() {
      _name = box.get('name', defaultValue: '');
      _age = box.get('age', defaultValue: 0);
      _nameController.text = _name;
      _ageController.text = _age.toString();
    });
  }

  Future<void> _saveProfile() async {
    var box = await Hive.openBox('userBox');
    await box.put('name', _nameController.text);
    await box.put('age', int.parse(_ageController.text));
    _loadProfile();
  }

  Future<void> _deleteProfile() async {
    var box = await Hive.openBox('userBox');
    await box.delete('name');
    await box.delete('age');
    _loadProfile();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('User Profile'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _nameController,
              decoration: InputDecoration(labelText: 'Name'),
            ),
            TextField(
              controller: _ageController,
              keyboardType: TextInputType.number,
              decoration: InputDecoration(labelText: 'Age'),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _saveProfile,
              child: Text('Save Profile'),
            ),
            ElevatedButton(
              onPressed: _deleteProfile,
              child: Text('Delete Profile'),
            ),
            SizedBox(height: 20),
            Text('Name: $_name'),
            Text('Age: $_age'),
          ],
        ),
      ),
    );
  }
}
```

---

### **Assignments**

#### **Assignment 1: Hive User Profile App**
- **Objective:** Build an app to save, read, update, and delete user profiles using Hive.
- **Tasks:**
  1. Implement a form to input and save user data.
  2. Display the saved data in the UI.
  3. Provide options to update and delete the saved data.

#### **Assignment 2: Local Storage for App Settings**
- **Objective:** Create an app that stores and retrieves user settings (e.g., theme preferences, notification settings) using Hive.
- **Tasks:**
  1. Use Hive to save and retrieve user settings.
  2. Implement toggles or dropdowns for different settings.
  3. Ensure the app maintains user settings across sessions.

#### **Assignment 3: To-Do List with Hive**
- **Objective:** Develop a to-do list application that uses Hive for data storage.
- **Tasks:**
  1. Implement CRUD operations for to-do items using Hive.
  2. Allow users to add, view, update, and delete tasks.
  3. Display the list of tasks and their status.

#### **Assignment 4: Notes Application**
- **Objective:** Build a notes application that stores and manages notes using Hive.
- **Tasks:**
  1. Implement functionality to create, edit, and delete notes.
  2. Display a list of notes with their content.
  3. Ensure that notes are saved and retrieved from Hive.

---

### **Quick MCQ Quizzes**

1. **What is Hive primarily used for in Flutter?**
   - a) Managing network connections
   - b) Storing simple key-value pairs
   - c) Handling HTTP requests
   - d) Managing database connections

2. **How do you initialize Hive in a Flutter application?**
   - a) `Hive.init()`
   - b) `Hive.start()`
   - c) `Hive.initFlutter()`
   - d) `Hive.open()`

3. **Which method is used to open a Hive box?**
   - a) `Hive.openBox()`
   - b) `Hive.createBox()`
   - c) `Hive.getBox()`
   - d) `Hive.loadBox()`

4. **How do you store a value in a

 Hive box?**
   - a) `box.add(key, value)`
   - b) `box.put(key, value)`
   - c) `box.store(key, value)`
   - d) `box.save(key, value)`

5. **Which method is used to retrieve a value from a Hive box?**
   - a) `box.fetch(key)`
   - b) `box.getValue(key)`
   - c) `box.retrieve(key)`
   - d) `box.get(key)`

6. **How do you delete a value from a Hive box?**
   - a) `box.remove(key)`
   - b) `box.delete(key)`
   - c) `box.clear(key)`
   - d) `box.removeValue(key)`

7. **Which method is used to close a Hive box?**
   - a) `box.shutdown()`
   - b) `box.close()`
   - c) `box.end()`
   - d) `box.terminate()`

---

### **Conclusion**

This session provides a comprehensive understanding of local data storage using the Hive database. By implementing CRUD operations and integrating Hive into applications, students gain practical experience in managing local data effectively in Flutter. The assignments and quizzes reinforce learning and practical skills.

