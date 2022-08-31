# Flutter OS (Android Wear OS app)

### **Medium article ["Flutter: Building Wear OS app"](https://medium.com/flutter-community/flutter-building-wearos-app-fedf0f06d1b4).**

## Plugin

The plugin used in this project is ["wear"](https://pub.dev/packages/wear).

Add this to your package's pubspec.yaml file to use wear:

```yaml
dependencies:
  wear: ^0.0.3
```

Import using:

```dart
import 'package:wear/wear.dart';
```

# Set Up (Important)

I am again stating the set up process below (not recommended):

## App Gradle File

Change the min SDK version to API 23:

```
minSdkVersion 23
```

Then, add the following dependencies to the Android Gradle file for the app:

```
dependencies {
    // Wear libraries
    implementation 'com.android.support:wear:27.1.1'
    implementation 'com.google.android.support:wearable:2.3.0'
    compileOnly 'com.google.android.wearable:wearable:2.3.0'
}
```

## Manifest File

Add the following to your AndroidManifest.xml file:

```xml
<!-- Required for ambient mode support -->
<uses-permission android:name="android.permission.WAKE_LOCK" />

<!-- Flags the app as a Wear app -->
<uses-feature android:name="android.hardware.type.watch" />

<!-- Flags that the app doesn't require a companion phone app -->
<application>
<meta-data
    android:name="com.google.android.wearable.standalone"
    android:value="true" />
</application>
```

## Update Android's MainActivity

The ambient mode widget needs some initialization in Android's MainActivity code. Update your code as follows:

```kotlin
class MainActivity: FlutterActivity(), AmbientMode.AmbientCallbackProvider {
  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    GeneratedPluginRegistrant.registerWith(this)

    // Wire up the activity for ambient callbacks
    AmbientMode.attachAmbientSupport(this)
  }

  override fun getAmbientCallback(): AmbientMode.AmbientCallback {
    return FlutterAmbientCallback(getChannel(flutterView))
  }
}
```
