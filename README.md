# Habeshan Events — Android Releases

Public release repository for the **Habeshan Events** Android app.  
Download the latest APK from the [Releases](https://github.com/AbelaTs/Habeshan-Events-Android-App-Public-Releases/releases) page.

[![App Store](https://img.shields.io/badge/iOS-App%20Store-blue?logo=apple)](https://apps.apple.com/us/app/habeshan-events/id6759814994)

## About

Habeshan Events is a community event discovery platform for finding, creating, and sharing events. Features include:

- Browse and search events by location, category, and date
- RSVP, favorite, and share events
- Real-time notifications for event updates
- In-app messaging between attendees and organizers
- Google and Apple sign-in

## Install

1. Go to [Releases](https://github.com/AbelaTs/Habeshan-Events-Android-App-Public-Releases/releases)
2. Download the latest `habeshan-events-vX.X.X.apk`
3. Open the APK on your Android device
4. If prompted, allow installation from unknown sources in your device settings
5. Tap **Install**

**Minimum Android version:** 5.0 (Lollipop, API 21)

## Release Process

Releases are built automatically via GitHub Actions from the private source repository. Each release includes:

- A signed release APK
- Version number and build number
- Release notes describing changes

### How to Trigger a Release

Releases are triggered manually via the **Actions** tab:

1. Go to **Actions** → **Build & Release Android APK**
2. Click **Run workflow**
3. Enter the **version** (e.g. `1.2.0`)
4. Optionally enter **release notes**
5. Click **Run workflow**

The workflow will:
- Check out the source code from the private repository
- Build a signed release APK using Flutter
- Create a GitHub Release with the APK attached

## CI/CD Setup

The workflow requires the following **repository secrets** to be configured:

| Secret | Description |
|---|---|
| `SOURCE_REPO` | Private source repo in `owner/repo` format (e.g. `AbelaTs/habeshan_events`) |
| `SOURCE_REPO_PAT` | GitHub Personal Access Token with `repo` scope for the private source repo |
| `KEYSTORE_BASE64` | Base64-encoded Android upload keystore (`.jks`) |
| `KEYSTORE_PASSWORD` | Keystore password |
| `KEY_PASSWORD` | Key password |
| `KEY_ALIAS` | Key alias name |
| `GOOGLE_SERVICES_JSON` | Base64-encoded `google-services.json` from Firebase |

### Generating Secrets

**Keystore (if you don't have one yet):**

```bash
keytool -genkey -v -keystore upload-keystore.jks -keyalg RSA \
  -keysize 2048 -validity 10000 -alias upload
```

**Base64 encode the keystore:**

```bash
base64 -i upload-keystore.jks | pbcopy
# Paste into KEYSTORE_BASE64 secret
```

**Base64 encode google-services.json:**

```bash
base64 -i mobile/android/app/google-services.json | pbcopy
# Paste into GOOGLE_SERVICES_JSON secret
```

**Personal Access Token:**

1. Go to [GitHub Settings → Tokens](https://github.com/settings/tokens)
2. Generate a **classic** token with `repo` scope
3. Paste into `SOURCE_REPO_PAT` secret

## Links

- **iOS App:** [App Store](https://apps.apple.com/us/app/habeshan-events/id6759814994)
- **Web App:** [habeshanevents.com](https://habeshanevents.com)
