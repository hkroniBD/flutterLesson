## Session 3: Flutter Widgets and Layouts

### Duration
- **Total Time**: 3 hours

### Objectives
By the end of this session, students should be able to:
1. Understand and use basic Flutter widgets.
2. Create and organize UI layouts using Flutter’s layout widgets.
3. Apply styling and customization to widgets.

### Materials Needed
- Laptops with Flutter SDK installed
- Code editor (Visual Studio Code, Android Studio, or IntelliJ IDEA)
- Projector or screen for demonstrations

### Detailed Material

### **1. Introduction to Flutter Widgets (60 minutes)**

#### **1.1 What is a Widget?**
- **Definition**: In Flutter, everything is a widget. Widgets are the building blocks of a Flutter app’s UI.
- **Types of Widgets**:
  - **StatelessWidget**: Immutable and does not change over time.
  - **StatefulWidget**: Mutable and can change state during runtime.

- **Reference**:
  - [Flutter Widgets Overview](https://flutter.dev/docs/development/ui/widgets)

#### **1.2 Basic Flutter Widgets**
- **Text Widget**:
  - **Purpose**: Display text on the screen.
  - **Example**:
    ```dart
    Text('Hello, Flutter!', style: TextStyle(fontSize: 24, color: Colors.blue))
    ```

- **Container Widget**:
  - **Purpose**: A versatile widget that can hold other widgets and apply padding, margin, and decoration.
  - **Example**:
    ```dart
    Container(
      padding: EdgeInsets.all(16),
      color: Colors.yellow,
      child: Text('Inside a Container'),
    )
    ```

- **Row and Column Widgets**:
  - **Purpose**: Arrange children widgets horizontally (Row) or vertically (Column).
  - **Example**:
    ```dart
    Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: <Widget>[
        Text('One'),
        Text('Two'),
        Text('Three'),
      ],
    )
    ```

    ```dart
    Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: <Widget>[
        Text('Top'),
        Text('Middle'),
        Text('Bottom'),
      ],
    )
    ```

- **Reference**:
  - [Flutter Basic Widgets](https://flutter.dev/docs/development/ui/widgets-intro)

### **2. Layout Widgets (60 minutes)**

#### **2.1 Using Layout Widgets**
- **Padding Widget**:
  - **Purpose**: Add space around a widget.
  - **Example**:
    ```dart
    Padding(
      padding: EdgeInsets.all(16),
      child: Text('Padding Example'),
    )
    ```

- **Align Widget**:
  - **Purpose**: Align a widget within its parent.
  - **Example**:
    ```dart
    Align(
      alignment: Alignment.center,
      child: Text('Aligned Center'),
    )
    ```

- **SizedBox Widget**:
  - **Purpose**: Create a box with a specified size.
  - **Example**:
    ```dart
    SizedBox(
      width: 100,
      height: 100,
      child: Container(color: Colors.red),
    )
    ```

- **Expanded and Flexible Widgets**:
  - **Purpose**: Control how a widget expands within a Row or Column.
  - **Example**:
    ```dart
    Expanded(
      child: Container(color: Colors.green),
    )
    ```

    ```dart
    Flexible(
      child: Container(color: Colors.blue),
      flex: 2,
    )
    ```

- **Reference**:
  - [Flutter Layout Widgets](https://flutter.dev/docs/development/ui/layout)

#### **2.2 Creating Complex Layouts**
- **Stack Widget**:
  - **Purpose**: Overlay widgets on top of each other.
  - **Example**:
    ```dart
    Stack(
      children: <Widget>[
        Container(color: Colors.blue, width: 100, height: 100),
        Positioned(
          top: 20,
          left: 20,
          child: Container(color: Colors.red, width: 50, height: 50),
        ),
      ],
    )
    ```

- **GridView Widget**:
  - **Purpose**: Display items in a grid.
  - **Example**:
    ```dart
    GridView.count(
      crossAxisCount: 3,
      children: <Widget>[
        Container(color: Colors.red),
        Container(color: Colors.green),
        Container(color: Colors.blue),
      ],
    )
    ```

- **Reference**:
  - [Flutter Stack and GridView](https://flutter.dev/docs/development/ui/widgets/layout#stack)

### **3. Styling and Customization (30 minutes)**

#### **3.1 Styling Widgets**
- **Text Style**:
  - **Purpose**: Customize text appearance.
  - **Example**:
    ```dart
    Text(
      'Styled Text',
      style: TextStyle(
        fontSize: 24,
        fontWeight: FontWeight.bold,
        color: Colors.purple,
      ),
    )
    ```

- **Container Decoration**:
  - **Purpose**: Apply background color, borders, and more.
  - **Example**:
    ```dart
    Container(
      decoration: BoxDecoration(
        color: Colors.yellow,
        border: Border.all(color: Colors.black),
        borderRadius: BorderRadius.circular(8),
      ),
      child: Text('Decorated Container'),
    )
    ```

- **Reference**:
  - [Flutter Styling and Themes](https://flutter.dev/docs/development/ui/widgets-intro#styling)

### **4. Hands-On Exercise and Practice (30 minutes)**

#### **4.1 Create a Simple Layout**
- **Objective**: Build a simple layout using the widgets and concepts covered.
- **Exercise**:
  - Create a Flutter app with a layout that includes a `Row`, `Column`, `Container`, and `Stack`.
  - Apply styling to each widget.

- **Reference**:
  - [Flutter Widget Catalog](https://flutter.dev/docs/development/ui/widgets)

### **5. Q&A and Wrap-Up (30 minutes)**

#### **5.1 Addressing Questions**
- Open floor for students to ask questions related to Flutter widgets and layouts.

#### **5.2 Recap of the Day**
- Summary of key points covered in the session.

#### **5.3 Homework Assignment**
- **Build a Layout**:
  - Create a more complex layout using a combination of widgets such as `Row`, `Column`, `Stack`, and `GridView`. Incorporate styling and customization.
- **Reference**:
  - [Flutter Layouts and Widgets](https://flutter.dev/docs/development/ui/layout)
