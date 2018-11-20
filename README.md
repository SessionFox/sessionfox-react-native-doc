### Getting started

`$ npm install sessionfox-rn-sdk --save`

### Mostly automatic installation

`$ react-native link sessionfox-rn-sdk`

### Including library in Android project

1. In the build.gradle inside your android folder, add following inside allprojects.repositories
```
allprojects {
    repositories {
        google()
        jcenter()
        maven {
            url "https://mymavenrepo.com/repo/PENxspKoeuoFCKp9veSD/"
        }
    }
}
```
Note: If your gradle version is below 3.0.0, you will have to upgrade gradle inside the above file to 3.0.0 version in your <Project>and sync project in Android Studio.

2. Add the line to your android/app/src/main/AndroidManifest.xml
``` 
<meta-data android:name="SESSION_FOX_API_KEY" android:value="<your-api-key>" />
```
Please replace with api key got from registering on the website.

3. Usage
```javascript
import SessionFoxRN from 'sessionfox-rn-sdk';

// Call the init function in your App.js render()
SessionFoxRN.init();

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
  

