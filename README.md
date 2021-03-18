# FirebasePhoneAuth_RN

### Firebase Phone Authentication in Android Using  React Native

# Installation Firebase

## Install & setup the app module
yarn add @react-native-firebase/app

## Install the authentication module
yarn add @react-native-firebase/auth

## If you're developing your app using iOS, run this command
cd ios/ && pod install

## Setup for Android

1) In your project Go To Tools -> Firebase -> Authentication -> Authentication Usign Sign In
  - Connect your app with Firebase

2) In Firebase Console Select your project and go to your project setting
  - Add SHA-1 and SHA-256 key in Firebase Project Setting.
  - Download Google-Service.json file and Add into your project in app folder.

3) In your project Go To Tools -> Firebase -> Authentication -> Authentication Usign Sign In
  - Add the Firebase Authentication SDK to your app.(In Android Studio)  
  - Select Target Module - App level build.gradle file
  - Accept Changes

## Open https://console.cloud.google.com/
  - Login same as account of Firebase
  - Select your project
  - Search Android Device Verification API
  - Enable Android Device Verification API
  - Go to MANAGE -> Credential -> Create Credential -> API Key -> Create and Copy it.

## How to generate Debug SHA-1 and SHA-256 key
- Open Terminal and go to your Project Path

**Enter below command:**
- cd android
- keytool -list -v -alias androiddebugkey -keystore "/Users/username/.android/debug.keystore" -storepass android -keypass android
- ./gradlew signingReport

**Result** 
Task :app:signingReport
Variant: releaseUnitTest
Config: debug
Store: /Users/dhavaljasoliya/Documents/Vaishali/ERPORATARO_RN/android/app/debug.keystore
Alias: androiddebugkey
MD5: 20:F4:61:48:B7:2D:8E:5E:5C:A2:3D:37:A4:F4:14:90
SHA1: 5E:8F:16:06:2E:A3:CD:2C:4A:0D:54:78:76:BA:A6:F3:8C:AB:F6:25
SHA-256: FA:C6:17:45:DC:09:03:78:6F:B9:ED:E6:2A:96:2B:39:9F:73:48:F0:BB:6F:89:9B:83:32:66:75:91:03:3B:9C
Valid until: Wednesday, 1 May 2052

**copy SHA1 and SHA-256 key and paste in to Firebase console -> Select Project -> Select APP -> Select Project Setting -> Add Fingerprint -> paste key -> save it.**

## SIGN IN
The module provides a signInWithPhoneNumber method which accepts a phone number. Firebase sends an SMS message to the user with a code, which they must then confirm. The signInWithPhoneNumber method returns a confirmation method which accepts a code. Based on whether the code is correct for the device, the method rejects or resolves.

**For More Info**
https://rnfirebase.io/auth/phone-auth
https://www.section.io/engineering-education/react-native-firebase-phone-authentication/

Add in your APP.js file
```
var firebaseConfig = {
    apiKey: "AIzaSyBEFAGXiMslrfRzPHVnbuaPj_vU_jbawiY",
    authDomain: "fcmnotificationdemo-36e37.firebaseapp.com",
    databaseURL: "https://fcmnotificationdemo-36e37.firebaseio.com",
    projectId: "fcmnotificationdemo-36e37",
    storageBucket: "fcmnotificationdemo-36e37.appspot.com",
    messagingSenderId: "sender-id",
    appId: "1:265701615074:android:72a5282ff943a7e02e05bb",
    measurementId: "G-measurement-id",
  };
  
  this.state =
        {
            isLoading: false,
            confirm: ''
        }
        
        async signInWithPhoneNumber(phoneNumber) {
        if (!firebase.apps.length) {
            firebase.initializeApp(firebaseConfig);
         }else {
            firebase.app();
           // if already initialized, use that one
         }
        
        const confirmation = await auth().signInWithPhoneNumber(phoneNumber);
        this.setState({confirm: confirmation});
      }
      
      
      {
          !this.state.confirm ? 
          <Button
              title="Phone Number Sign In"
              onPress={() => this.signInWithPhoneNumber('+91 987654321')}
          /> : 
          <Button
          title="UserLogged In Click for Logout"
          onPress={() => this.setState({confirm: ''})}
          />
      }
                
                ```
