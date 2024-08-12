### **Lecture Notes: Session 7 - Widgets Deep Dive**

---

#### **1. Detailed Exploration of Common Widgets**

**a. Buttons:**

- **Definition:** Buttons are interactive widgets that trigger an action when pressed. They come in various types and styles in Flutter.

- **Types of Buttons:**
  - **ElevatedButton:** A material design button with a shadow, often used for primary actions.
  - **TextButton:** A button without elevation, typically used for secondary actions.
  - **OutlinedButton:** A button with a border, used for actions that are less prominent.

- **Examples:**
  - **ElevatedButton:**
    ```dart
    ElevatedButton(
      onPressed: () {
        // Handle button press
      },
      child: Text('Elevated Button'),
    )
    ```

  - **TextButton:**
    ```dart
    TextButton(
      onPressed: () {
        // Handle button press
      },
      child: Text('Text Button'),
    )
    ```

  - **OutlinedButton:**
    ```dart
    OutlinedButton(
      onPressed: () {
        // Handle button press
      },
      child: Text('Outlined Button'),
    )
    ```

**b. Icons:**

- **Definition:** Icons are visual representations used to convey meaning through imagery. They are used to enhance the UI and provide visual cues.

- **Key Properties:**
  - **icon:** The icon to display.
  - **color:** The color of the icon.
  - **size:** The size of the icon.

- **Examples:**
  - **Using Icons:**
    ```dart
    Icon(
      Icons.home,
      color: Colors.blue,
      size: 30.0,
    )
    ```

  - **Icons in Buttons:**
    ```dart
    ElevatedButton.icon(
      onPressed: () {
        // Handle button press
      },
      icon: Icon(Icons.add),
      label: Text('Add Item'),
    )
    ```

**c. TextFields:**

- **Definition:** `TextField` is a widget used for user input, allowing the user to enter text.

- **Key Properties:**
  - **controller:** Controls the text being edited.
  - **decoration:** Defines the appearance, including labels, hints, and borders.
  - **obscureText:** Obscures the text (useful for passwords).

- **Examples:**
  - **Basic TextField:**
    ```dart
    TextField(
      decoration: InputDecoration(
        labelText: 'Enter your name',
      ),
    )
    ```

  - **TextField with Controller:**
    ```dart
    final TextEditingController _controller = TextEditingController();

    TextField(
      controller: _controller,
      decoration: InputDecoration(
        labelText: 'Enter your email',
      ),
    )
    ```

---

#### **2. Handling User Input and Forms**

**a. Handling User Input:**

- **TextEditingController:**
  - **Purpose:** Manages the text input and allows for reading and updating the text.
  - **Example:**
    ```dart
    final TextEditingController _controller = TextEditingController();

    TextField(
      controller: _controller,
      decoration: InputDecoration(
        labelText: 'Enter your text',
      ),
    )
    ```

- **FocusNode:**
  - **Purpose:** Manages the focus of a text field, allowing you to handle focus changes.
  - **Example:**
    ```dart
    final FocusNode _focusNode = FocusNode();

    TextField(
      focusNode: _focusNode,
      decoration: InputDecoration(
        labelText: 'Focused TextField',
      ),
    )
    ```

**b. Forms:**

- **Definition:** Forms are used to collect user input and validate it. The `Form` widget groups `TextFormField` widgets and provides validation functionality.

- **Key Properties:**
  - **key:** A unique key for the form.
  - **onSaved:** A callback function to save the form's state.

- **Example:**
  ```dart
  final _formKey = GlobalKey<FormState>();

  Form(
    key: _formKey,
    child: Column(
      children: <Widget>[
        TextFormField(
          decoration: InputDecoration(labelText: 'Name'),
          validator: (value) {
            if (value == null || value.isEmpty) {
              return 'Please enter your name';
            }
            return null;
          },
        ),
        TextFormField(
          decoration: InputDecoration(labelText: 'Email'),
          validator: (value) {
            if (value == null || value.isEmpty) {
              return 'Please enter your email';
            }
            return null;
          },
        ),
        ElevatedButton(
          onPressed: () {
            if (_formKey.currentState?.validate() ?? false) {
              // Process data
            }
          },
          child: Text('Submit'),
        ),
      ],
    ),
  )
  ```

**c. Validating Forms:**

- **Validation Function:** Use `validator` to check the validity of user input.
- **Saving Form State:** Use `onSaved` to handle the form submission and save data.

---

#### **3. Customizing Widgets (Styling, Theming, and Decoration)**

**a. Styling Widgets:**

- **Text Styling:**
  - **Example:**
    ```dart
    Text(
      'Styled Text',
      style: TextStyle(
        color: Colors.red,
        fontSize: 20,
        fontWeight: FontWeight.bold,
      ),
    )
    ```

- **Button Styling:**
  - **Example:**
    ```dart
    ElevatedButton(
      onPressed: () {},
      style: ElevatedButton.styleFrom(
        primary: Colors.purple,
        onPrimary: Colors.white,
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.circular(12),
        ),
      ),
      child: Text('Styled Button'),
    )
    ```

**b. Theming Widgets:**

- **Definition:** Theming allows you to define consistent styling across your application using a theme. You can customize colors, fonts, and shapes.

- **Example:**
  ```dart
  ThemeData(
    primarySwatch: Colors.teal,
    accentColor: Colors.orange,
    textTheme: TextTheme(
      bodyText1: TextStyle(fontSize: 18.0, fontFamily: 'Hind'),
    ),
  )
  ```

- **Applying Theme:**
  ```dart
  MaterialApp(
    theme: ThemeData(
      primarySwatch: Colors.blue,
    ),
    home: MyHomePage(),
  )
  ```

**c. Decoration:**

- **Container Decoration:**
  - **Example:**
    ```dart
    Container(
      decoration: BoxDecoration(
        color: Colors.green,
        borderRadius: BorderRadius.circular(15),
        boxShadow: [
          BoxShadow(
            color: Colors.black.withOpacity(0.3),
            spreadRadius: 5,
            blurRadius: 7,
            offset: Offset(0, 3),
          ),
        ],
      ),
      child: Padding(
        padding: EdgeInsets.all(16.0),
        child: Text('Decorated Container'),
      ),
    )
    ```

- **InputDecoration for TextField:**
  - **Example:**
    ```dart
    TextField(
      decoration: InputDecoration(
        labelText: 'Enter text',
        border: OutlineInputBorder(),
        prefixIcon: Icon(Icons.text_fields),
      ),
    )
    ```

**d. Best Practices:**

- **Consistent Styling:** Use themes to maintain consistent styling across your application.
- **Performance:** Avoid excessive use of decorations that may impact performance.
- **Responsiveness:** Ensure widgets adapt to different screen sizes and orientations.

---

### **Conclusion**

In this session, we explored common Flutter widgets such as buttons, icons, and text fields, including how to handle user input and forms effectively. We also covered customizing widgets through styling, theming, and decoration. Mastery of these concepts is essential for creating a visually appealing and user-friendly Flutter application.
