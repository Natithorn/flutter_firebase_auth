# flutter_firebase_auth

This project demonstrates how to integrate Firebase Authentication into a Flutter application. It includes features such as user registration, login, and logout using Firebase's authentication services.

## Installation

1. Create Firebase project at [firebase console](https://console.firebase.google.com/)
2. Install Firebase using command


   ```
   flutter pub add firebase_auth
   ```

   ```
   dart pub global activate flutterfire_cli
   ```

3. Link a project to Firebase project
   ```
   flutterfire configure --project=[FIREBASE-PROJECT-ID]
   ```
4. Enable authentication method with email/password in Firebase project

## Initialize firebase to app

to use Firebase in project we add this command to main()

```dart
import 'package:firebase_core/firebase_core.dart';
import 'package:flutter/material.dart';
import 'package:flutter_firebase_auth/firebase_options.dart';
import 'login_screen.dart';

void main() async {
WidgetsFlutterBinding.ensureInitialized();
await Firebase.initializeApp(
 options: DefaultFirebaseOptions.currentPlatform,
);
runApp(const MainApp());
}

class MainApp extends StatelessWidget {
const MainApp({Key? key}) : super(key: key);

@override
Widget build(BuildContext context) {
 return MaterialApp(
   title: 'Flutter Firebase Authentication',
   theme: ThemeData(
     primarySwatch: Colors.blue,
   ),
   home: LoginScreen(),
 );
}
}
```

## Create new account

use `createUserWithEmailAndPassword()` to create new user with email and password This can be done in `create_account_screen.dart`.

```dart
final FirebaseAuth _auth = FirebaseAuth.instance;

UserCredential userCredential = await _auth.createUserWithEmailAndPassword(
  email: email,
  password: password,
);
```

## User Login 

Use `signInWithEmailAndPassword()` to log in a user with email and password. This can be done in `login_screen.dart`.

```dart
final FirebaseAuth _auth = FirebaseAuth.instance;

UserCredential userCredential = await _auth.signInWithEmailAndPassword(
  email: email,
  password: password,
); 
```


## Logging Out

To log the user out, use `signOut()`.

```dart
await _auth.signOut();
```

## Screens
`login_screen.dart` : Screen for users to log in with email and password.
`create_account_screen.dart` : Screen for users to create a new account by providing email and password.
`home_screen.dart` : Main screen that users will see once logged in. Accessible only after authentication.

## Running the App
Once you've set up Firebase and completed the required configurations, run the app using:
  ```
  flutter run
  ```