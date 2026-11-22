# Step 2 · Build and install 4.0.0

Build 4.0.0 with the same method you used the first time. The wiki lists four:

| Original method | What to do for 4.0.0 |
| --- | --- |
| Browser, **AAPS Builder** | In your private repository (usually `my-aaps`), open the *Build AAPS* page, pick version 4.0.0 and download the app from GitHub. There is no fork to sync. |
| Browser, **fork + preparation file** | You run the **AAPS-CI** workflow in your fork (`AndroidAPS` in your account) and the APK lands in your Google Drive. Follow the official page [Update with a browser (fork)](https://androidaps.readthedocs.io/en/latest/Maintenance/UpdateBrowserBuild.html). |
| **Android Studio** | Follow the official page [Update with Android Studio](https://androidaps.readthedocs.io/en/latest/Maintenance/UpdateComputerBuild.html). |
| **Command line** | Use the same instructions as your original command-line build, but pull the new changes with `git`. |

In the code, tag `4.0.0` points to commit `f77abd9b82` (merge of PR #5448) and declares `appVersion = "4.0.0"`. The build uses Java 21 (`JavaVersion.VERSION_21`) and Gradle 9.8.2; if you build locally and get a Gradle JVM error, make sure Android Studio uses a JDK 21.

## Signing: the step that causes most trouble

Sign 4.0.0 with **the same keystore and the same alias** as the installed version. Android only allows installing over the old app when the signature matches, and that is the only way to keep the database and settings. If it does not match, Android forces an uninstall, which deletes everything in the app.

## Installing

- Install the new APK **over** the current version. **Do not uninstall** first. The wiki puts it plainly: to keep your history, always update, never uninstall and reinstall.
- If you use a watch, update the Wear app too, with the APK from the same build. The watch app was rewritten; see the wiki's "AAPS for Wear OS" page if it does not connect.

## Android developer verification

Google is introducing a check that, on most phones, blocks installing apps from unregistered developers, including from an APK file like the AAPS one. According to the official page [Android developer verification](https://androidaps.readthedocs.io/en/latest/SettingUpAaps/TransferringAndInstallingAaps.html#android-developer-verification):

- Building AAPS does not change, and neither does your keystore.
- Your installed app keeps running: the check only happens when you install or update.
- From 2026-09-30 it is enforced in Brazil, Indonesia, Singapore and Thailand. Google states that this first step does not cover installing an APK file directly.
- Everywhere else, nothing changes before 2027.

The wiki recommends setting up a free installation method now, so you do not find the block on the day an update is refused. With a computer, that method is ADB: with the phone connected by USB and USB debugging on, `adb install -r <your-apk-name>.apk` updates AAPS and keeps all its data and settings. The full steps are on the linked page.

Next: [Step 3 · Check and import](03-verify-and-import.md)
