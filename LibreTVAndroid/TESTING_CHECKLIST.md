# LibreTV Android TWA - Testing Checklist

This checklist outlines the key areas to test for the LibreTV Android Trusted Web Activity (TWA) application.

## I. Pre-requisites & Setup

*   [ ] **Digital Asset Links (`assetlinks.json`) Correctly Configured & Hosted:**
    *   **CRITICAL:** Verify that the `assetlinks.json` file is correctly generated with the **SHA256 fingerprint of the release signing key**.
    *   **CRITICAL:** Ensure `assetlinks.json` is hosted at `https://libretv-s.vercel.app/.well-known/assetlinks.json`.
    *   **Verification:** Use Google's Digital Asset Links API (`https://digitalassetlinks.googleapis.com/v1/statements:list?source.web.site=https://libretv-s.vercel.app&relation=delegate_permission/common.handle_all_urls`) to confirm the association with `com.libretv.android`. Check Logcat for "DigitalAssetLinks" messages during app launch for successful verification by Chrome.

## II. Installation & Basic App Info

*   [ ] **App Installation:**
    *   [ ] Install release build (APK or App Bundle) successfully on a target device/emulator.
    *   [ ] Install debug build successfully on a target device/emulator.
*   [ ] **App Icon & Name:**
    *   [ ] Verify the correct app icon is displayed on the home screen and app drawer.
    *   [ ] Verify the app name ("LibreTV") is displayed correctly under the icon and in app settings.

## III. Launch & Initial Experience

*   [ ] **Splash Screen:**
    *   [ ] Verify the custom splash screen (with `ic_splash_logo` and `splash_background_color`) appears on cold start.
    *   [ ] Verify the splash screen transitions smoothly to the main app content.
*   [ ] **TWA Launch & URL:**
    *   [ ] App opens directly into the TWA.
    *   [ ] The URL loaded is `https://libretv-s.vercel.app/`.
    *   [ ] No browser UI (URL bar, Chrome menu) is visible initially (this depends on successful Digital Asset Links verification).
*   [ ] **TWA Full-Screen Verification:**
    *   [ ] **If `assetlinks.json` is correctly set up and verified by Chrome:** The TWA should run in full screen without any browser chrome (URL bar, etc.).
    *   [ ] **If `assetlinks.json` is NOT working:** The TWA might open as a Custom Tab with a visible URL bar. This is a critical failure of the TWA setup.
    *   [ ] Verify status bar color matches `@color/colorPrimaryDark`.

## IV. Core Web App Functionality (within TWA)

*These tests depend on the features of `libretv-s.vercel.app` itself.*

*   [ ] **Navigation:**
    *   [ ] All navigation links (menu, buttons, etc.) within the web app work as expected.
    *   [ ] Back button (device hardware/software) navigates correctly within the web app's history.
    *   [ ] Back button exits the app if at the start of the web app's navigation stack.
*   [ ] **Search Functionality:**
    *   [ ] Search bar is usable.
    *   [ ] Search results are displayed correctly.
    *   [ ] Navigation from search results works.
*   [ ] **Video Playback:**
    *   [ ] Select a video/stream.
    *   [ ] Video playback starts correctly.
    *   [ ] Video player controls (play, pause, seek, volume, fullscreen toggle within the web content) are functional.
    *   [ ] Video playback quality is acceptable (test on different network conditions if possible).
    *   [ ] Audio plays correctly and is synchronized with video.
*   [ ] **Settings (if applicable):**
    *   [ ] Access settings within the web app.
    *   [ ] Modify settings and verify they are applied.
*   [ ] **History (if applicable):**
    *   [ ] Verify viewing history is updated as expected.

## V. App Behavior & System Integration

*   [ ] **Orientation Changes:**
    *   [ ] Rotate the device (portrait/landscape).
    *   [ ] Verify the web content adapts correctly without data loss or crashes.
    *   [ ] Video playback continues smoothly (or pauses and resumes correctly) during orientation changes.
*   [ ] **App Backgrounding & Resuming:**
    *   [ ] Send the app to the background (e.g., press home button).
    *   [ ] Resume the app from recents.
    *   [ ] Verify the app restores its previous state (e.g., same page, video paused at the same position).
*   [ ] **Permissions:**
    *   [ ] Verify the app only requests `INTERNET` permission (as defined in manifest).
    *   [ ] No other unexpected permission requests.
*   [ ] **Offline Capabilities (PWA features, if implemented in the web app):**
    *   [ ] If the PWA supports offline mode (e.g., cached content, service worker), test:
        *   [ ] Launch app in airplane mode/no network.
        *   [ ] Verify offline fallback page or cached content is displayed.
        *   [ ] Test any available offline functionality.
*   [ ] **Deep Linking (if configured beyond TWA default URL):**
    *   [ ] Test any specific deep links into the web app if additional `intent-filter` data elements were added.

## VI. Error Handling & Debugging

*   [ ] **Logcat Monitoring:**
    *   [ ] Monitor Logcat during testing for any errors, warnings, or crashes (filter by app's package name `com.libretv.android`).
    *   [ ] Specifically look for "DigitalAssetLinks" messages to confirm verification status.
    *   [ ] Look for any JavaScript errors from the WebView if possible (though Chrome usually handles this within TWA).
*   [ ] **Network Issues:**
    *   [ ] Test behavior when network connectivity is poor or lost (e.g., app shows appropriate error message from the web content, graceful degradation).

## VII. Performance

*   [ ] **Launch Time:** App launches reasonably quickly (splash screen to interactive TWA).
*   [ ] **Responsiveness:** UI within the TWA is responsive to user input.
*   [ ] **Resource Usage:** (Optional, more advanced) Monitor CPU and memory usage to ensure no excessive consumption.

This checklist should be adapted and expanded based on the specific features and requirements of the LibreTV web application.
---
