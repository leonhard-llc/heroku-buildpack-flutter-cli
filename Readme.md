# heroku-buildpack-flutter-cli

Use this to run Dart programs on Heroku that share code with a Flutter app.

The buildpack compiles all `**/bin/*.dart` files into
statically-linked Linux amd64 binaries with filenames ending in `.exe`.
For example, it compiles `dart/bin/test_bots.dart` to `dart/bin/test_bots.exe`.

This buildpack does not compile Flutter apps.

## Specify Flutter Version
Specify the Flutter version by setting config variables `FLUTTER_VERSION` and `FLUTTER_SHA256`.
You can find Flutter builds at:

<https://docs.flutter.dev/development/tools/sdk/releases?tab=linux>

Flutter team doesn't care to supply SHA-256 digests for you,
so you must download the massive archive and calculate the digest yourself.

Example values:
- `FLUTTER_VERSION=2.10.2`
- `FLUTTER_SHA256=03de160d1c30730a248cb5e168ec2de60f883d7e365e6cf57b27786e85436c0f`

Supports only stable Flutter releases.
Does *not* use the latest version of Flutter when the version is unspecified.

## Add to Heroku App
Add it to your Heroku app with:
```
$ heroku buildpacks:add --app=${APP_NAME} --index 1 https://github.com/leonhard-llc/heroku-buildpack-flutter-cli.git
```

## Includes Asset Files
When building a binary in a directory,
the buildpack finds all non-dart files under the directory and includes them in the Heroku slug.

This works around Dart Team's inexplicable abandonment
of the [resource](https://pub.dev/packages/resource) package
which allowed embedding files into binaries.
