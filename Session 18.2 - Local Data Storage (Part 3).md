### **Session 18.2: Local Data Storage - Part 3**

#### **Objective:**
This session covers using SQLite for structured data storage in Flutter applications. Students will learn how to set up and manage SQLite databases, and interact with them using the `sqflite` package.

---

### **1. Introduction to SQLite**

**a. What is SQLite?**
   - SQLite is a lightweight, self-contained SQL database engine. It is used for managing structured data and is integrated directly into applications.

**b. Why Use SQLite?**
   - Supports complex queries and transactions.
   - Efficient storage and retrieval of structured data.
   - Suitable for applications that require relational database features.

**c. When to Use SQLite:**
   - Ideal for applications with complex data models, requiring relational data storage, or needing offline support.

---

### **2. Setting Up SQLite in a Flutter Project**

**a. Adding Dependencies:**
   - Add `sqflite` and `path` dependencies to your `pubspec.yaml` file:
     ```yaml
     dependencies:
       flutter:
         sdk: flutter
       sqflite: ^2.0.0+4
       path: ^1.8.2
     ```

**b. Installing Packages:**
   - Run `flutter pub get` to install the dependencies.

---

### **3. Creating and Managing Databases**

**a. Setting Up the Database:**
   - **1. Import Packages:**
     ```dart
     import 'package:sqflite/sqflite.dart';
     import 'package:path/path.dart';
     ```

   - **2. Database Helper Class:**
     - Create a helper class to manage the SQLite database.
     ```dart
     class DatabaseHelper {
       static final DatabaseHelper _instance = DatabaseHelper._internal();
       factory DatabaseHelper() => _instance;
       DatabaseHelper._internal();

       static Database? _database;

       Future<Database> get database async {
         if (_database != null) return _database!;
         _database = await _initDatabase();
         return _database!;
       }

       Future<Database> _initDatabase() async {
         String path = join(await getDatabasesPath(), 'my_database.db');
         return await openDatabase(path, version: 1, onCreate: _onCreate);
       }

       Future<void> _onCreate(Database db, int version) async {
         await db.execute(
           'CREATE TABLE users(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, age INTEGER)',
         );
       }
     }
     ```

**b. Performing CRUD Operations:**
   - **1. Create Operation:**
     ```dart
     Future<void> insertUser(String name, int age) async {
       final Database db = await DatabaseHelper().database;
       await db.insert(
         'users',
         {'name': name, 'age': age},
         conflictAlgorithm: ConflictAlgorithm.replace,
       );
     }
     ```

   - **2. Read Operation:**
     ```dart
     Future<List<Map<String, dynamic>>> getUsers() async {
       final Database db = await DatabaseHelper().database;
       return await db.query('users');
     }
     ```

   - **3. Update Operation:**
     ```dart
     Future<void> updateUser(int id, String name, int age) async {
       final Database db = await DatabaseHelper().database;
       await db.update(
         'users',
         {'name': name, 'age': age},
         where: 'id = ?',
         whereArgs: [id],
       );
     }
     ```

   - **4. Delete Operation:**
     ```dart
     Future<void> deleteUser(int id) async {
       final Database db = await DatabaseHelper().database;
       await db.delete(
         'users',
         where: 'id = ?',
         whereArgs: [id],
       );
     }
     ```

---

### **4. Example Application: User Management with SQLite**

**Objective:** Build a simple application to manage user data using SQLite.

**Features:**
1. **Add User:** Input fields to add new users.
2. **Display Users:** Show a list of users stored in the database.
3. **Update User:** Allow users to update their details.
4. **Delete User:** Provide a way to delete user records.

**Code Example:**

```dart
import 'package:flutter/material.dart';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: UserManagementScreen(),
    );
  }
}

class UserManagementScreen extends StatefulWidget {
  @override
  _UserManagementScreenState createState() => _UserManagementScreenState();
}

class _UserManagementScreenState extends State<UserManagementScreen> {
  final TextEditingController _nameController = TextEditingController();
  final TextEditingController _ageController = TextEditingController();

  Future<void> _insertUser() async {
    final name = _nameController.text;
    final age = int.tryParse(_ageController.text) ?? 0;
    await DatabaseHelper().insertUser(name, age);
    _nameController.clear();
    _ageController.clear();
    setState(() {});
  }

  Future<List<Map<String, dynamic>>> _getUsers() async {
    return await DatabaseHelper().getUsers();
  }

  Future<void> _deleteUser(int id) async {
    await DatabaseHelper().deleteUser(id);
    setState(() {});
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('User Management'),
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
              onPressed: _insertUser,
              child: Text('Add User'),
            ),
            SizedBox(height: 20),
            FutureBuilder<List<Map<String, dynamic>>>(
              future: _getUsers(),
              builder: (context, snapshot) {
                if (snapshot.connectionState == ConnectionState.waiting) {
                  return Center(child: CircularProgressIndicator());
                } else if (snapshot.hasError) {
                  return Center(child: Text('Error: ${snapshot.error}'));
                } else if (!snapshot.hasData || snapshot.data!.isEmpty) {
                  return Center(child: Text('No users found.'));
                } else {
                  return Expanded(
                    child: ListView.builder(
                      itemCount: snapshot.data!.length,
                      itemBuilder: (context, index) {
                        final user = snapshot.data![index];
                        return ListTile(
                          title: Text('${user['name']} (Age: ${user['age']})'),
                          trailing: IconButton(
                            icon: Icon(Icons.delete),
                            onPressed: () => _deleteUser(user['id']),
                          ),
                        );
                      },
                    ),
                  );
                }
              },
            ),
          ],
        ),
      ),
    );
  }
}

class DatabaseHelper {
  static final DatabaseHelper _instance = DatabaseHelper._internal();
  factory DatabaseHelper() => _instance;
  DatabaseHelper._internal();

  static Database? _database;

  Future<Database> get database async {
    if (_database != null) return _database!;
    _database = await _initDatabase();
    return _database!;
  }

  Future<Database> _initDatabase() async {
    String path = join(await getDatabasesPath(), 'my_database.db');
    return await openDatabase(path, version: 1, onCreate: _onCreate);
  }

  Future<void> _onCreate(Database db, int version) async {
    await db.execute(
      'CREATE TABLE users(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, age INTEGER)',
    );
  }

  Future<void> insertUser(String name, int age) async {
    final Database db = await database;
    await db.insert(
      'users',
      {'name': name, 'age': age},
      conflictAlgorithm: ConflictAlgorithm.replace,
    );
  }

  Future<List<Map<String, dynamic>>> getUsers() async {
    final Database db = await database;
    return await db.query('users');
  }

  Future<void> updateUser(int id, String name, int age) async {
    final Database db = await database;
    await db.update(
      'users',
      {'name': name, 'age': age},
      where: 'id = ?',
      whereArgs: [id],
    );
  }

  Future<void> deleteUser(int id) async {
    final Database db = await database;
    await db.delete(
      'users',
      where: 'id = ?',
      whereArgs: [id],
    );
  }
}
```

---

### **Assignments**

#### **Assignment 1: SQLite User Management App**
- **Objective:** Develop an application to manage user data using SQLite.
- **Tasks:**
  1. Implement functionality to add, view, update, and delete user records.
  2. Display a list of users in the UI.

#### **Assignment 2: Task Manager with SQLite**
- **Objective:** Create a task manager application using SQLite for data storage.
- **Tasks:**
  1. Implement CRUD operations for tasks.
  2. Display tasks with their status and allow updating and deleting tasks.

#### **Assignment 3: Notes Application with SQLite**
- **Objective:** Build a notes application that uses SQLite for storing

 notes.
- **Tasks:**
  1. Add functionality to create, read, update, and delete notes.
  2. Implement a search feature to find notes.

---

### **Quiz**

1. **Which package is used for SQLite in Flutter?**
   - a) `sqflite`
   - b) `hive`
   - c) `moor`
   - d) `path_provider`

2. **How do you create a table in SQLite?**
   - a) `db.createTable('table_name')`
   - b) `db.execute('CREATE TABLE table_name (...)')`
   - c) `db.addTable('table_name', ...)`
   - d) `db.create('table_name', ...)`

3. **Which method is used to open a database in SQLite?**
   - a) `openDatabase()`
   - b) `connectDatabase()`
   - c) `initializeDatabase()`
   - d) `startDatabase()`

4. **To update an existing record in SQLite, which method is used?**
   - a) `db.update()`
   - b) `db.modify()`
   - c) `db.change()`
   - d) `db.alter()`

5. **Which method is used to delete a record from SQLite?**
   - a) `db.remove()`
   - b) `db.delete()`
   - c) `db.drop()`
   - d) `db.erase()`

---

### **Conclusion**

Session 18.2 provides practical knowledge of using SQLite for structured data storage in Flutter. By implementing and managing SQLite databases, students will be able to handle complex data storage needs effectively in their applications. Assignments and quizzes are designed to reinforce these concepts and assess practical skills.
