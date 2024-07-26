## Session 5: Handling User Input and Forms

### Duration
- **Total Time**: 3 hours

### Objectives
By the end of this session, students should be able to:
1. Understand and implement user input handling in Flutter.
2. Create and validate forms.
3. Manage form state and handle user interactions effectively.

### Materials Needed
- Laptops with Flutter SDK installed
- Code editor (Visual Studio Code, Android Studio, or IntelliJ IDEA)
- Projector or screen for demonstrations

### Detailed Material

### **1. Handling User Input (60 minutes)**

#### **1.1 Text Input**
- **TextField Widget**:
  - **Purpose**: Collect single-line or multi-line text input from users.
  - **Example**:
    ```dart
    TextField(
      decoration: InputDecoration(
        labelText: 'Enter your name',
        border: OutlineInputBorder(),
      ),
      onChanged: (text) {
        print('Text entered: $text');
      },
    )
    ```

- **TextEditingController**:
  - **Purpose**: Retrieve and manipulate the text from `TextField`.
  - **Example**:
    ```dart
    final TextEditingController _controller = TextEditingController();

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        body: Column(
          children: <Widget>[
            TextField(
              controller: _controller,
              decoration: InputDecoration(labelText: 'Enter your name'),
            ),
            ElevatedButton(
              onPressed: () {
                print('Text entered: ${_controller.text}');
              },
              child: Text('Submit'),
            ),
          ],
        ),
      );
    }
    ```

- **Reference**:
  - [Flutter TextField Documentation](https://flutter.dev/docs/development/ui/widgets/text)

#### **1.2 Number Input**
- **TextFormField Widget with InputType.number**:
  - **Purpose**: Collect numerical input from users.
  - **Example**:
    ```dart
    TextFormField(
      keyboardType: TextInputType.number,
      decoration: InputDecoration(
        labelText: 'Enter your age',
        border: OutlineInputBorder(),
      ),
      onChanged: (value) {
        print('Number entered: $value');
      },
    )
    ```

- **Reference**:
  - [Flutter TextFormField Documentation](https://flutter.dev/docs/development/ui/widgets/text-input)

#### **1.3 Other Input Types**
- **Switches, Checkboxes, and Radio Buttons**:
  - **Switch**:
    ```dart
    Switch(
      value: _switchValue,
      onChanged: (value) {
        setState(() {
          _switchValue = value;
        });
      },
    )
    ```

  - **Checkbox**:
    ```dart
    Checkbox(
      value: _checkboxValue,
      onChanged: (value) {
        setState(() {
          _checkboxValue = value!;
        });
      },
    )
    ```

  - **Radio**:
    ```dart
    Radio(
      value: 1,
      groupValue: _radioValue,
      onChanged: (value) {
        setState(() {
          _radioValue = value!;
        });
      },
    )
    ```

- **Reference**:
  - [Flutter Switch, Checkbox, and Radio Documentation](https://flutter.dev/docs/development/ui/widgets/material#input)

### **2. Forms and Validation (60 minutes)**

#### **2.1 Creating Forms**
- **Form Widget**:
  - **Purpose**: Group form fields and handle form submission.
  - **Example**:
    ```dart
    final _formKey = GlobalKey<FormState>();

    @override
    Widget build(BuildContext context) {
      return Form(
        key: _formKey,
        child: Column(
          children: <Widget>[
            TextFormField(
              decoration: InputDecoration(labelText: 'Enter your name'),
              validator: (value) {
                if (value == null || value.isEmpty) {
                  return 'Please enter some text';
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
      );
    }
    ```

- **Reference**:
  - [Flutter Forms Documentation](https://flutter.dev/docs/development/ui/forms)

#### **2.2 Form Validation**
- **Validation Rules**:
  - **Example**:
    ```dart
    String? _validateName(String? value) {
      if (value == null || value.isEmpty) {
        return 'Name is required';
      }
      return null;
    }

    @override
    Widget build(BuildContext context) {
      return Form(
        key: _formKey,
        child: Column(
          children: <Widget>[
            TextFormField(
              decoration: InputDecoration(labelText: 'Enter your name'),
              validator: _validateName,
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
      );
    }
    ```

- **Reference**:
  - [Flutter Form Validation](https://flutter.dev/docs/development/ui/forms#validating-input)

#### **2.3 Handling Form State**
- **Saving Form State**:
  - **Example**:
    ```dart
    void _saveForm() {
      if (_formKey.currentState!.validate()) {
        _formKey.currentState!.save();
        // Process the form data
      }
    }
    ```

- **Reference**:
  - [Flutter Form State Management](https://flutter.dev/docs/development/ui/forms#handling-form-state)

### **3. Hands-On Exercise and Practice (30 minutes)**

#### **3.1 Build a Form with Validation**
- **Objective**: Develop a form with multiple fields and implement validation.
- **Exercise**:
  - Create a form with text fields, number fields, and selection widgets (switches, checkboxes, radio buttons).
  - Implement validation for required fields and ensure correct data entry.

- **Reference**:
  - [Flutter Form Building and Validation Examples](https://flutter.dev/docs/cookbook/forms)

### **4. Q&A and Wrap-Up (30 minutes)**

#### **4.1 Addressing Questions**
- Open floor for students to ask questions related to user input handling and forms.

#### **4.2 Recap of the Day**
- Summary of key points covered in the session.

#### **4.3 Homework Assignment**
- **Create a Multi-Field Form**:
  - Build a more complex form that includes multiple types of input fields and validation rules. For example, a registration form with user details, contact information, and preferences.

- **Reference**:
  - [Advanced Form Examples](https://flutter.dev/docs/cookbook/forms/validation)
