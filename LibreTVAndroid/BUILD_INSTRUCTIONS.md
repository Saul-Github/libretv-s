# Building the LibreTV Android App

## Prerequisites
1.  **Android SDK:** Ensure the Android SDK is installed and configured (usually via Android Studio).
2.  **Java Development Kit (JDK):** Required for Gradle (often bundled with Android Studio or can be installed separately).
3.  **Keystore (for Release Builds):**
    *   You need a Java Keystore (JKS) file to sign your release builds.
    *   If you don't have one, you can generate it using the `keytool` command that comes with the JDK.
        Example `keytool` command:
        `keytool -genkey -v -keystore your_release_keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias your_key_alias`
    *   Store this keystore file securely and back it up. **Losing it means you cannot update your app on the Play Store.**
    *   You'll need to configure Gradle with the keystore path, store password, key alias, and key password. This is typically done in `app/build.gradle` (often by loading from a `keystore.properties` file that you add to `.gitignore`) or by providing these details via environment variables. The `app/build.gradle` in this project contains comments where this configuration should be added.

## Build Commands
Open a terminal or command prompt in the `LibreTVAndroid` project root directory.

### To build an APK (for direct installation/testing):
*   **Debug APK:**
    *   On Linux/macOS: `./gradlew assembleDebug`
    *   On Windows: `gradlew.bat assembleDebug`
    *   Output: `LibreTVAndroid/app/build/outputs/apk/debug/app-debug.apk`
*   **Release APK:**
    *   **Important:** Ensure you have configured release signing in `app/build.gradle` first.
    *   On Linux/macOS: `./gradlew assembleRelease`
    *   On Windows: `gradlew.bat assembleRelease`
    *   If signing is not configured, this might produce an `app-release-unsigned.apk` or the build might fail.
    *   If signing is configured: `LibreTVAndroid/app/build/outputs/apk/release/app-release.apk`

### To build an Android App Bundle (AAB) (preferred format for Google Play Store):
*   **Debug AAB (less common, mainly for testing bundle features):**
    *   On Linux/macOS: `./gradlew bundleDebug`
    *   On Windows: `gradlew.bat bundleDebug`
    *   Output: `LibreTVAndroid/app/build/outputs/bundle/debug/app-debug.aab`
*   **Release AAB:**
    *   **Important:** Ensure you have configured release signing in `app/build.gradle` first.
    *   On Linux/macOS: `./gradlew bundleRelease`
    *   On Windows: `gradlew.bat bundleRelease`
    *   Output: `LibreTVAndroid/app/build/outputs/bundle/release/app-release.aab`

## Important Notes on Release Signing & TWA:
*   The `assetlinks.json` file hosted on your website (`https://libretv-s.vercel.app/.well-known/assetlinks.json`) *must* contain the SHA-256 fingerprint of the certificate from the keystore used to sign your **release** build (`app-release.apk` or `app-release.aab`).
*   Using an APK/AAB signed with a debug key (e.g., `app-debug.apk`) **will not** allow the TWA to run in full-screen mode (without the browser UI) on users' devices. It might work for local testing if Chrome has developer flags enabled or if it's the same debug key Chrome uses for local development.
*   Always test your release-signed build to confirm Digital Asset Links verification is successful and the TWA runs as expected. You can check Logcat for messages related to "DigitalAssetLinks" during app startup.
*   The placeholder in `app/build.gradle` currently uses `signingConfigs.debug` for the release build type. This **must be changed** to your actual release signing configuration for a proper release.
