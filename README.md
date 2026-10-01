# Tasks: store app project (Capacitor 8)

Your Tasks app, wrapped as native Android and iOS projects. The web app lives in `www/`. I could not build, sign or submit it from here, so the steps below are yours to run.

## What you need
- Node 22 or newer
- **Android:** Android Studio 2025.2.1+ (Capacitor 8 minimum), plus a Google Play Console account (one-time fee, about $25)
- **iOS:** a Mac with Xcode 26+ (Capacitor 8 minimum), plus an Apple Developer Program membership (about $99/year)
Check current fees and requirements on each store's site.

## 1. Set your app ID
Edit `appId` in `capacitor.config.json` (reverse-domain style, like `com.yourname.tasks`). It must be unique and cannot be changed after you publish.

## 2. Build the native projects
```
npm install
npx cap add android
npx cap add ios          # Mac only
npx @capacitor/assets generate --iconBackgroundColor '#12353A' --splashBackgroundColor '#12353A'
npx cap sync
```
Try it on a phone or emulator: `npx cap run android` or `npx cap run ios`.
After any change to `www/`, run `npx cap sync` again.

## 3. Google Play (Android)
1. `npx cap open android`, then Build > Generate Signed App Bundle (.aab). Back up your keystore; losing it blocks updates.
2. Confirm `targetSdkVersion` in `android/variables.gradle` is 36 or higher. Play requires API 36 for new apps and updates from Aug 31, 2026.
3. In Play Console, create the app and upload the .aab to Internal testing first.
4. Complete the store listing, screenshots, privacy policy URL, Data safety, content rating and target audience.
5. Personal accounts created after Nov 13, 2023 must run a closed test with at least 12 testers for 14 continuous days before production. Organization accounts are exempt.

## 4. App Store (iOS)
1. `npx cap open ios`, set your Team and Bundle Identifier under Signing & Capabilities.
2. Product > Archive > Distribute App > App Store Connect.
3. In App Store Connect, add the listing, screenshots, privacy policy URL and App Privacy answers. With no analytics or network calls, "Data Not Collected" applies; update it if you add any.
4. Apple can reject apps that feel like a repackaged website (guideline 4.2). This app is fully usable offline, and adding native features such as reminders makes approval more likely. Approval is never guaranteed.

## Good to know
- Tasks are saved on the device only: no sync, and uninstalling deletes them.
- Tasks from the claude.ai page or the web/PWA version do not carry over.
- Web fonts were removed so the app makes no network requests. It uses the system font. To bundle the original fonts, put .woff2 files in `www/fonts` and add `@font-face` rules.
- `PRIVACY.md` is a starting policy. Host it at a public URL (GitHub Pages works) and fill in the brackets.
- `STORE_LISTING.md` has draft listing text.
