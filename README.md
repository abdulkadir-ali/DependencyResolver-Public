# DependencyResolver-Public

**Smart, one-click Android dependency management plugin for Android Studio and IntelliJ IDEA.**

![Dependency Resolver UI](assets/screenshot_0.0.5.png)

## 📌 Overview 
Adding dependencies to an Android project is historically tedious. Developers have to:
1. Search Maven Central for the correct artifact coordinates.
2. Figure out the right compatibility version for your project's Kotlin, AGP, and SDK versions.
3. Manually add entries to `libs.versions.toml`, `build.gradle.kts`, and handle `ksp`/`plugin` configurations.

**Dependency Resolver completely automates this.** It operates via a dedicated IDE tool window, fetching a daily-updated remote knowledge base (via Cloudflare Pages) and recommending the perfectly compatible Library + Plugin versions based on your actual local setup.

---

## ✨ Features

- **Auto-detects project config** — instantly reads your active Kotlin, AGP, Gradle, and compileSdk versions.
- **Remote Knowledge Base** — fetches daily-updated versions of 30+ libraries from a Custom Cloudflare Pages API.
- **Intelligent Compatibility Engine** — doesn't just give you the latest version; it guarantees the suggested version is compatible with your local Kotlin/AGP constraints, and dynamically aligns companion compiler plugins (like matching Kotlin `2.2.0` with KSP `2.2.0-1.0.28`).
- **One-click insertion** — automatically generates and inserts entries into `[versions]`, `[libraries]`, and `[plugins]` in your TOML catalog, plus corresponding lines in your app's Gradle file.
- **Supports both DSLs** — Kotlin DSL (`build.gradle.kts`) and Groovy DSL (`build.gradle`).
- **BOM support** — automatically uses `platform()` wrappers where required (e.g. Jetpack Compose, OkHttp, Koin, Ktor).

---

## 🚀 How to Use

### 1. Open the Tool Window
Open any Android project, then go to:
> **View → Tool Windows → Dependency Resolver**

The tool window appears at the bottom of the IDE alongside Logcat, Terminal, and Build.

### 2. Check Your Project Config
The **status bar** at the top instantly reads your environment. In the screenshot above, it detects:
- **Kotlin:** `2.2.0`
- **AGP:** `8.9.1`
- **Gradle:** `9.1.0`
- **compileSdk:** `36`
- **DSL:** `Kotlin`
- **Version Catalog:** `✓`

*(Click **↻ Refresh** on the far right to re-scan if you've recently changed your project config).*

### 3. Search for Libraries
Type a library name in the search field (e.g. `room` in the screenshot):
- `compose` → Jetpack Compose (BOM + UI + Material3)
- `retrofit` → Retrofit + Gson converter
- `room` → Room (runtime + KTX + KSP compiler)
- `hilt` → Hilt (Android + KSP compiler)
- ...and 25+ more!

You can also search by category keywords like `networking`, `database`, `testing`, `di`, `image`.

### 4. Review Suggestions
### 4. Review Suggestions
Each result card gives you everything you need to know. For example, the `Room` card in the screenshot shows:
- **Library Name & Version:** `Room v2.6.4` (guaranteed to be compatible)
- **Description & Category:** SQLite mapping library `[DATABASE]`
- **Dependencies list:** Adds `room-runtime`, `room-ktx`, and `room-compiler`
- **Required plugins:** Adds the `com.google.devtools.ksp` plugin. *(Notice how the plugin dynamically aligned the KSP version to `2.2.0-1.0.28` to perfectly match the project's Kotlin `2.2.0` compiler!)*
- **Compatibility Status:** ✅ Compatible

### 5. Add to Project
Click **✚ Add to Project** to insert the dependency. The plugin will:

1. Add version entries to `[versions]` in `libs.versions.toml`
2. Add library entries to `[libraries]` in `libs.versions.toml`
3. Add plugin entries to `[plugins]` if needed
4. Add `implementation(libs.xxx)` lines to `app/build.gradle.kts`
5. Add `alias(libs.plugins.xxx)` to the plugins block if needed
6. Show a balloon notification confirming success
7. Trigger Gradle sync

---

## 📦 Supported Libraries

| Category | Libraries |
|---|---|
| **UI** | Jetpack Compose (BOM), Material Components |
| **Networking** | Retrofit, OkHttp (BOM), Ktor Client (BOM) |
| **Database** | Room (w/ KSP), DataStore |
| **DI** | Hilt (w/ KSP), Koin (BOM) |
| **Architecture** | Navigation, Lifecycle, Paging, WorkManager, Fragment KTX, Activity KTX |
| **Image Loading** | Coil, Glide (w/ KSP) |
| **Serialization** | Kotlinx Serialization, Moshi (w/ KSP), Gson |
| **Async** | Kotlin Coroutines |
| **Utility** | Timber, LeakCanary |
| **Media** | CameraX, Media3 / ExoPlayer |
| **Testing** | JUnit, MockK, Truth, Espresso, Turbine, Robolectric |

---

## 📋 Requirements

- Android Studio Ladybug (2024.2) or newer
- IntelliJ IDEA 2024.2+

---

## 📬 Contact & Support

Developed by **Abdulkadir Ali**

Have a question, suggestion, or feature request? Reach out at:
📧 [abdulkadir.ali@live.in](mailto:abdulkadir.ali@live.in)
