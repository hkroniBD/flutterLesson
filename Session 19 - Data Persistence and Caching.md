### **Session 19: Data Persistence and Caching**

#### **Objective:**
This session focuses on data persistence and caching strategies in Flutter. Students will learn how to implement offline support, manage data synchronization between local and remote sources, and use caching to improve app performance.

---

### **1. Introduction to Data Caching Strategies**

**a. What is Data Caching?**
   - Caching is the process of storing data in a temporary storage (cache) to reduce access time and improve performance. It is especially useful for frequently accessed data.

**b. Benefits of Data Caching:**
   - **Improves Performance:** Reduces the need for repeated data fetching.
   - **Decreases Latency:** Speeds up data access by storing it closer to the application.
   - **Reduces Network Load:** Minimizes the number of network requests.

**c. Common Caching Strategies:**
   - **Memory Caching:** Stores data in RAM for fast access.
   - **File-Based Caching:** Saves data in files on disk for persistence.
   - **Database Caching:** Uses a local database to store and retrieve cached data.

---

### **2. Implementing Offline Support in Flutter Apps**

**a. Why Offline Support?**
   - Offline support ensures that users can interact with the app and access data even without an internet connection. It is crucial for improving user experience and app reliability.

**b. Techniques for Implementing Offline Support:**
   - **Local Storage:** Use local databases (e.g., SQLite, Hive) to store data when offline.
   - **Persistent Caching:** Cache API responses and other data locally.
   - **Network Status Monitoring:** Detect changes in network connectivity to manage offline and online modes.

**c. Example Implementation:**
   - **1. Use `connectivity_plus` package:**
     ```yaml
     dependencies:
       connectivity_plus: ^2.0.2
     ```
     ```dart
     import 'package:connectivity_plus/connectivity_plus.dart';

     Future<void> checkConnectivity() async {
       var connectivityResult = await Connectivity().checkConnectivity();
       if (connectivityResult == ConnectivityResult.mobile) {
         // Connected to mobile network
       } else if (connectivityResult == ConnectivityResult.wifi) {
         // Connected to WiFi
       } else {
         // No connection
       }
     }
     ```

   - **2. Implementing Local Storage (using Hive):**
     ```dart
     import 'package:hive/hive.dart';

     Future<void> saveData(String key, String value) async {
       var box = await Hive.openBox('myBox');
       await box.put(key, value);
     }

     Future<String?> loadData(String key) async {
       var box = await Hive.openBox('myBox');
       return box.get(key);
     }
     ```

---

### **3. Syncing Local and Remote Data**

**a. Why Sync Local and Remote Data?**
   - Synchronization ensures that the data stored locally is up-to-date with the remote server. It helps in maintaining data consistency across different devices and platforms.

**b. Techniques for Data Synchronization:**
   - **Manual Sync:** Trigger data synchronization manually when needed.
   - **Automatic Sync:** Set up periodic synchronization tasks or use event-driven syncing.

**c. Example Implementation:**
   - **1. Fetch Remote Data and Store Locally:**
     ```dart
     import 'package:http/http.dart' as http;
     import 'dart:convert';

     Future<void> fetchDataAndSave() async {
       final response = await http.get(Uri.parse('https://api.example.com/data'));
       if (response.statusCode == 200) {
         var data = json.decode(response.body);
         await saveData('remoteData', json.encode(data));
       } else {
         throw Exception('Failed to load data');
       }
     }
     ```

   - **2. Sync Local Changes with Remote Server:**
     ```dart
     Future<void> syncLocalChanges() async {
       var localData = await loadData('localChanges');
       if (localData != null) {
         final response = await http.post(
           Uri.parse('https://api.example.com/sync'),
           headers: {'Content-Type': 'application/json'},
           body: localData,
         );
         if (response.statusCode == 200) {
           // Clear local changes after successful sync
           var box = await Hive.openBox('myBox');
           await box.delete('localChanges');
         } else {
           throw Exception('Failed to sync data');
         }
       }
     }
     ```

---

### **4. Example Application: Offline-Enabled To-Do List**

**Objective:** Build a to-do list application with offline support and data synchronization.

**Features:**
1. **Add and View Tasks:** Users can add and view tasks even when offline.
2. **Sync Tasks:** Sync tasks with a remote server when online.
3. **Display Offline Status:** Indicate whether the app is online or offline.

**Code Example:**

```dart
import 'package:flutter/material.dart';
import 'package:connectivity_plus/connectivity_plus.dart';
import 'package:hive/hive.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TodoListScreen(),
    );
  }
}

class TodoListScreen extends StatefulWidget {
  @override
  _TodoListScreenState createState() => _TodoListScreenState();
}

class _TodoListScreenState extends State<TodoListScreen> {
  final TextEditingController _taskController = TextEditingController();
  final Box _box = Hive.box('tasks');
  bool _isOnline = true;

  @override
  void initState() {
    super.initState();
    _checkConnectivity();
    _syncLocalTasks();
  }

  Future<void> _checkConnectivity() async {
    var connectivityResult = await Connectivity().checkConnectivity();
    setState(() {
      _isOnline = connectivityResult != ConnectivityResult.none;
    });
  }

  Future<void> _syncLocalTasks() async {
    if (_isOnline) {
      var localTasks = _box.get('tasks') ?? [];
      final response = await http.post(
        Uri.parse('https://api.example.com/sync'),
        headers: {'Content-Type': 'application/json'},
        body: json.encode(localTasks),
      );
      if (response.statusCode == 200) {
        // Clear local tasks after successful sync
        _box.delete('tasks');
      } else {
        throw Exception('Failed to sync tasks');
      }
    }
  }

  Future<void> _addTask() async {
    var task = _taskController.text;
    if (task.isNotEmpty) {
      if (_isOnline) {
        await http.post(
          Uri.parse('https://api.example.com/tasks'),
          headers: {'Content-Type': 'application/json'},
          body: json.encode({'task': task}),
        );
      } else {
        var tasks = _box.get('tasks') ?? [];
        tasks.add(task);
        await _box.put('tasks', tasks);
      }
      _taskController.clear();
      setState(() {});
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('To-Do List'),
        actions: [
          IconButton(
            icon: Icon(_isOnline ? Icons.wifi : Icons.wifi_off),
            onPressed: _checkConnectivity,
          ),
        ],
      ),
      body: Column(
        children: [
          Padding(
            padding: const EdgeInsets.all(16.0),
            child: TextField(
              controller: _taskController,
              decoration: InputDecoration(labelText: 'New Task'),
            ),
          ),
          ElevatedButton(
            onPressed: _addTask,
            child: Text('Add Task'),
          ),
          Expanded(
            child: FutureBuilder<List<dynamic>>(
              future: _isOnline
                  ? http.get(Uri.parse('https://api.example.com/tasks')).then(
                      (response) => json.decode(response.body) as List<dynamic>)
                  : Future.value(_box.get('tasks') ?? []),
              builder: (context, snapshot) {
                if (snapshot.connectionState == ConnectionState.waiting) {
                  return Center(child: CircularProgressIndicator());
                } else if (snapshot.hasError) {
                  return Center(child: Text('Error: ${snapshot.error}'));
                } else if (!snapshot.hasData || snapshot.data!.isEmpty) {
                  return Center(child: Text('No tasks found.'));
                } else {
                  return ListView.builder(
                    itemCount: snapshot.data!.length,
                    itemBuilder: (context, index) {
                      final task = snapshot.data![index];
                      return ListTile(
                        title: Text(task),
                      );
                    },
                  );
                }
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

#### **Assignment 1: Offline-Enabled Notes App**
- **Objective:** Create a notes application with offline support.
- **Tasks:**
  1. Implement functionality to add, view, and delete notes offline.
  2. Sync notes with a remote server when online.

#### **Assignment 2: Caching Weather Data**
- **Objective:** Build a weather app that caches weather data.
- **Tasks:**
  1. Fetch and cache weather data from an API.
  2. Display cached data when offline.

#### **Assignment 3: Syncing Task Manager**
- **Objective:** Develop a task manager app with local and remote synchronization.
- **Tasks:**
  1. Implement CRUD operations for tasks.
  2. Sync

 local tasks with a remote server.

---

### **Quiz**

1. **What is the primary purpose of data caching?**
   - a) To increase data security
   - b) To reduce data access time
   - c) To synchronize data
   - d) To encrypt data

2. **Which package can be used for connectivity status in Flutter?**
   - a) `connectivity_plus`
   - b) `http`
   - c) `sqflite`
   - d) `path_provider`

3. **How can you detect network connectivity in Flutter?**
   - a) `Connectivity().checkConnectivity()`
   - b) `Network().getStatus()`
   - c) `Connection().status()`
   - d) `Internet().detect()`

4. **What method is used to synchronize local data with a remote server?**
   - a) `syncLocalData()`
   - b) `syncData()`
   - c) `uploadData()`
   - d) `sendData()`

5. **Which caching strategy stores data in RAM for fast access?**
   - a) File-Based Caching
   - b) Memory Caching
   - c) Database Caching
   - d) Disk Caching

---

### **Conclusion**

Session 19 explores critical aspects of data persistence and caching in Flutter. By implementing offline support, managing data synchronization, and utilizing caching strategies, students will enhance their application's reliability and performance. The assignments and quizzes are designed to reinforce practical skills and assess understanding.
