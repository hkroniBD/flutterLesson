In Android development, you specify permissions in the `AndroidManifest.xml` file to grant your app access to various resources or functionalities. Here’s a list of common permissions codes that you might need to add to your `AndroidManifest.xml` file:

### **Basic Permissions**

| Permission Code                               | Description                                                                                       |
|-----------------------------------------------|---------------------------------------------------------------------------------------------------|
| `<uses-permission android:name="android.permission.INTERNET"/>` | Allows access to the internet.                                                                  |
| `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` | Allows the app to check the network state.                                                     |
| `<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>` | Allows the app to access information about Wi-Fi networks.                                       |
| `<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>` | Allows the app to write to external storage.                                                     |
| `<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>` | Allows the app to read from external storage.                                                     |
| `<uses-permission android:name="android.permission.CAMERA"/>` | Allows the app to use the device’s camera.                                                       |
| `<uses-permission android:name="android.permission.RECORD_AUDIO"/>` | Allows the app to record audio.                                                                   |
| `<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>` | Allows the app to access precise location from GPS.                                                |
| `<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>` | Allows the app to access approximate location from network sources.                                |
| `<uses-permission android:name="android.permission.SEND_SMS"/>` | Allows the app to send SMS messages.                                                             |
| `<uses-permission android:name="android.permission.RECEIVE_SMS"/>` | Allows the app to receive SMS messages.                                                          |

### **Advanced Permissions**

| Permission Code                               | Description                                                                                       |
|-----------------------------------------------|---------------------------------------------------------------------------------------------------|
| `<uses-permission android:name="android.permission.READ_PHONE_STATE"/>` | Allows the app to access the phone’s state, such as the phone number.                             |
| `<uses-permission android:name="android.permission.CALL_PHONE"/>` | Allows the app to make phone calls directly.                                                      |
| `<uses-permission android:name="android.permission.READ_CONTACTS"/>` | Allows the app to read the user’s contacts.                                                       |
| `<uses-permission android:name="android.permission.WRITE_CONTACTS"/>` | Allows the app to write to the user’s contacts.                                                   |
| `<uses-permission android:name="android.permission.GET_ACCOUNTS"/>` | Allows the app to access the list of accounts in the Accounts Service.                           |
| `<uses-permission android:name="android.permission.USE_FINGERPRINT"/>` | Allows the app to use fingerprint hardware.                                                       |
| `<uses-permission android:name="android.permission.BLUETOOTH"/>` | Allows the app to use Bluetooth features.                                                         |
| `<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>` | Allows the app to manage Bluetooth settings.                                                     |
| `<uses-permission android:name="android.permission.NFC"/>` | Allows the app to use NFC features.                                                               |
| `<uses-permission android:name="android.permission.VIBRATE"/>` | Allows the app to use the device’s vibration feature.                                              |

### **Background & Sync**

| Permission Code                               | Description                                                                                       |
|-----------------------------------------------|---------------------------------------------------------------------------------------------------|
| `<uses-permission android:name="android.permission.WAKE_LOCK"/>` | Allows the app to prevent the phone from going to sleep.                                           |
| `<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>` | Allows the app to receive the `BOOT_COMPLETED` broadcast after the device finishes booting.       |
| `<uses-permission android:name="android.permission.AUTHENTICATE_ACCOUNTS"/>` | Allows the app to create accounts and set passwords.                                               |
| `<uses-permission android:name="android.permission.READ_SYNC_SETTINGS"/>` | Allows the app to read the synchronization settings.                                               |
| `<uses-permission android:name="android.permission.WRITE_SYNC_SETTINGS"/>` | Allows the app to write the synchronization settings.                                              |

### **Others**

| Permission Code                               | Description                                                                                       |
|-----------------------------------------------|---------------------------------------------------------------------------------------------------|
| `<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW"/>` | Allows the app to display windows over other apps.                                                |
| `<uses-permission android:name="android.permission.REQUEST_INSTALL_PACKAGES"/>` | Allows the app to request the installation of packages.                                            |
| `<uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/>` | Allows the app to change network connectivity state.                                                |

When adding permissions to your `AndroidManifest.xml`, make sure to only request those that are necessary for your app’s functionality. For sensitive permissions, such as location or camera access, you should also handle runtime permission requests as required by newer versions of Android.
