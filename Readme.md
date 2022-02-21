# heroku-buildpack-flutter-cli

This buildpack compiles Dart CLI programs that depend on Flutter libraries.

You can use it to run Dart programs on Heroku that share code with a Flutter app.

The buildpack compiles all `**/bin/*.dart` files into binaries.
For example, it compiles `dart/bin/test_bots.dart` into
a statically-linked Linux amd64 binary called `dart/bin/test_bots.exe`.

This buildpack does not compile Flutter apps.
