### **Session 7: Widgets Deep Dive**

#### **Objective:**
This session provides an in-depth exploration of common Flutter widgets, focusing on buttons, icons, and text fields. It also covers handling user input and forms and customizing widgets through styling, theming, and decoration.

---

### **1. Detailed Exploration of Common Widgets**

**a. Buttons:**

- **Types of Buttons:**
  - **ElevatedButton:** A button with a shadow that appears elevated above the surrounding content.
  - **TextButton:** A button with no elevation or border, typically used for simple text interactions.
  - **OutlinedButton:** A button with an outline but no background color, suitable for secondary actions.

- **Syntax Examples:**
  ```dart
  ElevatedButton(
    onPressed: () {
      // Handle button press
    },
    child: Text('Elevated Button'),
  )

  TextButton(
    onPressed: () {
      // Handle button press
    },
    child: Text('Text Button'),
  )

  OutlinedButton(
    onPressed: () {
      // Handle button press
    },
    child: Text('Outlined Button'),
  )
  ```

- **References:**
  - [ElevatedButton Documentation](https://flutter.dev/docs/development/ui/widgets/material#elevatedbutton)
  - [TextButton Documentation](https://flutter.dev/docs/development/ui/widgets/material#textbutton)
  - [OutlinedButton Documentation](https://flutter.dev/docs/development/ui/widgets/material#outlinedbutton)

**b. Icons:**

- **Definition:**
  - `Icon` widgets are used to display icons from the Material Icons font.

- **Syntax Example:**
  ```dart
  Icon(
    Icons.star,
    color: Colors.yellow,
    size: 50.0,
  )
  ```

- **References:**
  - [Icon Documentation](https://flutter.dev/docs/development/ui/widgets/material#icon)

**c. TextFields:**

- **Definition:**
  - `TextField` widgets are used for user input in text form.

- **Syntax Example:**
  ```dart
  TextField(
    decoration: InputDecoration(
      labelText: 'Enter your text',
      border: OutlineInputBorder(),
    ),
    onChanged: (text) {
      // Handle text input
    },
  )
  ```

- **References:**
  - [TextField Documentation](https://flutter.dev/docs/development/ui/widgets/material#textfield)

---

### **2. Handling User Input and Forms**

**a. Creating Forms:**

- **Definition:**
  - Forms in Flutter allow users to enter and submit data. The `Form` widget helps manage form state and validation.

- **Syntax Example:**
  ```dart
  final _formKey = GlobalKey<FormState>();

  Form(
    key: _formKey,
    child: Column(
      children: <Widget>[
        TextFormField(
          decoration: InputDecoration(labelText: 'Username'),
          validator: (value) {
            if (value == null || value.isEmpty) {
              return 'Please enter your username';
            }
            return null;
          },
        ),
        TextFormField(
          decoration: InputDecoration(labelText: 'Password'),
          obscureText: true,
          validator: (value) {
            if (value == null || value.isEmpty) {
              return 'Please enter your password';
            }
            return null;
          },
        ),
        ElevatedButton(
          onPressed: () {
            if (_formKey.currentState!.validate()) {
              // Process data
            }
          },
          child: Text('Submit'),
        ),
      ],
    ),
  )
  ```

- **References:**
  - [Form Documentation](https://flutter.dev/docs/development/ui/widgets/forms)
  - [TextFormField Documentation](https://flutter.dev/docs/development/ui/widgets/forms#textformfield)

**b. Handling Form Validation:**

- **Definition:**
  - Form validation ensures that user input meets certain criteria before submission.

- **Syntax Example:**
  ```dart
  TextFormField(
    decoration: InputDecoration(labelText: 'Email'),
    validator: (value) {
      if (value == null || !RegExp(r'^[^@]+@[^@]+\.[^@]+').hasMatch(value)) {
        return 'Please enter a valid email address';
      }
      return null;
    },
  )
  ```

- **References:**
  - [Form Validation Documentation](https://flutter.dev/docs/development/ui/widgets/forms#validating-input)

---

### **3. Customizing Widgets (Styling, Theming, and Decoration)**

**a. Styling Widgets:**

- **Text Styling:**
  - Use the `TextStyle` class to apply styling to text.

- **Syntax Example:**
  ```dart
  Text(
    'Styled Text',
    style: TextStyle(
      fontSize: 24.0,
      fontWeight: FontWeight.bold,
      color: Colors.blue,
    ),
  )
  ```

- **References:**
  - [TextStyle Documentation](https://flutter.dev/docs/development/ui/widgets/text#textstyle)

**b. Theming:**

- **Definition:**
  - Theming allows you to apply consistent styling across your app using the `ThemeData` class.

- **Syntax Example:**
  ```dart
  ThemeData(
    primarySwatch: Colors.blue,
    textTheme: TextTheme(
      headline1: TextStyle(fontSize: 72.0, fontWeight: FontWeight.bold),
      bodyText1: TextStyle(fontSize: 14.0),
    ),
  )
  ```

- **References:**
  - [Theming Documentation](https://flutter.dev/docs/development/ui/widgets/material#themes)

**c. Decoration:**

- **Definition:**
  - Use the `BoxDecoration` class to decorate containers with background color, border, and shadows.

- **Syntax Example:**
  ```dart
  Container(
    decoration: BoxDecoration(
      color: Colors.green,
      borderRadius: BorderRadius.circular(10.0),
      boxShadow: [
        BoxShadow(
          color: Colors.black26,
          blurRadius: 5.0,
          offset: Offset(0, 2),
        ),
      ],
    ),
    child: Padding(
      padding: const EdgeInsets.all(8.0),
      child: Text('Decorated Container'),
    ),
  )
  ```

- **References:**
  - [BoxDecoration Documentation](https://flutter.dev/docs/development/ui/widgets/container#decoration)

---

### **Assignments**

#### **Assignment 1: Button and Icon Implementation**

- **Objective:** Practice using different button types and icons.
- **Tasks:**
  1. Create a UI with `ElevatedButton`, `TextButton`, and `OutlinedButton`. Apply different styles to each button.
  2. Add icons to a list of `ListTile` widgets and style them appropriately.

#### **Assignment 2: Form Creation and Validation**

- **Objective:** Build a form with validation and handle user input.
- **Tasks:**
  1. Create a form with fields for email, password, and phone number. Add validation rules for each field.
  2. Implement a submit button that processes the form data when valid.

#### **Assignment 3: Customizing Widgets**

- **Objective:** Apply styling, theming, and decoration to widgets.
- **Tasks:**
  1. Customize a `Text` widget with various `TextStyle` attributes.
  2. Create a themed `MaterialApp` with a custom `ThemeData`.
  3. Decorate a `Container` with background color, border, and shadow effects.

---

### **Quiz**

1. **Which widget is used for creating a button with a shadow?**
   - a) TextButton
   - b) OutlinedButton
   - c) ElevatedButton
   - d) IconButton

2. **What is the purpose of the `TextFormField` widget in Flutter?**
   - a) To display images
   - b) To create a button
   - c) To handle text input from users
   - d) To display icons

3. **How can you ensure that a form field contains a valid email address?**
   - a) Use the `TextStyle` class
   - b) Use a `RegExp` pattern in the validator function
   - c) Set a minimum character length
   - d) Apply `BoxDecoration`

4. **What does `ThemeData` allow you to do in a Flutter app?**
   - a) Add animations
   - b) Define global styling and theming for the app
   - c) Manage local storage
   - d) Implement navigation and routing

5. **Which class is used to add background color and borders to a container?**
   - a) TextStyle
   - b) ThemeData
   - c) BoxDecoration
   - d) InputDecoration

---

### **Conclusion**

Session 7 provides a deep dive into common Flutter widgets such as buttons, icons, and text fields. It covers how to handle user input through forms, validate input, and customize widgets using styling, theming, and decoration techniques. Mastery of these concepts is crucial for building interactive and visually appealing Flutter applications.
