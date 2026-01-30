# RYN Highway Drift — Unity Android APK Kit

This kit helps you produce a **debug (unsigned)** Android APK for your Unity project quickly. 
It assumes **Unity 2021.3 LTS or newer** with **Android Build Support (SDK/NDK, OpenJDK)** installed.

## What’s inside
- `Assets/RYN/Editor/BuildCLI.cs` — One-click/CLI build to `Builds/Android/RYN-Highway-Drift.apk`.
- `Assets/RYN/Editor/RynConfigure.cs` — Menu action to set **app name**, **package id**, **minSdk**, and **icon**.
- `Assets/RYN/icon-ryn-512.png` — Placeholder 512×512 app icon.
- `CI/android-apk.yml` — Optional GitHub Actions workflow (GameCI) for cloud builds.
- `build_android.sh` / `build_android.ps1` — Local command-line build runners.
- `.gitignore` — Unity-friendly ignores.

## Defaults applied
- **App name**: `RYN Highway Drift`
- **Package id**: `com.ryn.highwaydrift`
- **Min SDK**: Android 8.0 (API 26)
- **Build**: Debug APK (unsigned). Signed release can be added later.

---

## Quick Start (Local Build)
1. Open your Unity game project (or create a new 3D URP/3D project).
2. Copy the `Assets/RYN` folder from this kit **into your project’s `Assets/`** folder.
3. In Unity: **File → Build Settings → Android → Switch Platform**.
4. Go to **Tools → RYN → Apply Android Settings** to auto-set app name, package id, minSdk, and icon.
5. **File → Build Settings → Scenes In Build**: ensure your game scenes are added and enabled.
6. Build from menu: **Tools → RYN → Build Android APK** (or see CLI below).

The APK will be created at: `Builds/Android/RYN-Highway-Drift.apk`

### Command-line build
- **macOS/Linux**: edit `build_android.sh` to set `UNITY_PATH` to your Unity Editor binary, then:
  ```bash
  chmod +x build_android.sh
  ./build_android.sh
  ```
- **Windows PowerShell**: edit `build_android.ps1` `UNITY_PATH`, then run:
  ```powershell
  ./build_android.ps1
  ```

> Tip: Add/enable your scenes in **File → Build Settings**. The builder uses the enabled list.

---

## Cloud Build (GitHub Actions) — Optional
1. Create a GitHub repo and push your Unity project.
2. Copy `CI/android-apk.yml` to `.github/workflows/android-apk.yml` in your repo.
3. **Unity license activation**: Follow GameCI docs to generate and add `UNITY_LICENSE` as a GitHub secret (Personal license works).
4. Push to `main`. The workflow will produce an artifact named **RYN-Highway-Drift** containing the APK.

GameCI docs: https://game.ci/docs/github/getting-started

---

## Later: Signed Release (Play Store)
When ready:
1. Generate a keystore (one-time):
   ```bash
   keytool -genkey -v -keystore ryn.keystore -alias rynkey -keyalg RSA -keysize 2048 -validity 36500
   ```
2. In Unity **Player Settings → Publishing Settings**, assign the keystore, alias, and passwords.
3. Build **AAB** for Play Store or **APK** for side-loading.

---

## Troubleshooting
- **Android SDK/NDK not found**: Reinstall *Android Build Support* via Unity Hub → Installs → Add Modules.
- **No scenes in build**: Add your scene(s) in **File → Build Settings**.
- **Gradle/SDK errors**: Set **Target API** to the latest installed in **Player Settings → Android**.

Happy drifting! 🏁
