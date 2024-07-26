## Session 4: Building Layouts in Flutter

### Duration
- **Total Time**: 3 hours

### Objectives
By the end of this session, students should be able to:
1. Understand and use Flex, Expanded, and Spacer widgets for layout design.
2. Implement Stack and Positioned widgets for layered UI elements.
3. Build responsive layouts using MediaQuery.
4. Gain an introduction to Flutter's Material Design components and principles.

### Materials Needed
- Laptops with Flutter SDK installed
- Code editor (Visual Studio Code, Android Studio, or IntelliJ IDEA)
- Projector or screen for demonstrations

### Detailed Material

### **1. Using Flex, Expanded, and Spacer Widgets (60 minutes)**

#### **1.1 Overview of Flex Layout**
- **Definition**: Flex is a layout model that allows for flexible sizing and positioning of widgets in a row or column.
- **Flex and Expanded Widgets**:
  - **Flex**: A widget that directs its children to be laid out horizontally or vertically.
  - **Expanded**: A widget that expands a child of a Row, Column, or Flex so that the child fills the available space.

- **Example**:
  ```dart
  import 'package:flutter/material.dart';

  class FlexExample extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(title: Text('Flex Example')),
        body: Column(
          children: <Widget>[
            Row(
              children: <Widget>[
                Expanded(child: Container(color: Colors.red, height: 100)),
                Expanded(child: Container(color: Colors.green, height: 100)),
                Expanded(child: Container(color: Colors.blue, height: 100)),
              ],
            ),
            Spacer(),
            Container(color: Colors.yellow, height: 50),
          ],
        ),
      );
    }
  }
  ```

- **Reference**:
  - [Flex Widget Documentation](https://flutter.dev/docs/development/ui/widgets/layout#flex)

#### **1.2 Using Spacer Widget**
- **Definition**: Spacer is used within a Flex container to create empty space between widgets.
- **Usage**:
  - **Example**:
    ```dart
    Row(
      children: <Widget>[
        Container(color: Colors.red, width: 50),
        Spacer(),
        Container(color: Colors.green, width: 50),
      ],
    )
    ```

- **Reference**:
  - [Spacer Widget Documentation](https://api.flutter.dev/flutter/widgets/Spacer-class.html)

### **2. Using Stack and Positioned Widgets (60 minutes)**

#### **2.1 Overview of Stack Layout**
- **Definition**: Stack allows for the overlaying of widgets on top of one another.
- **Stack and Positioned Widgets**:
  - **Stack**: A widget that places its children on top of each other in a z-order.
  - **Positioned**: A widget that specifies where a child should be positioned within a Stack.

- **Example**:
  ```dart
  import 'package:flutter/material.dart';

  class StackExample extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(title: Text('Stack Example')),
        body: Stack(
          children: <Widget>[
            Container(color: Colors.red, width: 300, height: 300),
            Positioned(
              top: 50,
              left: 50,
              child: Container(color: Colors.green, width: 100, height: 100),
            ),
            Positioned(
              bottom: 50,
              right: 50,
              child: Container(color: Colors.blue, width: 100, height: 100),
            ),
          ],
        ),
      );
    }
  }
  ```

- **Reference**:
  - [Stack Widget Documentation](https://flutter.dev/docs/development/ui/widgets/layout#stack)

### **3. Building Responsive Layouts with MediaQuery (30 minutes)**

#### **3.1 Introduction to MediaQuery**
- **Definition**: MediaQuery provides information about the size and orientation of the screen.
- **Usage**:
  - **Example**:
    ```dart
    import 'package:flutter/material.dart';

    class MediaQueryExample extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        final mediaQuery = MediaQuery.of(context);
        final screenWidth = mediaQuery.size.width;

        return Scaffold(
          appBar: AppBar(title: Text('MediaQuery Example')),
          body: Center(
            child: Container(
              color: Colors.blue,
              width: screenWidth * 0.8,
              height: 100,
              child: Center(child: Text('80% of screen width')),
            ),
          ),
        );
      }
    }
    ```

- **Reference**:
  - [MediaQuery Documentation](https://flutter.dev/docs/development/ui/media-query)

### **4. Introduction to Flutter's Material Design (30 minutes)**

#### **4.1 Overview of Material Design**
- **Definition**: Material Design is a design system created by Google that provides guidelines and components for creating visually appealing and functional user interfaces.
- **Key Principles**: Material Design emphasizes usability, accessibility, and a cohesive visual language.

- **Reference**:
  - [Material Design Overview](https://material.io/design)

#### **4.2 Using Material Components**
- **Examples**:
  - **AppBar**:
    ```dart
    AppBar(
      title: Text('Material Design Example'),
      backgroundColor: Colors.blue,
    )
    ```

  - **FloatingActionButton**:
    ```dart
    FloatingActionButton(
      onPressed: () {},
      child: Icon(Icons.add),
      backgroundColor: Colors.blue,
    )
    ```

  - **Card**:
    ```dart
    Card(
      elevation: 5,
      child: Padding(
        padding: EdgeInsets.all(16),
        child: Text('This is a card'),
      ),
    )
    ```

- **Reference**:
  - [Material Components Documentation](https://flutter.dev/docs/development/ui/widgets/material)

### **5. Hands-On Exercise and Practice (30 minutes)**

#### **5.1 Build a Responsive Layout with Stack**
- **Objective**: Create a layout using Stack and Positioned widgets with responsive design elements.
- **Exercise**:
  - Develop a UI that utilizes Stack for overlapping elements and MediaQuery for responsive adjustments. Implement Material Design components in the layout.

- **Reference**:
  - [Responsive Layout Examples](https://flutter.dev/docs/development/ui/layout/responsive)

### **6. Q&A and Wrap-Up (30 minutes)**

#### **6.1 Addressing Questions**
- Open floor for students to ask questions related to layout design and Material Design.

#### **6.2 Recap of the Day**
- Summary of key points covered in the session.

#### **6.3 Homework Assignment**
- **Design a Multi-Layout App**:
  - Create an app that includes different layout techniques using Flex, Stack, and MediaQuery. Implement Material Design components to enhance the UI.

- **Reference**:
  - [Multi-Layout Examples](https://flutter.dev/docs/development/ui/layout)
