# Lab Activity 0B: Running Your First Flutter Application

Mobile Programming, AY 2026–2027
Gwyneth S. Manalo — INF 246

| Path | Description |
|---|---|
| `manalo_mobprog/` | Flutter application (Empty Application template), created new for this activity |
| `Manalo_LabAct0B.pdf` | Submission form |

## Running the app

```
cd manalo_mobprog
flutter pub get
flutter run -d chrome
```

## Lab Activity 0B: Discussion

**Creating and running the app.** For this activity I created a separate Flutter project instead of reusing my Lab 0A project. It has its own repository, `manalo_labact0b`, and the app is named `manalo_mobprog`. I created it with the Empty Application template (the same template as VS Code's "Flutter: New Project → Empty Application", or `flutter create --empty manalo_mobprog` in the terminal), then opened `manalo_mobprog/lib/main.dart` in VS Code. It contains the template code: `main()` calls `runApp(const MainApp())`, and `MainApp` returns a `MaterialApp` whose `Scaffold` centers a `Text('Hello World!')` widget. Before running it, I ran `flutter pub get` to fetch dependencies and `flutter analyze`, which reported "No issues found!"

**Device selection.** `flutter devices` listed two targets: **macOS (desktop)** and **Chrome (web)**. No Android emulator or phone appeared, because the Android SDK is still not installed. The macOS target is listed, but `flutter doctor` still reports "Xcode installation is incomplete" and "CocoaPods not installed," so macOS and iOS builds aren't reliable yet. I chose **Chrome** as my device by running `flutter run -d chrome`. VS Code's status bar defaults to macOS, so I chose the device explicitly instead of relying on the default.

**Errors and troubleshooting.**
- `flutter doctor` still flags the Android toolchain (✗ "Unable to locate Android SDK") and Xcode (!). Neither blocks the web target, so I worked around them by choosing Chrome. Fixing them means installing Android Studio, running `flutter doctor --android-licenses`, and creating an emulator. On the Xcode side, it means running `sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer` and `sudo xcodebuild -runFirstLaunch`, then installing CocoaPods.
- `flutter pub get` warned that "4 packages have newer versions incompatible with dependency constraints." This is only informational: the locked versions work, and `flutter pub outdated` shows the details.
- When I ran the app with the `web-server` device, the page stayed blank until a debugger attached. That's expected in debug mode. Running on the Chrome device, or serving the release build (`flutter build web`), showed the app right away.

**How I verified it works.** `flutter analyze` passed with no issues, `flutter build web` finished with "✓ Built build/web", and `flutter run -d chrome` printed "Launching lib/main.dart on Chrome in debug mode..." A Chrome window opened at `localhost` and showed the "Hello World!" text centered on the screen, which matches the template's expected output.

**What I learned.** `flutter run` compiles the Dart code for whichever device you pick, launches it, and keeps a session open for hot reload (`r`) and hot restart (`R`). One codebase can run on web, desktop, or mobile, but each target needs its own platform toolchain. `flutter doctor` and `flutter devices` tell you what's actually available before you hit an error.

**Best practices for future activities.**
- Run `flutter doctor` and `flutter devices` before starting each lab.
- Run `flutter pub get` and `flutter analyze` before `flutter run`, so errors are caught early.
- Use hot reload while editing UI, and hot restart after changing app state or `main()`.
- Finish setting up an Android emulator before labs that need mobile-specific features.
- Keep `build/` out of Git (it's in `.gitignore`), and commit after each working milestone.
