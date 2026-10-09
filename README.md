# CAT Prep: build the Android APK

This folder wraps the CAT prep web app (in `www/index.html`) as an Android app using Capacitor.
Your progress is stored on the phone, so it survives app restarts.

## Option A: build with GitHub (no Android Studio needed)
1. Create a free account at github.com and make a new empty repository.
2. Upload everything in this folder to it (drag and drop on the web page works), keeping the `.github` folder.
3. Open the repository's **Actions** tab, choose **Build APK**, and click **Run workflow**.
4. When it finishes (about 5 minutes), open the run and download the **cat-prep-apk** file under Artifacts. Unzip it to get `app-debug.apk`.
5. Send the APK to your phone, open it, and allow "Install unknown apps" when asked.

## Option B: build on your computer
Requires Node.js 20+, JDK 17, and Android Studio (for the Android SDK).
```
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug        # Windows: gradlew.bat assembleDebug
```
The APK is at `android/app/build/outputs/apk/debug/app-debug.apk`.

## Changing the app
Edit `www/index.html`, then run `npx cap sync android` and rebuild.
To change the app name or package id, edit `capacitor.config.json` before `npx cap add android`.

## Notes
- This is a debug-signed APK: fine for your own phone, not for the Play Store.
  A Play Store release needs your own signing key and a release build.
- Android will warn about installing from outside the Play Store. That is expected for a self-built app.
