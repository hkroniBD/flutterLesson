### **Session 13: Forms and Input Validation**

#### **Objective:**
This session focuses on creating and managing forms in Flutter, handling form validation and submission, managing form state, and developing custom form field widgets.

---

### **1. Creating Forms in Flutter**

**a. Overview**

- Forms in Flutter are used to collect user input. The primary widget for forms is `Form`, which can contain one or more `FormField` widgets such as `TextFormField`.

**b. Example:**

- **Basic Form Creation:**

  ```dart
  import 'package:flutter/material.dart';

  void main() => runApp(MyApp());

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          appBar: AppBar(title: Text('Form Example')),
          body: Padding(
            padding: EdgeInsets.all(16.0),
            child: MyForm(),
          ),
        ),
      );
    }
  }

  class MyForm extends StatefulWidget {
    @override
    _MyFormState createState() => _MyFormState();
  }

  class _MyFormState extends State<MyForm> {
    final _formKey = GlobalKey<FormState>();
    final _nameController = TextEditingController();

    @override
    Widget build(BuildContext context) {
      return Form(
        key: _formKey,
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            TextFormField(
              controller: _nameController,
              decoration: InputDecoration(labelText: 'Name'),
              validator: (value) {
                if (value == null || value.isEmpty) {
                  return 'Please enter some text';
                }
                return null;
              },
            ),
            Padding(
              padding: EdgeInsets.symmetric(vertical: 16.0),
              child: ElevatedButton(
                onPressed: () {
                  if (_formKey.currentState!.validate()) {
                    ScaffoldMessenger.of(context).showSnackBar(
                      SnackBar(content: Text('Processing Data')),
                    );
                  }
                },
                child: Text('Submit'),
              ),
            ),
          ],
        ),
      );
    }
  }
  ```

- **References:**
  - [Flutter Forms Documentation](https://flutter.dev/docs/development/ui/widgets/form)

---

### **2. Handling Form Validation and Submission**

**a. Validation**

- Validation is performed by using the `validator` property of `TextFormField`. It returns a `String` with the error message if validation fails or `null` if the input is valid.

**b. Submitting Forms**

- Forms are submitted by calling `validate()` on the `FormState`. If validation passes, form data can be processed or submitted.

**c. Example:**

  ```dart
  void _submitForm() {
    if (_formKey.currentState!.validate()) {
      // Process data
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Form Submitted')),
      );
    }
  }
  ```

- **References:**
  - [Flutter Form Validation](https://flutter.dev/docs/cookbook/forms/validation)

---

### **3. Managing Form State**

**a. Overview**

- Form state management involves keeping track of the form’s state, including its data and validation status. This is typically handled using a `GlobalKey<FormState>`.

**b. Example:**

  ```dart
  final _formKey = GlobalKey<FormState>();

  void _resetForm() {
    _formKey.currentState?.reset();
  }
  ```

**c. Form State Management Techniques**

- **Using Controllers:** Manage text input using `TextEditingController`.
- **Resetting Form State:** Use `_formKey.currentState?.reset()` to clear form data.
- **Saving Form Data:** Use `_formKey.currentState?.save()` to save form data.

- **References:**
  - [Flutter Managing Form State](https://flutter.dev/docs/cookbook/forms)

---

### **4. Custom Form Field Widgets**

**a. Overview**

- Custom form fields are created by extending `FormField` or by composing existing form field widgets.

**b. Example:**

- **Custom Text Field Widget:**

  ```dart
  import 'package:flutter/material.dart';

  class CustomTextField extends FormField<String> {
    CustomTextField({
      Key? key,
      required String initialValue,
      required FormFieldSetter<String> onSaved,
      required FormFieldValidator<String> validator,
    }) : super(
      key: key,
      initialValue: initialValue,
      onSaved: onSaved,
      validator: validator,
      builder: (FormFieldState<String> state) {
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            TextField(
              decoration: InputDecoration(
                labelText: 'Custom Field',
                errorText: state.errorText,
              ),
              onChanged: (value) {
                state.didChange(value);
              },
            ),
          ],
        );
      },
    );
  }

  // Usage
  CustomTextField(
    initialValue: '',
    onSaved: (value) {
      // Save value
    },
    validator: (value) {
      if (value == null || value.isEmpty) {
        return 'This field is required';
      }
      return null;
    },
  );
  ```

- **References:**
  - [Flutter Custom Form Fields](https://flutter.dev/docs/development/ui/widgets/form#custom-form-fields)

---

### **Assignments**

#### **Assignment 1: Create a Basic Form**

- **Objective:** Build a basic form using Flutter's `Form` and `TextFormField` widgets.
- **Tasks:**
  1. Create a form with at least two text fields and a submit button.
  2. Implement validation for each field.
  3. Handle form submission by displaying a `SnackBar` message.

#### **Assignment 2: Custom Form Field Widget**

- **Objective:** Develop a custom form field widget and use it within a form.
- **Tasks:**
  1. Create a custom form field widget that extends `FormField`.
  2. Integrate the custom field into a form.
  3. Implement validation and submission for the custom field.

---

### **Quiz**

1. **What is the purpose of the `validator` property in `TextFormField`?**
   - a) To format text input
   - b) To validate user input
   - c) To save form data
   - d) To reset the form

2. **How do you reset a form’s state in Flutter?**
   - a) By calling `reset()` on the `TextEditingController`
   - b) By using `clear()` on `TextFormField`
   - c) By calling `_formKey.currentState?.reset()`
   - d) By creating a new `Form` widget

3. **What is the benefit of using `InheritedWidget` for state management in forms?**
   - a) To store local form data
   - b) To provide form state to descendant widgets efficiently
   - c) To handle form validation
   - d) To manage form submission

4. **How can custom form field widgets enhance your Flutter app?**
   - a) By improving form validation
   - b) By allowing for more flexible and reusable form fields
   - c) By managing state automatically
   - d) By adding animations to form fields

5. **Which method should be used to handle form submission in Flutter?**
   - a) `FormState.save()`
   - b) `FormState.validate()`
   - c) `FormState.submit()`
   - d) `FormState.reset()`

---

### **Conclusion**

Session 13 provides a comprehensive overview of forms and input validation in Flutter, covering form creation, validation, state management, and custom form field widgets. These concepts are crucial for building interactive and user-friendly applications that require data input and validation.
