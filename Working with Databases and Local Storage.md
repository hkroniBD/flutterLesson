## Session 7: Working with Databases and Local Storage

### Duration
- **Total Time**: 3 hours

### Objectives
By the end of this session, students should be able to:
1. Understand and implement local storage solutions in Flutter.
2. Use SQLite for local database management.
3. Utilize Hive for NoSQL local storage.
4. Utilize shared preferences for simple key-value storage.

### Materials Needed
- Laptops with Flutter SDK installed
- Code editor (Visual Studio Code, Android Studio, or IntelliJ IDEA)
- Projector or screen for demonstrations
- Access to sample databases and code examples

### Detailed Material

### **1. Introduction to Local Storage in Flutter (60 minutes)**

#### **1.1 Overview of Local Storage**
- **Definition**: Local storage refers to saving data on the device, either in files or databases, to persist data between app sessions.
- **Types of Local Storage**:
  - **Shared Preferences**: For storing simple key-value pairs.
  - **SQLite**: For structured data with complex queries.
  - **Hive**: For NoSQL storage with fast and lightweight capabilities.

- **Reference**:
  - [Local Storage Overview](https://flutter.dev/docs/development/data-and-backend/local-data)

#### **1.2 Using Shared Preferences**
- **Adding Dependency**:
  - **Setup**:
    ```yaml
    dependencies:
      shared_preferences: ^2.0.15
    ```

- **Basic Operations**:
  - **Saving Data**:
    ```dart
    import 'package:shared_preferences/shared_preferences.dart';

    Future<void> saveData() async {
      final prefs = await SharedPreferences.getInstance();
      await prefs.setString('key', 'value');
    }
    ```

  - **Retrieving Data**:
    ```dart
    Future<String?> getData() async {
      final prefs = await SharedPreferences.getInstance();
      return prefs.getString('key');
    }
    ```

  - **Deleting Data**:
    ```dart
    Future<void> deleteData() async {
      final prefs = await SharedPreferences.getInstance();
      await prefs.remove('key');
    }
    ```

- **Reference**:
  - [Shared Preferences Documentation](https://pub.dev/packages/shared_preferences)

### **2. Working with SQLite (60 minutes)**

#### **2.1 Introduction to SQLite**
- **Definition**: SQLite is a lightweight, disk-based database that doesn’t require a separate server process and allows access to the database using a nonstandard variant of the SQL query language.
- **Use Cases**: Suitable for structured data and complex queries.

- **Reference**:
  - [SQLite Overview](https://flutter.dev/docs/cookbook/persistence/sqlite)

#### **2.2 Using the sqflite Package**
- **Adding Dependency**:
  - **Setup**:
    ```yaml
    dependencies:
      sqflite: ^2.0.0+4
      path: ^1.8.0
    ```

- **Database Setup and Schema Definition**:
  - **Creating Database**:
    ```dart
    import 'package:sqflite/sqflite.dart';
    import 'package:path/path.dart';

    Future<Database> database() async {
      return openDatabase(
        join(await getDatabasesPath(), 'example.db'),
        onCreate: (db, version) {
          return db.execute(
            "CREATE TABLE items(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT)",
          );
        },
        version: 1,
      );
    }
    ```

- **CRUD Operations**:
  - **Insert Data**:
    ```dart
    Future<void> insertItem(Map<String, dynamic> item) async {
      final db = await database();
      await db.insert(
        'items',
        item,
        conflictAlgorithm: ConflictAlgorithm.replace,
      );
    }
    ```

  - **Query Data**:
    ```dart
    Future<List<Map<String, dynamic>>> getItems() async {
      final db = await database();
      return await db.query('items');
    }
    ```

  - **Update Data**:
    ```dart
    Future<void> updateItem(Map<String, dynamic> item) async {
      final db = await database();
      await db.update(
        'items',
        item,
        where: "id = ?",
        whereArgs: [item['id']],
      );
    }
    ```

  - **Delete Data**:
    ```dart
    Future<void> deleteItem(int id) async {
      final db = await database();
      await db.delete(
        'items',
        where: "id = ?",
        whereArgs: [id],
      );
    }
    ```

- **Reference**:
  - [sqflite Package Documentation](https://pub.dev/packages/sqflite)

#### **2.3 Handling Database Migration**
- **Migration Example**:
  - **Updating Database Schema**:
    ```dart
    Future<Database> database() async {
      return openDatabase(
        join(await getDatabasesPath(), 'example.db'),
        onCreate: (db, version) {
          return db.execute(
            "CREATE TABLE items(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT)",
          );
        },
        onUpgrade: (db, oldVersion, newVersion) {
          if (oldVersion < 2) {
            db.execute("ALTER TABLE items ADD COLUMN description TEXT");
          }
        },
        version: 2,
      );
    }
    ```

- **Reference**:
  - [Database Migration Guide](https://flutter.dev/docs/cookbook/persistence/sqlite#database-migrations)

### **3. Introduction to Hive (60 minutes)**

#### **3.1 Overview of Hive**
- **Definition**: Hive is a lightweight and fast key-value database for Flutter applications. It supports a NoSQL database model and is known for its high performance and ease of use.
- **Use Cases**: Suitable for storing small to medium-sized datasets locally with low overhead.

- **Reference**:
  - [Hive Overview](https://docs.hivedb.dev/#/)

#### **3.2 Using the Hive Package**
- **Adding Dependency**:
  - **Setup**:
    ```yaml
    dependencies:
      hive: ^2.2.1
      hive_flutter: ^1.1.0
    ```

  - **Dev Dependencies**:
    ```yaml
    dev_dependencies:
      hive_generator: ^1.1.0
      build_runner: ^2.1.1
    ```

- **Setup Hive Database**:
  - **Initialization**:
    ```dart
    import 'package:hive/hive.dart';
    import 'package:hive_flutter/hive_flutter.dart';

    void main() async {
      await Hive.initFlutter();
      runApp(MyApp());
    }
    ```

- **Creating and Using a Box**:
  - **Open a Box**:
    ```dart
    var box = await Hive.openBox('myBox');
    ```

  - **Add Data**:
    ```dart
    box.put('key', 'value');
    ```

  - **Retrieve Data**:
    ```dart
    var value = box.get('key');
    ```

  - **Delete Data**:
    ```dart
    box.delete('key');
    ```

- **Reference**:
  - [Hive Documentation](https://docs.hivedb.dev/#/)

#### **3.3 Working with Custom Objects**
- **Storing Custom Objects**:
  - **Define Adapter**:
    ```dart
    import 'package:hive/hive.dart';

    part 'model.g.dart';

    @HiveType(typeId: 0)
    class MyModel extends HiveObject {
      @HiveField(0)
      final String name;

      MyModel(this.name);
    }
    ```

  - **Register Adapter**:
    ```dart
    void main() async {
      Hive.registerAdapter(MyModelAdapter());
      await Hive.openBox<MyModel>('myModelBox');
      runApp(MyApp());
    }
    ```

  - **Add and Retrieve Custom Objects**:
    ```dart
    var box = await Hive.openBox<MyModel>('myModelBox');
    box.add(MyModel('Test'));
    var items = box.values.toList();
    ```

- **Reference**:
  - [Hive Custom Objects](https://docs.hivedb.dev/#/custom-objects)

### **4. Hands-On Exercise and Practice (30 minutes)**

#### **4.1 Build a Local Storage App**
- **Objective**: Develop an app that uses Shared Preferences, SQLite, and Hive to store and manage data locally.
- **Exercise**:
  - Implement an app that uses SQLite for structured data, Hive for NoSQL data, and Shared Preferences for user settings.
  - Create a form to input and store data, and display it using different storage options.

- **Reference**:
  - [Local Storage and Database Examples](https://flutter.dev/docs/cookbook)

### **5. Q&A and Wrap-Up (30 minutes)**

#### **5.1 Addressing Questions**
- Open floor for students to ask questions related to local storage, databases, and Hive.

#### **5.2 Recap of the Day**
- Summary of key points covered in the session.

#### **5.3 Homework Assignment**
- **Build a Comprehensive Data Management App**:
  - Create an app that integrates Shared Preferences, SQLite, and Hive. Implement features to store and manage user data, settings, and application state effectively.

- **Reference**:
  - [Advanced Local Storage Examples](https://flutter.dev/docs/cookbook)
