# Android Development Environment for LibreTV App

This document outlines the necessary components and configuration for the Android Development Environment (ADE) required to build and test the LibreTV Android application.

## 1. Core Tools

The primary software tools required for developing the LibreTV Android app are:

*   **Android Studio:** The official Integrated Development Environment (IDE) for Android app development. This includes:
    *   **Android SDK (Software Development Kit):** A collection of tools and libraries necessary for developing Android applications.
    *   **Build Tools:** Tools required to compile and package the Android application (e.g., AAPT, dx, d8, R8).
    *   **Android Emulator:** For running and testing the application on virtual devices.
    *   **Gradle:** The build automation system used for Android projects.
*   **Java Development Kit (JDK):** Android development requires JDK, typically version 8 or higher (Android Studio often bundles a compatible OpenJDK).
*   **Git:** For version control.

## 2. Key SDK Packages

Within the Android SDK Manager, the following packages are essential:

*   **Android SDK Platform-Tools:** Contains tools like `adb` (Android Debug Bridge) and `fastboot`.
*   **Android SDK Build-Tools:** The latest stable version is recommended.
*   **Android Platform (SDK):** The latest stable Android API version (e.g., Android 13 - API Level 33, or newer as available). It's also good practice to install SDKs for target Android versions if they differ from the latest.
*   **System Images for Emulator:**
    *   At least one system image for a recent Android version (e.g., Android 13 or newer).
    *   Consider images for different form factors (e.g., phone, tablet) and architectures (e.g., x86_64, ARM) if relevant for broader testing.
*   **Android SDK Command-line Tools (latest):** For managing SDK packages via the command line.
*   **NDK (Native Development Kit):** Only if native C/C++ code is anticipated. (Not explicitly mentioned for LibreTV TWA, but good to be aware of).

## 3. Emulator Configuration (Conceptual)

A suitable Android Virtual Device (AVD) configuration for testing the LibreTV app would be:

*   **Device Type:** Pixel 6 (or a similar modern generic phone profile)
*   **Android Version (API Level):** Android 13 (API Level 33) or the latest stable version.
*   **Screen Size:** ~6.4 inches (matching the Pixel 6)
*   **Resolution:** ~1080 x 2400 pixels
*   **RAM:** 2GB or higher
*   **Storage:** 2GB or higher (internal storage for the AVD)
*   **ABI (Application Binary Interface):** `x86_64` for better performance on most development machines, but also consider testing on `arm64-v8a` if performance on ARM devices is critical or if specific ARM-only libraries are used.

## 4. Project Dependencies (Anticipated)

*   **AndroidX Browser Library (`androidx.browser:browser`):** This is crucial for implementing Trusted Web Activities (TWAs), which is a core requirement for the LibreTV app.
*   **AndroidX Core Libraries (`androidx.core:core-ktx`, etc.):** Provides backward compatibility and utility functions.
*   **AndroidX AppCompat Library (`androidx.appcompat:appcompat`):** Provides support for Material Design user interface components and backward compatibility.
*   **AndroidX ConstraintLayout (`androidx.constraintlayout:constraintlayout`):** For flexible and efficient UI design.
*   **Material Components for Android (`com.google.android.material:material`):** For modern UI elements following Material Design guidelines.
*   **Testing Libraries:**
    *   **JUnit (`junit:junit`):** For unit testing.
    *   **Espresso (`androidx.test.espresso:espresso-core`):** For UI testing.
    *   **Mockito (`org.mockito:mockito-core`):** For creating mock objects in tests.
*   **Potential Future Dependencies:**
    *   Networking libraries (e.g., Retrofit, OkHttp) if the app needs to make direct API calls beyond the TWA's scope.
    *   Image loading libraries (e.g., Glide, Picasso) if handling native image views.
    *   Analytics libraries.
    *   Push notification libraries (e.g., Firebase Cloud Messaging).

## 5. Verification

All the components listed above are standard parts of an Android development setup.

*   **Android Studio:** Can be downloaded from the official Android Developer website. It includes the SDK manager to install and manage SDK packages, build tools, and emulator images.
*   **JDK:** Often bundled with Android Studio, or can be installed separately.
*   **SDK Packages:** All listed SDK packages (Platform-Tools, Build-Tools, Platforms, System Images) are available through the Android SDK Manager within Android Studio.
*   **Dependencies:** The AndroidX libraries and other common libraries are available from Google's Maven repository or Maven Central and can be easily added to a Gradle project.

A developer with a standard installation of Android Studio will either have these components or can easily acquire them through the IDE's built-in tools. The environment is well-supported and documented.
