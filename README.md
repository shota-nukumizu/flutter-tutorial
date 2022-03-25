# Twitter Clone for Flutter and Firebase

FlutterとFirebaseで開発したTwitterのクローンアプリ。

# ホームページや認証ページの作成

その前に、前提として`lib/main.dart`を以下のように書き換える

```dart
import 'package:flutter/material.dart';
import 'package:turorial/Screens/WelcomeScreen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  Widget getScreenId() {
    return StreamBuilder(builder: (BuildContext context, snapshot) {
      return WelcomeScreen();
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData.light(),
      home: getScreenId(),
    );
  }
}
```

## ホームページ

`lib/Screens/WelcomeScreen.dart`

```dart
import 'package:flutter/material.dart';
import 'package:turorial/Widgets/RoundedButton.dart';

class WelcomeScreen extends StatefulWidget {
  @override
  _WelcomeScreenState createState() => _WelcomeScreenState();
}

class _WelcomeScreenState extends State<WelcomeScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        body: SafeArea(
            child: Padding(
                padding: const EdgeInsets.symmetric(horizontal: 20),
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    Column(
                      children: [
                        SizedBox(
                          width: MediaQuery.of(context).size.width,
                        ),
                        Image.asset(
                          'assets/logo.png',
                          height: 200,
                          width: 200,
                        ),
                        Text(
                          'See what is happening in the world right now.',
                          style: TextStyle(
                              fontSize: 40, fontWeight: FontWeight.bold),
                        ),
                      ],
                    ),
                    Column(
                      children: [
                        RoundedButton(
                            btnText: 'LOG IN',
                            onBtnPressed: () {
                              Navigator.push(
                                  context,
                                  MaterialPageRoute(
                                      builder: (context) => LoginScreen()));
                            }),
                        SizedBox(height: 30),
                        RoundedButton(
                            btnText: 'Create account',
                            onBtnPressed: () {
                              Navigator.push(
                                  context,
                                  MaterialPageRoute(
                                      builder: (context) =>
                                          RegistrationScreen()));
                            }),
                      ],
                    )
                  ],
                ))));
  }
}

```

## ボタン作成

`lib/Widgets/RoundedButton.dart`

```dart
import 'package:flutter/material.dart';

class RoundedButton extends StatelessWidget {
  final String btnText;
  final Function onBtnPressed;

  const RoundedButton({Key key, this.btnText, this.onBtnPressed})
      : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Material(
        elevation: 5,
        color: Color(0xff00acee),
        borderRadius: BorderRadius.circular(25),
        child: MaterialButton(
          onPressed: onBtnPressed,
          minWidth: 320,
          height: 60,
          child: Text(
            btnText,
            style: TextStyle(color: Colors.white, fontSize: 20),
          ),
        ));
  }
}
```