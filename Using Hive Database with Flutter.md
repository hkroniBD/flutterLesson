## Lecture: Hive Database Basics with Flutter

### Introduction to Hive

Hive is a lightweight and blazing fast key-value database written in pure Dart. It is perfect for Flutter and Dart web applications due to its simplicity, efficiency, and performance.

### Official Documentation

For more detailed information, you can refer to the official Hive documentation:

- [Hive Documentation](https://docs.hivedb.dev/)
- [Hive GitHub Repository](https://github.com/hivedb/hive)
- [Hive Flutter Package](https://pub.dev/packages/hive_flutter)

### Features of Hive 🌟
- **No native dependencies**: Pure Dart implementation.
- **Strongly encrypted**: AES-256 encryption for security.
- **Fast**: High performance for both read and write operations.
- **Lightweight**: Minimal footprint and efficient memory usage.

(
- 🌍 **Bee everywhere**: mobile, desktop, browser
- 🚀 **Buzzing speed**: Faster than a bee on caffeine!
- 💡 Sweet, powerful, & intuitive API
- 🔐 **Queen's Guard**: Encryption built right in.
- 🧠 **Thinking in swarms**: Multi-isolate support.
- 🍯 Everything a bee needs and more!
Bee fact: A single bee can visit 5,000 flowers in a day!

)

### Setting Up Hive in Flutter

#### 1. Add Dependencies

Add the Hive and Hive Flutter packages to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  hive: ^2.0.0
  hive_flutter: ^1.1.0
```

#### 2. Install Dependencies

Run the following command to install the new dependencies:

```sh
flutter pub get
```

#### 3. Initialize Hive

Initialize Hive in your `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:hive_flutter/hive_flutter.dart';

void main() async {
  await Hive.initFlutter();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Hive Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}
```

### Hive Basics

Hive stores data in boxes. A box can be thought of as a table in a SQL database or a collection in a NoSQL database.

#### Opening a Box

To open a box, use the `Hive.openBox` method:

```dart
void main() async {
  await Hive.initFlutter();
  var box = await Hive.openBox('testBox');
  runApp(MyApp());
}
```

#### CRUD Operations with Hive

1. **Adding Data**

   To add data to a Hive box:

   ```dart
   var box = Hive.box('testBox');
   box.put('name', 'John Doe');
   ```

2. **Retrieving Data**

   To retrieve data from a Hive box:

   ```dart
   var name = box.get('name');
   print(name); // Output: John Doe
   ```

3. **Updating Data**

   To update data in a Hive box:

   ```dart
   box.put('name', 'Jane Doe');
   ```

4. **Deleting Data**

   To delete data from a Hive box:

   ```dart
   box.delete('name');
   ```

### Using Custom Objects with Hive

Hive can also store custom objects. To do this, you need to:

1. **Create a Model Class**

   Create a model class and annotate it with `HiveType` and `HiveField`:

   ```dart
   import 'package:hive/hive.dart';

   part 'person.g.dart';

   @HiveType(typeId: 0)
   class Person extends HiveObject {
     @HiveField(0)
     String name;

     @HiveField(1)
     int age;

     Person({required this.name, required this.age});
   }
   ```

2. **Generate Type Adapter**

   Run the following command to generate the type adapter:

   ```sh
   flutter packages pub run build_runner build
   ```

3. **Register the Adapter**

   Register the adapter in your `main.dart` file:

   ```dart
   void main() async {
     await Hive.initFlutter();
     Hive.registerAdapter(PersonAdapter());
     var box = await Hive.openBox<Person>('personBox');
     runApp(MyApp());
   }
   ```

4. **CRUD Operations with Custom Objects**

   ```dart
   var personBox = Hive.box<Person>('personBox');

   // Adding a person
   var person = Person(name: 'John Doe', age: 30);
   personBox.add(person);

   // Retrieving a person
   var retrievedPerson = personBox.getAt(0);
   print(retrievedPerson?.name); // Output: John Doe

   // Updating a person
   retrievedPerson?.name = 'Jane Doe';
   retrievedPerson?.save();

   // Deleting a person
   personBox.deleteAt(0);
   ```

### Example Application

Here is a simple Flutter application demonstrating the use of Hive for storing and retrieving data.

#### main.dart

```dart
import 'package:flutter/material.dart';
import 'package:hive_flutter/hive_flutter.dart';
import 'person.dart';

void main() async {
  await Hive.initFlutter();
  Hive.registerAdapter(PersonAdapter());
  await Hive.openBox<Person>('personBox');
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Hive Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final _nameController = TextEditingController();
  final _ageController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    var personBox = Hive.box<Person>('personBox');

    return Scaffold(
      appBar: AppBar(
        title: Text('Flutter Hive Example'),
      ),
      body: Column(
        children: [
          Padding(
            padding: EdgeInsets.all(8.0),
            child: TextField(
              controller: _nameController,
              decoration: InputDecoration(labelText: 'Name'),
            ),
          ),
          Padding(
            padding: EdgeInsets.all(8.0),
            child: TextField(
              controller: _ageController,
              decoration: InputDecoration(labelText: 'Age'),
              keyboardType: TextInputType.number,
            ),
          ),
          ElevatedButton(
            onPressed: () {
              final name = _nameController.text;
              final age = int.tryParse(_ageController.text);
              if (name.isNotEmpty && age != null) {
                final person = Person(name: name, age: age);
                personBox.add(person);
              }
            },
            child: Text('Add Person'),
          ),
          Expanded(
            child: ValueListenableBuilder(
              valueListenable: personBox.listenable(),
              builder: (context, Box<Person> box, _) {
                if (box.values.isEmpty) {
                  return Center(
                    child: Text('No data available.'),
                  );
                }

                return ListView.builder(
                  itemCount: box.length,
                  itemBuilder: (context, index) {
                    final person = box.getAt(index);
                    return ListTile(
                      title: Text(person?.name ?? ''),
                      subtitle: Text('Age: ${person?.age ?? 0}'),
                      trailing: IconButton(
                        icon: Icon(Icons.delete),
                        onPressed: () {
                          box.deleteAt(index);
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

#### person.dart

```dart
import 'package:hive/hive.dart';

part 'person.g.dart';

@HiveType(typeId: 0)
class Person extends HiveObject {
  @HiveField(0)
  String name;

  @HiveField(1)
  int age;

  Person({required this.name, required this.age});
}
```

### Summary

- **Hive Basics**: Hive is a lightweight key-value database.
- **CRUD Operations**: Adding, retrieving, updating, and deleting data.
- **Custom Objects**: Storing and managing custom objects in Hive.
- **Example Application**: Demonstrated the usage of Hive in a simple Flutter application.

### Homework

1. Create a `Task` model class with fields `title` and `isCompleted`. Implement CRUD operations for managing tasks using Hive.
2. Extend the example application to include a feature for editing existing person entries.
3. Add encryption to the Hive box to secure the stored data.
