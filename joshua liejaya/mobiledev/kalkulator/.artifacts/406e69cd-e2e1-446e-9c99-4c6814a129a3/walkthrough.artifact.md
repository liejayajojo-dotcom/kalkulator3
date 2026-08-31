# Walkthrough - Resolved Kotlin Extension Conflict

I have successfully resolved the Gradle sync error by migrating the project to use the built-in Kotlin support provided by Android Gradle Plugin (AGP) 9.0+.

## Changes Made

### [app](file:///C:/Users/Admin/Documents/joshua%20liejaya/mobiledev/kalkulator/app)

#### [build.gradle.kts](file:///C:/Users/Admin/Documents/joshua%20liejaya/mobiledev/kalkulator/app/build.gradle.kts)
- Removed `id("org.jetbrains.kotlin.android")` as it is now redundant and causes conflicts with AGP 9.0's built-in Kotlin support.
- Removed the `kotlinOptions` block. The `jvmTarget` now automatically aligns with the `android.compileOptions` settings.

```diff
 plugins {
     id("com.android.application")
-    id("org.jetbrains.kotlin.android")
 }

 android {
@@ -30,9 +29,6 @@
     compileOptions {
         sourceCompatibility = JavaVersion.VERSION_1_8
         targetCompatibility = JavaVersion.VERSION_1_8
     }
-    kotlinOptions {
-        jvmTarget = "1.8"
-    }
 }
```

## Verification Results

### Automated Tests
- **Gradle Sync**: Completed successfully.
- **Build (`app:assembleDebug`)**: Completed successfully, confirming that Kotlin source files are still correctly compiled using the built-in support.

> [!TIP]
> With AGP 9.0+, you no longer need to manually manage the Kotlin plugin version in your build files for standard Android modules, as it is bundled with the Android Gradle Plugin.
