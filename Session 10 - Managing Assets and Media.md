### **Lecture Notes: Session 10 - Managing Assets and Media**

---

#### **1. Managing Assets (Images, Fonts)**

**a. Managing Images:**

- **Definition:** Assets are files bundled with your app that can be used for various purposes, such as images, fonts, and other resources.

- **Adding Images:**
  - **Step 1: Add Images to Asset Directory:**
    Place your images in the `assets` directory of your project. Create this directory if it doesn't exist.

    ```plaintext
    my_app/
    ├── assets/
    │   ├── images/
    │   │   ├── logo.png
    │   │   ├── background.jpg
    ├── lib/
    ├── pubspec.yaml
    ```

  - **Step 2: Register Assets in `pubspec.yaml`:**

    ```yaml
    flutter:
      assets:
        - assets/images/logo.png
        - assets/images/background.jpg
    ```

  - **Step 3: Use Images in Widgets:**

    ```dart
    Image.asset('assets/images/logo.png');
    ```

**b. Managing Fonts:**

- **Adding Custom Fonts:**
  - **Step 1: Add Fonts to Asset Directory:**
    Place your font files (e.g., `.ttf`, `.otf`) in a `fonts` directory under `assets`.

    ```plaintext
    my_app/
    ├── assets/
    │   ├── fonts/
    │   │   ├── OpenSans-Regular.ttf
    │   │   ├── OpenSans-Bold.ttf
    ├── lib/
    ├── pubspec.yaml
    ```

  - **Step 2: Register Fonts in `pubspec.yaml`:**

    ```yaml
    flutter:
      fonts:
        - family: OpenSans
          fonts:
            - asset: assets/fonts/OpenSans-Regular.ttf
            - asset: assets/fonts/OpenSans-Bold.ttf
              weight: 700
    ```

  - **Step 3: Use Fonts in Text Styles:**

    ```dart
    Text(
      'Custom Font Text',
      style: TextStyle(
        fontFamily: 'OpenSans',
        fontWeight: FontWeight.bold,
      ),
    );
    ```

---

#### **2. Adding Audio and Video to Your App**

**a. Adding Audio:**

- **Adding Audio Files:**
  - **Step 1: Add Audio Files to Asset Directory:**
    Place your audio files (e.g., `.mp3`, `.wav`) in an `audio` directory under `assets`.

    ```plaintext
    my_app/
    ├── assets/
    │   ├── audio/
    │   │   ├── background_music.mp3
    ├── lib/
    ├── pubspec.yaml
    ```

  - **Step 2: Register Audio Assets in `pubspec.yaml`:**

    ```yaml
    flutter:
      assets:
        - assets/audio/background_music.mp3
    ```

  - **Step 3: Play Audio:**

    Use a package like `audioplayers` to play audio.

    ```dart
    import 'package:audioplayers/audioplayers.dart';

    AudioPlayer audioPlayer = AudioPlayer();
    audioPlayer.play('assets/audio/background_music.mp3');
    ```

**b. Adding Video:**

- **Adding Video Files:**
  - **Step 1: Add Video Files to Asset Directory:**
    Place your video files (e.g., `.mp4`) in a `videos` directory under `assets`.

    ```plaintext
    my_app/
    ├── assets/
    │   ├── videos/
    │   │   ├── introduction.mp4
    ├── lib/
    ├── pubspec.yaml
    ```

  - **Step 2: Register Video Assets in `pubspec.yaml`:**

    ```yaml
    flutter:
      assets:
        - assets/videos/introduction.mp4
    ```

  - **Step 3: Play Video:**

    Use a package like `video_player` to play video.

    ```dart
    import 'package:video_player/video_player.dart';

    class VideoScreen extends StatefulWidget {
      @override
      _VideoScreenState createState() => _VideoScreenState();
    }

    class _VideoScreenState extends State<VideoScreen> {
      late VideoPlayerController _controller;

      @override
      void initState() {
        super.initState();
        _controller = VideoPlayerController.asset('assets/videos/introduction.mp4')
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

      @override
      void dispose() {
        super.dispose();
        _controller.dispose();
      }
    }
    ```

---

#### **3. Using the Image Widget for Local and Network Images**

**a. Local Images:**

- **Definition:** Local images are stored within your app's assets directory.

- **Usage:**

  ```dart
  Image.asset('assets/images/local_image.png');
  ```

**b. Network Images:**

- **Definition:** Network images are loaded from a URL.

- **Usage:**

  ```dart
  Image.network('https://example.com/image.png');
  ```

**c. Common Properties:**

- **width, height:** Specify the size of the image.
- **fit:** Define how the image should be resized to fit its container. Options include `BoxFit.cover`, `BoxFit.fill`, etc.
- **alignment:** Align the image within its container.

  ```dart
  Image.asset(
    'assets/images/local_image.png',
    width: 100,
    height: 100,
    fit: BoxFit.cover,
  );
  ```

---

#### **4. Introduction to Animations and Transitions**

**a. Basic Animations:**

- **Definition:** Animations add visual interest and feedback by changing widget properties over time.

- **Example:**

  ```dart
  class AnimatedContainerExample extends StatefulWidget {
    @override
    _AnimatedContainerExampleState createState() => _AnimatedContainerExampleState();
  }

  class _AnimatedContainerExampleState extends State<AnimatedContainerExample> {
    double _width = 100.0;
    double _height = 100.0;
    Color _color = Colors.blue;

    void _changeProperties() {
      setState(() {
        _width = _width == 100.0 ? 200.0 : 100.0;
        _height = _height == 100.0 ? 200.0 : 100.0;
        _color = _color == Colors.blue ? Colors.red : Colors.blue;
      });
    }

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(title: Text('Animated Container')),
        body: Center(
          child: AnimatedContainer(
            width: _width,
            height: _height,
            color: _color,
            duration: Duration(seconds: 1),
            child: Center(child: Text('Tap to Animate')),
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: _changeProperties,
          child: Icon(Icons.play_arrow),
        ),
      );
    }
  }
  ```

**b. Transitions:**

- **Definition:** Transitions animate changes between routes or widgets, providing a smoother visual experience.

- **Page Route Transitions:**

  - **Fade Transition:**

    ```dart
    class FadeTransitionPage extends PageRouteBuilder {
      FadeTransitionPage()
        : super(
            pageBuilder: (context, animation, secondaryAnimation) => YourScreen(),
            transitionsBuilder: (context, animation, secondaryAnimation, child) {
              const begin = 0.0;
              const end = 1.0;
              const curve = Curves.easeIn;

              var tween = Tween(begin: begin, end: end);
              var opacityAnimation = animation.drive(tween);
              return FadeTransition(opacity: opacityAnimation, child: child);
            },
          );
    }
    ```

  - **Slide Transition:**

    ```dart
    class SlideTransitionPage extends PageRouteBuilder {
      SlideTransitionPage()
        : super(
            pageBuilder: (context, animation, secondaryAnimation) => YourScreen(),
            transitionsBuilder: (context, animation, secondaryAnimation, child) {
              const begin = Offset(1.0, 0.0);
              const end = Offset.zero;
              const curve = Curves.easeIn;

              var tween = Tween(begin: begin, end: end);
              var offsetAnimation = animation.drive(tween);
              return SlideTransition(position: offsetAnimation, child: child);
            },
          );
    }
    ```

---

### **Conclusion**

In this session, we explored managing assets like images and fonts, adding audio and video to your app, utilizing the `Image` widget for local and network images, and introduced animations and transitions. Mastery of these concepts allows you to create rich and interactive user experiences in your Flutter applications.
