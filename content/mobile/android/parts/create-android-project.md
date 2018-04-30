## Create Android Project

### Android Studio

To add rave to your project is seamless and very simple, takes less than 5 minutes on the average. You don’t have to clone any repo or install any external file, simple add this maven repository to your project level build.gradle file (Project Module):

    allprojects {
        repositories {
           .....
            maven { url 'https://jitpack.io' }
        }
    }

Then click sync. Next add this dependency to your app level build.gradle file (Application Module):
    
    compile 'com.github.Flutterwave:rave-android:1.0.16'
    
Again click the visible sync button and BOOOOM!!! you have rave installed. 

### Permissions

Now that you have rave, lets add it’s required permissions, this library requires the `READ_PHONE_STATE` to get the build number for fraud detection and flagging as recommended [here](https://developer.android.com/training/articles/user-data-ids.html#i_abuse_detection_detecting_high_value_stolen_credentials).
So open your `AndroidManifest.xml` file and add these permissions:

```
<uses-permission android:name="android.permission.READ_PHONE_STATE" />

<uses-permission android:name="android.Manifest.permission.READ_PHONE_STATE" />
```