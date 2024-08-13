### **Session 23: Styling and Theming**

#### **Objective:**
This session explores how to style and theme Flutter applications. Students will learn how to customize the look and feel of their app, implement themes including dark mode, use Google Fonts and custom fonts, and manage global styles and themes.

---

### **1. Customizing the Look and Feel of Your Flutter App**

**a. Styling Widgets:**

   - **Text Styling:**
     - Use the `TextStyle` class to style text.
     - Example:
       ```dart
       Text(
         'Hello, Flutter!',
         style: TextStyle(
           fontSize: 24,
           fontWeight: FontWeight.bold,
           color: Colors.blue,
         ),
       )
       ```

   - **Container Styling:**
     - Customize `Container` with properties like `padding`, `margin`, `decoration`, and `border`.
     - Example:
       ```dart
       Container(
         padding: EdgeInsets.all(16),
         margin: EdgeInsets.symmetric(vertical: 8),
         decoration: BoxDecoration(
           color: Colors.lightBlue,
           borderRadius: BorderRadius.circular(8),
         ),
         child: Text('Styled Container'),
       )
       ```

   - **Button Styling:**
     - Style buttons using properties of `ElevatedButton`, `TextButton`, and `OutlinedButton`.
     - Example:
       ```dart
       ElevatedButton(
         onPressed: () {},
         style: ElevatedButton.styleFrom(
           primary: Colors.green,
           onPrimary: Colors.white,
           padding: EdgeInsets.symmetric(horizontal: 16, vertical: 8),
         ),
         child: Text('Styled Button'),
       )
       ```

**b. Customizing App Bar and Bottom Navigation:**

   - **AppBar Customization:**
     - Customize `AppBar` with properties like `backgroundColor`, `titleTextStyle`, and `elevation`.
     - Example:
       ```dart
       AppBar(
         title: Text('Custom AppBar'),
         backgroundColor: Colors.deepPurple,
         elevation: 4,
       )
       ```

   - **BottomNavigationBar Customization:**
     - Style `BottomNavigationBar` with `selectedItemColor`, `unselectedItemColor`, and `backgroundColor`.
     - Example:
       ```dart
       BottomNavigationBar(
         items: [
           BottomNavigationBarItem(
             icon: Icon(Icons.home),
             label: 'Home',
           ),
           BottomNavigationBarItem(
             icon: Icon(Icons.search),
             label: 'Search',
           ),
         ],
         selectedItemColor: Colors.blue,
         unselectedItemColor: Colors.grey,
         backgroundColor: Colors.white,
       )
       ```

---

### **2. Implementing Themes and Dark Mode**

**a. Defining Themes:**

   - **Creating a ThemeData:**
     - Define themes in the `MaterialApp` widget using `ThemeData`.
     - Example:
       ```dart
       MaterialApp(
         theme: ThemeData(
           primarySwatch: Colors.blue,
           accentColor: Colors.orange,
           textTheme: TextTheme(
             headline1: TextStyle(fontSize: 72.0, fontWeight: FontWeight.bold),
             bodyText1: TextStyle(fontSize: 14.0, fontFamily: 'Hind'),
           ),
         ),
         home: HomeScreen(),
       )
       ```

**b. Implementing Dark Mode:**

   - **Using ThemeMode:**
     - Implement dark mode by providing `darkTheme` and using `ThemeMode`.
     - Example:
       ```dart
       MaterialApp(
         theme: ThemeData.light(), // Light theme
         darkTheme: ThemeData.dark(), // Dark theme
         themeMode: ThemeMode.system, // Switches between light and dark based on system settings
         home: HomeScreen(),
       )
       ```

**c. Toggle Dark Mode Manually:**

   - **Using a Switch:**
     - Add a switch or toggle in your app to switch between light and dark themes manually.
     - Example:
       ```dart
       class ThemeSwitcher extends StatefulWidget {
         @override
         _ThemeSwitcherState createState() => _ThemeSwitcherState();
       }

       class _ThemeSwitcherState extends State<ThemeSwitcher> {
         bool _isDarkMode = false;

         @override
         Widget build(BuildContext context) {
           return MaterialApp(
             theme: _isDarkMode ? ThemeData.dark() : ThemeData.light(),
             home: Scaffold(
               appBar: AppBar(
                 title: Text('Theme Switcher'),
                 actions: [
                   Switch(
                     value: _isDarkMode,
                     onChanged: (value) {
                       setState(() {
                         _isDarkMode = value;
                       });
                     },
                   ),
                 ],
               ),
             ),
           );
         }
       }
       ```

---

### **3. Using Google Fonts and Custom Fonts**

**a. Adding Google Fonts:**

   - **Using google_fonts Package:**
     - Add `google_fonts` package to `pubspec.yaml`.
     - Example:
       ```yaml
       dependencies:
         google_fonts: ^3.0.1
       ```

   - **Using Google Fonts:**
     - Import and use Google Fonts in your app.
     - Example:
       ```dart
       import 'package:google_fonts/google_fonts.dart';

       Text(
         'Hello, Google Fonts!',
         style: GoogleFonts.lato(
           textStyle: TextStyle(fontSize: 20, fontWeight: FontWeight.w600),
         ),
       )
       ```

**b. Adding Custom Fonts:**

   - **Adding Font Files:**
     - Place font files in the `assets/fonts` directory.
     - Declare fonts in `pubspec.yaml`:
       ```yaml
       flutter:
         fonts:
           - family: CustomFont
             fonts:
               - asset: assets/fonts/CustomFont-Regular.ttf
               - asset: assets/fonts/CustomFont-Bold.ttf
                 weight: 700
       ```

   - **Using Custom Fonts:**
     - Use custom fonts in your `TextStyle`.
     - Example:
       ```dart
       Text(
         'Custom Font Text',
         style: TextStyle(
           fontFamily: 'CustomFont',
           fontSize: 20,
           fontWeight: FontWeight.bold,
         ),
       )
       ```

---

### **4. Managing Global Styles and Themes**

**a. Defining Global Styles:**

   - **Creating a Global Theme:**
     - Define and apply global styles in the `ThemeData` for consistent styling across the app.
     - Example:
       ```dart
       final ThemeData globalTheme = ThemeData(
         primarySwatch: Colors.teal,
         textTheme: TextTheme(
           bodyText1: TextStyle(color: Colors.grey[800]),
           bodyText2: TextStyle(color: Colors.grey[600]),
         ),
         buttonTheme: ButtonThemeData(
           buttonColor: Colors.teal,
           textTheme: ButtonTextTheme.primary,
         ),
       );

       MaterialApp(
         theme: globalTheme,
         home: HomeScreen(),
       )
       ```

**b. Using Theme Extensions:**

   - **Defining Extensions:**
     - Create custom theme extensions to add custom styles.
     - Example:
       ```dart
       class MyCustomTheme extends ThemeExtension<MyCustomTheme> {
         final Color customColor;

         MyCustomTheme({required this.customColor});

         @override
         MyCustomTheme copyWith({Color? customColor}) {
           return MyCustomTheme(
             customColor: customColor ?? this.customColor,
           );
         }

         @override
         MyCustomTheme lerp(ThemeExtension<MyCustomTheme>? other, double t) {
           if (other is! MyCustomTheme) return this;
           return MyCustomTheme(
             customColor: Color.lerp(customColor, other.customColor, t)!,
           );
         }
       }
       ```

   - **Using Extensions:**
     - Access custom theme properties in widgets.
     - Example:
       ```dart
       class HomeScreen extends StatelessWidget {
         @override
         Widget build(BuildContext context) {
           final customColor = Theme.of(context).extension<MyCustomTheme>()!.customColor;

           return Scaffold(
             appBar: AppBar(
               backgroundColor: customColor,
               title: Text('Custom Theme Example'),
             ),
           );
         }
       }
       ```

---

### **Assignments**

#### **Assignment 1: Apply Custom Styling**
- **Objective:** Apply custom styles to a Flutter app to enhance its appearance.
- **Tasks:**
  1. Create a sample Flutter app.
  2. Apply custom styles to text, containers, and buttons.
  3. Submit screenshots of the styled app and code.

#### **Assignment 2: Implement Dark Mode**
- **Objective:** Implement a dark mode toggle in a Flutter app.
- **Tasks:**
  1. Create a Flutter app with light mode.
  2. Add a switch to toggle between light and dark modes.
  3. Submit the code and screenshots of the app in both modes.

#### **Assignment 3: Use Google Fonts**
- **Objective:** Integrate Google Fonts into a Flutter app.
- **Tasks:**
  1. Add a Google Font to your Flutter app.
  2. Apply the Google Font to text widgets.
  3. Submit the code and screenshots of the text with the custom font.

#### **Assignment 4: Manage Global Styles**
- **Objective:** Define and use global styles in a Flutter app.
- **Tasks:**
  1. Define global styles using `ThemeData`.
  2. Apply global styles consistently across different widgets.
  3. Submit the code and screenshots demonstrating the global styles.

---

###

 **Quiz**

1. **What is the purpose of the `ThemeData` class in Flutter?**
   - a) To manage state across the app
   - b) To define and apply global styles and themes
   - c) To handle navigation and routing
   - d) To manage local data storage

2. **Which Flutter widget allows for customizing the appearance of buttons?**
   - a) Text
   - b) Container
   - c) ElevatedButton
   - d) Column

3. **How can you toggle dark mode in a Flutter app?**
   - a) Using `ThemeMode` with `darkTheme`
   - b) By modifying the app's theme manually
   - c) With a custom `Switch` widget
   - d) By setting `ThemeData` directly

4. **Which package is used to add Google Fonts to a Flutter app?**
   - a) font_awesome_flutter
   - b) google_fonts
   - c) flutter_custom_fonts
   - d) font_manager

5. **What is the purpose of the `copyWith` method in a custom theme extension?**
   - a) To create a new theme with updated properties
   - b) To apply a theme to a specific widget
   - c) To handle state management
   - d) To synchronize local and remote data

---

### **Conclusion**

Session 23 covers key concepts for styling and theming Flutter applications, including customizing widgets, implementing themes, using fonts, and managing global styles. The assignments and quizzes are designed to provide practical experience and assess understanding of these concepts.
