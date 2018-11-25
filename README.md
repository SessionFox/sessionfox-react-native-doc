### Getting started

```
$ npm install sessionfox-rn-sdk --save
$ react-native link sessionfox-rn-sdk
```

### Including library in Android project

#### Step 1
In the build.gradle inside your android folder, add following inside allprojects.repositories
```
allprojects {
    repositories {
        google()
        jcenter()
        maven {
            url "https://mymavenrepo.com/repo/EpCerWf2f0TbbXSSpgLb/"
        }
    }
}
```
Note: If your gradle version is below 3.0.0, you will have to upgrade gradle. Inside the above file change version to 3.2.0 in your Project and sync project in Android Studio. Once the sync is complete, you can ignore the other errors in android studio and move on to the next step.

In the build.gradle inside android/app folder, please add the below lines, so that it is java 1.8 compatible
```java
android {
    compileOptions {
        targetCompatibility 1.8
        sourceCompatibility 1.8
    }
}
```

#### Step 2
Add the line to your android/app/src/main/AndroidManifest.xml
```
<meta-data android:name="SESSION_FOX_API_KEY" android:value="<your-api-key>" />
```
Please replace with api key got from registering on the website.

#### Step 3
In the Main application class within android/app folder, import these packages if not already present
```java
import com.sessionfoxrn.SessionFoxRNPackage;
import com.sessionfox.sdk.SessionFox;
```
Make sure that your Application class implements the `ReactApplication` interface and `getPackages()` method has `new SessionFoxRNPackage()` added to it.

Example:

```java
@Override
protected List<ReactPackage> getPackages() {
  return Arrays.<ReactPackage>asList(
      new SomeOtherPackage(),
      new SessionFoxRNPackage()
  );
}
```
Once this is done, in the `onCreate()` method of the application, add ```SessionFox.init()```.

Example:
```java
@Override
public void onCreate() {
  super.onCreate();
  SessionFox.init(this);
}
```

Thats it! you are now ready to use SessionFox

### Usage
```javascript
// Tag screen name visited
SessionFoxRN.tagScreenName('com.sample.CheckoutScreen');

// Send custom user meta data
SessionFoxRN.setUser({
  name: 'Mark',
  rollnum: '25',
});

// Send custom event
SessionFoxRN.sendEvent('purchase',{
  amount: '30',
  card: 'hdfc',
});
```

### Using Proguard with the SessionFox SDK
If your app is proguarded, you may notice some errors at the time of making a release apk. If this happens, add the following lines to the end of your proguard-rules.pro
```
# Class names are needed in reflection
-keepnames class com.amazonaws.**
-keepnames class com.amazon.**
# Request handlers defined in request.handlers
-keep class com.amazonaws.services.**.*Handler
# The following are referenced but aren't required to run
-dontwarn com.fasterxml.jackson.**
-dontwarn org.apache.commons.logging.**
# Android 6.0 release removes support for the Apache HTTP client
-dontwarn org.apache.http.**
# The SDK has several references of Apache HTTP client
-dontwarn com.amazonaws.http.**
-dontwarn com.amazonaws.metrics.**
```
