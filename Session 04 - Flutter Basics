### **Session 4: Flutter Basics**

#### **Objective:**
This session focuses on the fundamental concepts of Flutter, including widgets, the widget tree, and basic widget types. Understanding these concepts is essential for building and designing user interfaces in Flutter.

---

### **1. Understanding Flutter Widgets**

**a. What is a Widget?**

- **Definition:**
  - In Flutter, everything is a widget. A widget is a basic building block of a Flutter app's UI. It represents an element on the screen, such as a button, text, or image.
  - Widgets are immutable and are used to describe what the UI should look like. They can be combined to create complex UIs.

- **References:**
  - [Flutter Widgets](https://flutter.dev/docs/development/ui/widgets-intro)

**b. Widget Lifecycle:**

- **Creation:** Widgets are created using the `build()` method.
- **Configuration:** Widgets are configured by the properties they are given.
- **Rendering:** Widgets are rendered to the screen based on their configuration.

---

### **2. StatelessWidget vs. StatefulWidget**

**a. StatelessWidget:**

- **Definition:**
  - `StatelessWidget` is used for widgets that do not require mutable state. Once created, they cannot change their properties.
  - **Usage:**
    - Ideal for static elements that do not change over time.

- **Syntax:**
  ```dart
  class MyStaticWidget extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Container(
        child: Text('This is a static widget'),
      );
    }
  }
  ```

- **References:**
  - [StatelessWidget Documentation](https://flutter.dev/docs/development/ui/widgets-intro#stateless-widgets)

**b. StatefulWidget:**

- **Definition:**
  - `StatefulWidget` is used for widgets that can change state during their lifecycle. It requires a separate `State` object that contains mutable state.

- **Syntax:**
  ```dart
  class MyDynamicWidget extends StatefulWidget {
    @override
    _MyDynamicWidgetState createState() => _MyDynamicWidgetState();
  }

  class _MyDynamicWidgetState extends State<MyDynamicWidget> {
    int _counter = 0;

    void _incrementCounter() {
      setState(() {
        _counter++;
      });
    }

    @override
    Widget build(BuildContext context) {
      return Column(
        children: [
          Text('Counter: $_counter'),
          ElevatedButton(
            onPressed: _incrementCounter,
            child: Text('Increment'),
          ),
        ],
      );
    }
  }
  ```

- **References:**
  - [StatefulWidget Documentation](https://flutter.dev/docs/development/ui/widgets-intro#stateful-widgets)

---

### **3. The Widget Tree and the Build Method**

**a. Widget Tree:**

- **Definition:**
  - The widget tree represents the hierarchy of widgets in a Flutter application. Each widget can have child widgets, forming a tree structure.
  - **Example:**
    ```dart
    MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('My App')),
        body: Center(child: Text('Hello, World!')),
      ),
    );
    ```

- **References:**
  - [Flutter Widget Tree](https://flutter.dev/docs/development/ui/widgets-intro#widget-tree)

**b. Build Method:**

- **Definition:**
  - The `build()` method is responsible for describing the part of the user interface represented by a widget. It is called whenever the widget's state changes.

- **Usage:**
  - The `build()` method returns a widget tree that represents the UI of the widget.

- **References:**
  - [Flutter Build Method](https://flutter.dev/docs/development/ui/widgets-intro#the-build-method)

---

### **4. Introduction to Basic Widgets**

**a. Container:**

- **Definition:**
  - `Container` is a versatile widget used for layout and decoration. It can contain other widgets and apply padding, margins, borders, and more.

- **Syntax:**
  ```dart
  Container(
    padding: EdgeInsets.all(16.0),
    margin: EdgeInsets.all(16.0),
    decoration: BoxDecoration(
      color: Colors.blue,
      borderRadius: BorderRadius.circular(8.0),
    ),
    child: Text('This is a container'),
  )
  ```

- **References:**
  - [Container Widget Documentation](https://flutter.dev/docs/development/ui/widgets/layout#container)

**b. Text:**

- **Definition:**
  - `Text` is used to display a string of text. It is highly customizable, with options for styling and alignment.

- **Syntax:**
  ```dart
  Text(
    'Hello, Flutter!',
    style: TextStyle(fontSize: 24, color: Colors.black),
  )
  ```

- **References:**
  - [Text Widget Documentation](https://flutter.dev/docs/development/ui/widgets/text)

**c. Row and Column:**

- **Definition:**
  - `Row` and `Column` are layout widgets used to arrange their children horizontally (`Row`) or vertically (`Column`).

- **Syntax:**
  ```dart
  Row(
    children: [
      Text('First'),
      Text('Second'),
    ],
  )

  Column(
    children: [
      Text('Top'),
      Text('Bottom'),
    ],
  )
  ```

- **References:**
  - [Row Widget Documentation](https://flutter.dev/docs/development/ui/widgets/layout#row)
  - [Column Widget Documentation](https://flutter.dev/docs/development/ui/widgets/layout#column)

**d. Image:**

- **Definition:**
  - `Image` is used to display images in the app, either from assets or network sources.

- **Syntax:**
  ```dart
  Image.asset('assets/image.png') // For local assets

  Image.network('https://example.com/image.png') // For network images
  ```

- **References:**
  - [Image Widget Documentation](https://flutter.dev/docs/development/ui/widgets/image)

---

### **Assignments**

#### **Assignment 1: Basic Widgets**

- **Objective:** Practice using basic Flutter widgets to build a simple UI.
- **Tasks:**
  1. Create a Flutter app with a `Container` that includes `Text` widgets, using padding and decoration.
  2. Use `Row` and `Column` to layout multiple `Text` widgets in a structured format.
  3. Add an `Image` widget to the app that displays an image from local assets or a network URL.

#### **Assignment 2: Stateless and Stateful Widgets**

- **Objective:** Implement both `StatelessWidget` and `StatefulWidget` to understand their differences.
- **Tasks:**
  1. Create a `StatelessWidget` that displays a static `Text` widget.
  2. Create a `StatefulWidget` with a button that updates a counter when pressed.

---

### **Quiz**

1. **What is the primary difference between `StatelessWidget` and `StatefulWidget`?**
   - a) `StatelessWidget` can change state; `StatefulWidget` cannot
   - b) `StatefulWidget` can change state; `StatelessWidget` cannot
   - c) `StatelessWidget` is used for layout; `StatefulWidget` is used for decoration
   - d) `StatelessWidget` and `StatefulWidget` are identical

2. **Which method is called to describe the part of the user interface represented by a widget?**
   - a) `create()`
   - b) `build()`
   - c) `render()`
   - d) `update()`

3. **What is the purpose of the `Container` widget in Flutter?**
   - a) To display text
   - b) To manage layout constraints
   - c) To provide decoration and padding
   - d) To handle navigation

4. **How do you display a network image in Flutter?**
   - a) `Image.asset()`
   - b) `Image.network()`
   - c) `Image.file()`
   - d) `Image.memory()`

5. **Which widget is used to arrange children horizontally?**
   - a) `Column`
   - b) `Row`
   - c) `Stack`
   - d) `ListView`

---

### **Conclusion**

Session 4 provides a foundational understanding of Flutter widgets, including the differences between `StatelessWidget` and `StatefulWidget`, the widget tree, and key basic widgets. Mastery of these concepts is crucial for developing and designing user interfaces in Flutter applications.
