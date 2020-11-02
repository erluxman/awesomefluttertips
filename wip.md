<!-- ---
title: Flutter Tips 85-91
date: '2020-07-12'
spoiler: 14th batch of 7 tips and tricks on the series 100DaysOfFlutter.
---

### #99 Bottom Sheet(modal_bottom_sheet)

### #98 Flutter TTS

### #98 avatar_glow 1.2.0

### #98 animate_do 1.7.2
### workmanager

### zefyr
### oktoast 2.3.2
### feature_discovery
### settings_ui 0.3.0 (Building setting UI that will reflect corresponding platform)
### flutter_neumorphic 3.0.1
### #98 awesome_dialog
### #98 after_layout
### #flutter_email_sender
### #flutter_staggered_animations
### #flutter_native_splash

## #97 `rate_my_app`

We ask users to **`rate our app`**, but doing it effeciently without irritating users is a difficult job.

Instead of making manual popups and logic, `rate_my_app` makes it easy to properly show **`rate our app`** properly with requirements to show dialog like:

- Minimum number of days & launches from app is installed.
- Minimum number of days & launches between two popups.
- iOS in-app rating dialog.
  
1. Add dependency.

```yml
dependencies:
  rate_my_app: ^0.6.1+6
```

2. Add following to iOS/Runner/Info.plist

```xml
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>itms</string>
</array>
```

3. Initialze

```dart
  WidgetsFlutterBinding.ensureInitialized();
```

## #95 Flutter hooks(`flutter_hooks`)

- Do you think `StatefulWidget` is too verbose?
- Do you want to reuse it's init() and dispose() method?
- Do you want AnimationControoler,TextInputController, StreamController etc's creation and dispose() taken care of automatically?
- Do you want to reuse logic inside StatefulWidget in different widgets?
  
  Use `flutter_hooks`.

### Without `flutter_hooks`

```

## #95 https://pub.dev/packages/sa_stateless_animation

## #94 EZ simple_animations: ^2.2.1

## #94 EZ animations

## #95 Riverpod Flutter

## #Day86 Difference between pump(),pumpWidget() and pumpAndSettle()

## #Day86 Flutter-Neumorphic

If you need advanced library for flutter with lots of Neumorphic features, use this package.

https://github.com/Idean/Flutter-Neumorphic

## #Publish a library

https://stackoverflow.com/questions/51536756/flutter-listview-jumps-to-top

https://blog.codemagic.io/how-to-improve-the-performance-of-your-flutter-app./

https://blog.codemagic.io/flutter-matrix4-perspective-transformations/ -->