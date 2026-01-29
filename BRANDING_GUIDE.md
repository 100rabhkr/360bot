# Branding & White-labeling Guide

This guide explains how to fully rebrand the project to **360labs** and **360bot**, including the CLI, documentation, and companion apps.

## 1. Project Renaming (Completed)

The core project has been renamed from **Moltbot** to **360bot**.

-   **CLI Command**: The command `moltbot` has been renamed to `360bot`.
-   **Package Name**: `package.json` now uses `360bot`.
-   **Configuration Directory**: Defaults to `~/.360bot` (with fallback to `~/.moltbot` for legacy support).
-   **Configuration File**: Defaults to `360bot.json`.

### Verification
Run the CLI to see the new branding:
```bash
360bot --version
360bot setup
```

## 2. Branding Checklist

To complete the white-labeling process for **360labs**, you need to update the following areas.

### A. Codebase Strings & URLs
There are still references to `moltbot` in the codebase that should be updated to `360bot` or `360labs` where appropriate.

**Search & Replace:**
-   **Strings**: Search for `Moltbot` and `Clawdbot` (legacy name) in `src/`.
-   **URLs**: Search for `docs.360bot.com` and `360bot.com`. You should replace these with your own documentation URLs.

**Key Files to Check:**
-   `src/cli/banner.ts`: ASCII art and CLI header.
-   `src/cli/*.ts`: Help text often links to `docs.360bot.com`.
-   `src/config/types.ts`: TypeScript interfaces might still be named `MoltbotConfig`.

### B. Environment Variables
The project respects environment variables for configuration. While we updated the code to check for `MOLTBOT_*` variables, you may want to introduce `360BOT_*` prefixes.

**Files:** `src/config/env-vars.ts`, `src/config/paths.ts`.

### C. Assets & Logos
You need to replace the following image assets with **360labs** branding.

| Location | Description | Action |
| :--- | :--- | :--- |
| `README-header.png` | GitHub README Header | Replace with 360labs header |
| `docs/whatsapp-clawd.jpg` | Documentation Image | Replace with 360labs image |
| `apps/macos/Sources/Moltbot/Resources/Assets.xcassets` | macOS App Icon | Replace AppIcon |
| `apps/ios/Moltbot/Assets.xcassets` | iOS App Icon | Replace AppIcon |
| `apps/android/app/src/main/res/mipmap-*` | Android Launcher Icon | Replace icons |

## 3. Companion Apps (macOS, iOS, Android)

The mobile and desktop apps require specific updates to identifiers and display names.

### macOS App (`apps/macos`)
1.  **Info.plist**: Open `apps/macos/Sources/Moltbot/Resources/Info.plist`.
    -   Change `CFBundleName` to `360bot`.
    -   Change `CFBundleIdentifier` to `com.360labs.bot.mac` (or your domain).
2.  **Xcode Project**: Rename the project and scheme from `Moltbot` to `360bot`.

### iOS App (`apps/ios`)
1.  **Info.plist**: Open `apps/ios/Moltbot/Info.plist`.
    -   Change `CFBundleDisplayName` to `360bot`.
    -   Change `CFBundleIdentifier` to `com.360labs.bot.ios`.
2.  **Xcode Project**: Rename targets.

### Android App (`apps/android`)
1.  **Gradle Config**: Open `apps/android/app/build.gradle.kts`.
    -   Change `applicationId` to `com.360labs.bot.android`.
2.  **Strings**: Open `apps/android/app/src/main/res/values/strings.xml`.
    -   Change `app_name` to `360bot`.

## 4. Documentation

1.  **README.md**: Already updated to reflect `360bot`.
2.  **Docs Site**: If you are hosting your own docs (e.g., Mintlify), find the configuration (usually `mint.json` or similar in `docs/`) and update the project name and logo.

## 5. Deployment

When deploying your white-labeled version:
1.  **NPM**: If publishing to a private registry, update the `name` in `package.json` to `@360labs/360bot` or similar.
2.  **Docker**: Update `Dockerfile` and `docker-compose.yml` to use your new package name and binary (`360bot`).
