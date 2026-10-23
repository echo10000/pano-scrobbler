# First Android test APK (Last.fm dashboard)

This fork keeps the upstream Pano source unchanged and adds an Android-only
GitHub Actions build. The stock APK is not yet rebranded.

## Configure Last.fm

1. Register a new Last.fm API application at https://www.last.fm/api/account/create.
2. Go to **Settings → Secrets and variables → Actions** in this fork.
3. Add two **repository secrets**:
   - `LASTFM_API_KEY`: your application API key
   - `LASTFM_API_SECRET`: your application shared secret
4. Never commit `local.properties`, keys, account passwords, or keystores.

Pano's Gradle configuration encodes these values into the APK. That is
obfuscation, **not secure storage**: treat app API credentials as extractable
by APK recipients. Follow Last.fm's API terms before public distribution.

## Build

1. Open **Actions → Build Android test APK → Run workflow**, on `main`.
2. When the run succeeds, download artifact `pano-android-test-apk`.
3. Extract the artifact ZIP and install the APK on an Android device.

If the build fails, inspect the failing Actions step and its logs. This build
uses the upstream task `androidApp:assembleReleaseGithub`.

## Limits of this first build

- This is a test build, **not** a Play Store release.
- It uses a new temporary signing key on each run. To install subsequent test
  builds you may need to uninstall the previous one first. Back up any data
  you care about before doing so.
- The app still uses Pano's upstream package name, icon, and branding.
  It may conflict with the official Pano app already installed.
- `spotify.refreshToken` is set to `disabled` only to meet an upstream
  Gradle configuration requirement. Spotify-only integration is not set up.
- This workflow is separate from the upstream multi-OS release process.
- First validate Last.fm login, recent scrobbles, top albums/artists/tracks,
  charts, image fetching, collage export, and sharing before redesigning.

## Future custom release

Choose a distinct package ID, name and logo; decide which non-chart features
to retain; generate and back up a **stable release signing key**; and review
upstream GPL-3.0-or-later license obligations and third-party API policies.
