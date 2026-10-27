# OpenWA Android app

A small Capacitor app that packages the [OpenWA](https://github.com/rmyndharis/OpenWA) dashboard as
an installable APK. It does not run the gateway itself: it opens the dashboard served by your own
OpenWA server.

## How it works

- `www/index.html` is a launcher. On first start it asks for your server URL, stores it, and
  opens it. Later starts show a short "Connecting…" screen with a **Change server** button.
- Plain `http://` addresses (LAN, VPN) are allowed. Prefer `https://` for anything public.

## Build with GitHub Actions

Workflow: `.github/workflows/android-apk.yml`

| Trigger                         | Result                                          |
| ------------------------------- | ----------------------------------------------- |
| Push to `main`                  | Debug APK as a downloadable workflow artifact   |
| **Actions → Android APK → Run** | Pick debug or release, optionally bake in a URL |
| Tag `v1.0.0`                    | Release build and a GitHub Release with the APK |

Download the APK from the run page (Artifacts) or the Release, copy it to your phone and open it.

### Default server URL (optional)

Set the repository variable `OPENWA_DEFAULT_URL` (Settings → Secrets and variables → Actions →
Variables), or fill the `server_url` input when running manually.

### Signed release builds (optional)

Add these repository secrets: `ANDROID_KEYSTORE_BASE64` (output of `base64 -w0 release.jks`),
`ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS`, `ANDROID_KEY_PASSWORD`. Without them, release
builds are unsigned and the debug APK is the one to install.

## Build locally

Requires Node 22, JDK 21 and the Android SDK.

```bash
npm ci
npm run build:debug
# APK: android/app/build/outputs/apk/debug/app-debug.apk
```
