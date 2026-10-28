# SwiftHome 2: minimal, offline Android TV launcher

* One Java file, zero libraries, NO permissions (no INTERNET). It cannot send data anywhere.
* Does not disable, uninstall or modify other apps. Your stock launcher stays installed.

## Features
App grid with banners and focus animation, clock, Network / Apps / Settings pills,
tiles per row 4-7, motion on/off, move apps left/right/first, hide/show apps,
app info, auto-refresh when apps are installed or removed.
Hold OK on the Settings pill = Launcher settings. Hold OK on an app = app menu.

## Get the APK without Android Studio (GitHub Actions)
1. Create a free GitHub account and a NEW PRIVATE repository.
2. Upload every file in this folder (including the hidden .github folder) to it.
3. Open the Actions tab > "Build APK" > wait for the green tick (about 3 minutes).
4. Download the artifact "SwiftHome-apk", unzip it to get app-debug.apk.

## Or build locally
Android Studio: File > Open this folder > Build > Build APK(s).

## Install on the TV (PowerShell, TV connected via adb)
adb install -r app-debug.apk
adb shell cmd package set-home-activity com.example.swifthome/.MainActivity

## Undo
adb shell cmd package set-home-activity com.google.android.apps.tv.launcherx/com.google.android.apps.tv.launcherx.home.HomeActivity
adb uninstall com.example.swifthome

## Clock screensaver
Settings > Device Preferences > Screen saver > SwiftHome Clock, or via adb:
adb shell settings put secure screensaver_components com.example.swifthome/.ClockDream
adb shell settings put secure screensaver_enabled 1

## Added in v3
* Assistant button: opens the TV's own Gemini / Google Assistant (no data passes through SwiftHome).
* Inputs button: lists HDMI/AV inputs and switches to the one you pick.
* Themes: Midnight, Purple, Forest, Black (Launcher settings).
* Subscription tracker: hold OK on an app > "Subscription end date" (dd/mm/yyyy).
  Tiles show days left, turn orange at 7 days and red when expired; a notice appears in the top bar.
  Dates are typed by you and stored only on the TV. Other apps' real subscription data is not readable.
