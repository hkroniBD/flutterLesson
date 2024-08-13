### **Session 17: Local Data Storage - Part 1**

#### **Objective:**
This session introduces local data storage options in Flutter. Students will learn how to use `SharedPreferences` for simple key-value storage and implement basic CRUD (Create, Read, Update, Delete) operations.

---

### **1. Introduction to Local Storage Options in Flutter**

**a. Why Local Storage?**
   - Local storage is used to save data on the device, providing a way to persist user preferences, settings, or small amounts of data without needing a network connection.

**b. Common Local Storage Options:**
   - **SharedPreferences:** Simple key-value storage suitable for storing user preferences and settings.
   - **SQLite:** For more complex data storage needs, including relational data.
   - **File Storage:** For storing files and other data types.

**c. Focus of This Session:**
   - We will focus on `SharedPreferences`, which is suitable for storing small amounts of data like user preferences and app settings.

---

### **2. Using SharedPreferences for Simple Key-Value Storage**

**a. What is SharedPreferences?**
   - `SharedPreferences` is a plugin for Flutter that allows you to store and retrieve simple key-value pairs.

**b. Adding the Dependency:**
   - Include `shared_preferences` in your `pubspec.yaml` file:
     ```yaml
     dependencies:
       flutter:
         sdk: flutter
       shared_preferences: ^2.0.15
     ```

**c. Basic Operations with SharedPreferences:**

   **1. Import the Package:**
   ```dart
   import 'package:shared_preferences/shared_preferences.dart';
   ```

   **2. Writing Data:**
   - **Example: Storing a String Value**
     ```dart
     Future<void> saveStringValue(String key, String value) async {
       final prefs = await SharedPreferences.getInstance();
       await prefs.setString(key, value);
     }
     ```

   **3. Reading Data:**
   - **Example: Retrieving a String Value**
     ```dart
     Future<String?> getStringValue(String key) async {
       final prefs = await SharedPreferences.getInstance();
       return prefs.getString(key);
     }
     ```

   **4. Updating Data:**
   - To update data, simply use the `set` method again with the same key. For instance, updating a value:
     ```dart
     await prefs.setString('username', 'new_username');
     ```

   **5. Deleting Data:**
   - **Example: Removing a Value**
     ```dart
     Future<void> removeValue(String key) async {
       final prefs = await SharedPreferences.getInstance();
       await prefs.remove(key);
     }
     ```

   **6. Clearing All Data:**
     ```dart
     Future<void> clearAll() async {
       final prefs = await SharedPreferences.getInstance();
       await prefs.clear();
     }
     ```

---

### **3. Implementing Basic CRUD Operations**

**a. Create Operation:**
   - **Example: Saving User Preferences**
     ```dart
     Future<void> saveUserPreferences(String name, int age) async {
       final prefs = await SharedPreferences.getInstance();
       await prefs.setString('name', name);
       await prefs.setInt('age', age);
     }
     ```

**b. Read Operation:**
   - **Example: Fetching User Preferences**
     ```dart
     Future<Map<String, dynamic>> getUserPreferences() async {
       final prefs = await SharedPreferences.getInstance();
       final name = prefs.getString('name');
       final age = prefs.getInt('age');
       return {'name': name, 'age': age};
     }
     ```

**c. Update Operation:**
   - **Example: Updating User Preferences**
     ```dart
     Future<void> updateUserPreferences(String name, int age) async {
       final prefs = await SharedPreferences.getInstance();
       await prefs.setString('name', name);
       await prefs.setInt('age', age);
     }
     ```

**d. Delete Operation:**
   - **Example: Deleting Specific Preference**
     ```dart
     Future<void> deleteUserPreferences() async {
       final prefs = await SharedPreferences.getInstance();
       await prefs.remove('name');
       await prefs.remove('age');
     }
     ```

---

### **Example Application: User Preferences Manager**

**Objective:** Build a simple application to manage user preferences using `SharedPreferences`.

**Features:**
1. **Save Preferences:** Input fields to save user name and age.
2. **Read Preferences:** Display saved user name and age.
3. **Update Preferences:** Allow users to update their information.
4. **Delete Preferences:** Provide a way to clear stored preferences.

**Code Example:**

```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: PreferencesScreen(),
    );
  }
}

class PreferencesScreen extends StatefulWidget {
  @override
  _PreferencesScreenState createState() => _PreferencesScreenState();
}

class _PreferencesScreenState extends State<PreferencesScreen> {
  final TextEditingController _nameController = TextEditingController();
  final TextEditingController _ageController = TextEditingController();

  String _name = '';
  int _age = 0;

  @override
  void initState() {
    super.initState();
    _loadPreferences();
  }

  Future<void> _loadPreferences() async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      _name = prefs.getString('name') ?? '';
      _age = prefs.getInt('age') ?? 0;
      _nameController.text = _name;
      _ageController.text = _age.toString();
    });
  }

  Future<void> _savePreferences() async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setString('name', _nameController.text);
    await prefs.setInt('age', int.parse(_ageController.text));
    _loadPreferences();
  }

  Future<void> _deletePreferences() async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.remove('name');
    await prefs.remove('age');
    _loadPreferences();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('User Preferences'),
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
              onPressed: _savePreferences,
              child: Text('Save Preferences'),
            ),
            ElevatedButton(
              onPressed: _deletePreferences,
              child: Text('Delete Preferences'),
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

#### **Assignment 1: User Preferences App**
- **Objective:** Build an app to save, read, update, and delete user preferences using `SharedPreferences`.
- **Tasks:**
  1. Implement a form to input and save user data.
  2. Display the saved data in the UI.
  3. Provide options to update and delete the saved data.

#### **Assignment 2: Settings Manager**
- **Objective:** Create an app that stores user settings (e.g., theme preference, notification settings).
- **Tasks:**
  1. Use `SharedPreferences` to save and retrieve user settings.
  2. Implement toggles or dropdowns for different settings.
  3. Ensure the app remembers user settings across sessions.

#### **Assignment 3: Simple To-Do List**
- **Objective:** Develop a basic to-do list app that uses local storage to save tasks.
- **Tasks:**
  1. Implement CRUD operations for to-do items using `SharedPreferences`.
  2. Allow users to add, view, update, and delete tasks.
  3. Display the list of tasks and their completion status.

#### **Assignment 4: User Profile Storage**
- **Objective:** Create an app that saves and displays user profile information (name, email).
- **Tasks:**
  1. Implement a form to input and save user profile details.
  2. Display the saved profile information on the main screen.
  3. Provide options to update and clear profile details.

---

### **Quick MCQ Quizzes**

1. **What is `SharedPreferences` used for in Flutter?**
   - a) Storing complex data structures
   - b) Saving simple key-value pairs
   - c) Managing network connections
   - d) Performing file operations

2. **Which method is used to retrieve a string value from `SharedPreferences`?**
   - a) `getStringValue()`
   - b) `getValue()`
   - c) `getString()`
   - d) `fetchString()`

3. **How can you remove a specific key-value pair from `SharedPreferences`?**
   - a) `prefs.delete(key)`
   - b) `prefs.remove(key)`
   - c) `prefs.clear(key)`
   - d) `prefs.deleteValue(key)`

4. **What method is used to store an integer value in `SharedPreferences`?**
   -

 a) `setIntValue()`
   - b) `setInteger()`
   - c) `setInt()`
   - d) `saveInt()`

5. **Which method clears all data from `SharedPreferences`?**
   - a) `prefs.removeAll()`
   - b) `prefs.deleteAll()`
   - c) `prefs.clear()`
   - d) `prefs.reset()`

---

### **Conclusion**

This session provides a foundation in local data storage using `SharedPreferences`. By understanding how to perform basic CRUD operations, students can effectively manage simple data needs in their Flutter applications. The assignments and quizzes are designed to reinforce practical implementation and theoretical concepts.

