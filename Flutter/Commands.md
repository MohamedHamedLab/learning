# Commands

## Running Flutter
    Flutter run
    Then enter R in the terminal window to trigger hot restart
### Argument 
**Build Flavors**
- `--debug`: A debug version. This is the default build flavor.
- `--profile`: A version specialized for performance profiling. This option does not currently support emulator targets.
- `--release`:  A release version ready for publishing to app store.
- `--flavor`: Build a custom app flavor defined by platform-specific build setup. This requires using product flavors in Android Gradle scripts and custom Xcode schemes.
- `--target-platform`: The target platform. Possible values are android-arm and android-arm64.

**Other Options**
- `--target`: specifies the main entry point file of the app.
-` --route` to specify the route to load when running the app.
- `-hot` / --not-hot: Whether hot reload should be enabled.

- `--build` / --no-build: Whether the app should be built if necessary before running it.
- `--pub` / --no-pub: Whether to run flutter packages get before running it.
 
-`-target-platform`: Specify the target platform when building the app for Android devices. Possible values are default, android-arm, and android-arm64.
 
- `--observatory-port`: Specify the port for Observatory debugger connections.

- `--start-paused`: Make the app to start in a paused mode and wait for a debugger to connect.
 
- `--trace-startup`: Start tracing.
 
-` --enable-software-rendering`: Enable rendering using Skia.
 
- `--skia-deterministic-rendering`: Provide 100% deterministic Skia rendering when used with --enable-software-rendering.
 
- `--trace-skia`: Enable tracing of Skia code.

## Fixing Configuration Issues
    `flutter doctor`

##  Upgrade the SDK
   ` flutter upgrade`

## Creating Flutter Projects
flutter create **Project Type**

### Project types
 -  **app** : A Flutter application. This is the default type.  
 `flutter create -t app my_app`
 -  **package** : A sharable Flutter project that contains modular Dart code.
  `flutter create -t package my_package`
 -  **plugin** : A sharable Flutter project that contains platform-specific code for Android and iOS.
  `flutter create -t plugin my_plugin`

## Running Flutter Tests
`flutter test`

### Filter the Tests to Run

- `flutter test --name="smoke\d+`
- `flutter test --plain-name=smoke`
- `flutter test --name="smoke.*" --plain-name=test`

## Managing Emulators
### Manage different emulators used by Flutter SDK
- `flutter emulators`
### To start a simulator
- `flutter emulators --launch Nexus`
- `flutter emulators --create --name Pixel`

## Taking Screenshots
- `flutter screenshot`
- `flutter screenshot -o ~/myapp/screenshots/home.png`

## Attaching to Running Apps
-`flutter attach`
- `flutter attach --debug-port 10010`

## Tracing Running Flutter Apps
- `flutter trace`
- `flutter trace --debug-port=51240`
- `flutter trace --start`
- `flutter trace --stop`

## Formatting Source Code
- `flutter format`
### Argument
- `-n, --dry-run`: Just show which files would be modified without actually modifying them.
- `--set-exit-if-changed`: Return exit code 1 if there are any formatting changes made by this command.
- -m, --machine: Set the output format to JSON.

## Cleaning Build Files of Flutter App
- `flutter clean`

## Managing Flutter SDK Cache
- `flutter precache`
- `-a  --all-platforms` : to specify whether artifacts for all platforms should be downloaded

 