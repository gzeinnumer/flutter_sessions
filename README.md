# flutter_sessions
 
- main.dart
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sessions/preferences_service.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final session = PreferencesService();

  MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          title: const Text(''),
        ),
        body: SizedBox(
          width: double.infinity,
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            crossAxisAlignment: CrossAxisAlignment.center,
            children: [
              ElevatedButton(
                child: const Text("Save"),
                onPressed: () {
                  session.setSession("key", "data");
                },
              ),
              ElevatedButton(
                child: const Text("Get"),
                onPressed: () async {
                  final str = await session.getSession("key");
                  print("get_"+str);
                },
              )
            ],
          ),
        ),
      ),
    );
  }
}
```

- preferences_service.dart
```dart
import 'package:shared_preferences/shared_preferences.dart';

class PreferencesService {
  static const String KEY_USERNAME = "USERNAME";

  Future setSession(String key, String data) async {
    final preferences = await SharedPreferences.getInstance();
    await preferences.setString(key, data);
  }

  Future<String> getSession(String key) async {
    final preferences = await SharedPreferences.getInstance();
    final value = preferences.getString(key) ?? "";
    return value;
  }
}
```