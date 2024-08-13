### **Session 10: Managing Assets and Media**

#### **Objective:**
This session focuses on managing various types of assets in a Flutter app, including images, fonts, audio, and video. Additionally, it introduces the `Image` widget for handling images and provides an overview of animations and transitions.

---

### **1. Managing Assets in Flutter**

**a. Managing Images and Fonts:**

- **Images:**
  - **Adding Images:**
    - Place your image files in the `assets/images/` directory.
    - Register the assets in `pubspec.yaml`:
      ```yaml
      flutter:
        assets:
          - assets/images/
      ```
  - **Using Images:**
    - **Local Images:**
      ```dart
      Image.asset('assets/images/my_image.png');
      ```
    - **Network Images:**
      ```dart
      Image.network('https://example.com/my_image.png');
      ```

- **Fonts:**
  - **Adding Fonts:**
    - Place font files in the `assets/fonts/` directory.
    - Register the fonts in `pubspec.yaml`:
      ```yaml
      flutter:
        fonts:
          - family: MyCustomFont
            fonts:
              - asset: assets/fonts/MyCustomFont-Regular.ttf
              - asset: assets/fonts/MyCustomFont-Bold.ttf
                weight: 700
      ```
  - **Using Fonts:**
    - Set font family in `TextStyle`:
      ```dart
      Text(
        'Hello, World!',
        style: TextStyle(fontFamily: 'MyCustomFont'),
      );
      ```

- **References:**
  - [Flutter Asset Management Documentation](https://flutter.dev/docs/development/ui/assets-and-images)
  - [Flutter Fonts Documentation](https://flutter.dev/docs/cookbook/design/fonts)

---

### **2. Adding Audio and Video to Your App**

**a. Adding Audio:**

- **Adding Audio Files:**
  - Place audio files in the `assets/audio/` directory.
  - Register the assets in `pubspec.yaml`:
    ```yaml
    flutter:
      assets:
        - assets/audio/
    ```

- **Playing Audio:**
  - Use the `audioplayers` package:
    ```yaml
    dependencies:
      audioplayers: ^0.20.1
    ```
  - **Example:**
    ```dart
    import 'package:audioplayers/audioplayers.dart';

    AudioPlayer audioPlayer = AudioPlayer();
    audioPlayer.play('assets/audio/my_audio.mp3');
    ```

- **References:**
  - [audioplayers Package Documentation](https://pub.dev/packages/audioplayers)

**b. Adding Video:**

- **Adding Video Files:**
  - Place video files in the `assets/videos/` directory.
  - Register the assets in `pubspec.yaml`:
    ```yaml
    flutter:
      assets:
        - assets/videos/
    ```

- **Playing Video:**
  - Use the `video_player` package:
    ```yaml
    dependencies:
      video_player: ^2.3.0
    ```
  - **Example:**
    ```dart
    import 'package:video_player/video_player.dart';

    class VideoPlayerScreen extends StatefulWidget {
      @override
      _VideoPlayerScreenState createState() => _VideoPlayerScreenState();
    }

    class _VideoPlayerScreenState extends State<VideoPlayerScreen> {
      late VideoPlayerController _controller;

      @override
      void initState() {
        super.initState();
        _controller = VideoPlayerController.asset('assets/videos/my_video.mp4')
          ..initialize().then((_) {
            setState(() {});
          });
      }

      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(title: Text('Video Player')),
          body: Center(
            child: _controller.value.isInitialized
                ? AspectRatio(
                    aspectRatio: _controller.value.aspectRatio,
                    child: VideoPlayer(_controller),
                  )
                : CircularProgressIndicator(),
          ),
          floatingActionButton: FloatingActionButton(
            onPressed: () {
              setState(() {
                _controller.value.isPlaying
                    ? _controller.pause()
                    : _controller.play();
              });
            },
            child: Icon(
              _controller.value.isPlaying ? Icons.pause : Icons.play_arrow,
            ),
          ),
        );
      }
    }
    ```

- **References:**
  - [video_player Package Documentation](https://pub.dev/packages/video_player)

---

### **3. Using the Image Widget for Local and Network Images**

**a. Displaying Local Images:**

- **Syntax Example:**
  ```dart
  Image.asset('assets/images/my_image.png');
  ```

**b. Displaying Network Images:**

- **Syntax Example:**
  ```dart
  Image.network('https://example.com/my_image.png');
  ```

- **References:**
  - [Image Widget Documentation](https://flutter.dev/docs/development/ui/widgets/intro#image)

---

### **4. Introduction to Animations and Transitions**

**a. Basic Animations:**

- **Using `AnimatedContainer`:**
  - **Example:**
    ```dart
    AnimatedContainer(
      duration: Duration(seconds: 1),
      width: _width,
      height: _height,
      color: _color,
      child: Center(child: Text('Animated Container')),
    );
    ```

- **Using `FadeTransition`:**
  - **Example:**
    ```dart
    FadeTransition(
      opacity: _animation,
      child: Text('Fade Transition'),
    );
    ```

**b. Advanced Animations:**

- **Using `Hero` Widgets:**
  - **Example:**
    ```dart
    Hero(
      tag: 'hero-tag',
      child: Image.asset('assets/images/my_image.png'),
    );
    ```

- **Using `PageRouteBuilder` for Custom Transitions:**
  - **Example:**
    ```dart
    Navigator.of(context).push(PageRouteBuilder(
      pageBuilder: (context, animation, secondaryAnimation) {
        return FadeTransition(
          opacity: animation,
          child: NextScreen(),
        );
      },
    ));
    ```

- **References:**
  - [Flutter Animations Documentation](https://flutter.dev/docs/development/ui/animations)

---

### **Assignments**

#### **Assignment 1: Asset Management**

- **Objective:** Add and manage images and fonts in a Flutter app.
- **Tasks:**
  1. Add local images and fonts to your project.
  2. Display an image and text using the custom font.

#### **Assignment 2: Audio and Video Integration**

- **Objective:** Integrate and play audio and video files in a Flutter app.
- **Tasks:**
  1. Add audio and video files to your project.
  2. Implement functionality to play an audio file and a video file.

#### **Assignment 3: Basic Animations**

- **Objective:** Implement basic animations using Flutter widgets.
- **Tasks:**
  1. Create an animated container that changes size and color.
  2. Implement a fade transition between two widgets.

---

### **Quiz**

1. **How do you add assets such as images and fonts to a Flutter app?**
   - a) By including them in the `pubspec.yaml` file
   - b) By placing them in the `assets` directory and defining them in `pubspec.yaml`
   - c) By importing them directly into the Dart files
   - d) By configuring them in `AndroidManifest.xml` or `Info.plist`

2. **Which package is used for playing audio in Flutter?**
   - a) video_player
   - b) audioplayers
   - c) flutter_sound
   - d) audio_player

3. **How can you display a network image in Flutter?**
   - a) `Image.asset('network-image-url')`
   - b) `Image.network('network-image-url')`
   - c) `Image.file('network-image-url')`
   - d) `Image.memory('network-image-url')`

4. **What is the purpose of the `Hero` widget in Flutter?**
   - a) To manage state transitions
   - b) To animate between two screens with shared content
   - c) To handle data persistence
   - d) To display animations

5. **How can you implement a custom page transition in Flutter?**
   - a) Using `PageRouteBuilder`
   - b) Using `AnimatedContainer`
   - c) Using `FadeTransition`
   - d) Using `Hero`

---

### **Conclusion**

Session 10 covers essential techniques for managing assets and media in Flutter, including handling images, fonts, audio, and video. It also introduces basic animations and transitions, providing a foundation for creating dynamic and engaging user interfaces. Mastery of these concepts will enhance the visual and functional quality of your Flutter applications.
