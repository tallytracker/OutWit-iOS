# OutWit-iOS

The App Store wrapper for OutWit (https://outwit-37291.web.app).

Copied on 28 Sep 2026 from `tallytracker/Tally-iOS` at commit `353e349`, which is
the proven no-Mac pipeline: GitHub's macOS runners compile, sign and upload.

- `ios-build.yml`: simulator build on every push, no signing. Checks that the project compiles.
- `ios-release.yml`: manual. Signed archive → .ipa → (optional) App Store Connect upload.
  Needs repo secrets `APPSTORE_API_KEY_ID`, `APPSTORE_API_ISSUER_ID`, `APPSTORE_API_PRIVATE_KEY`
  (the same team-level App Store Connect API key Tally-iOS uses).

Before the first release:
1. Replace `src/OutWit/GoogleService-Info.plist` with the real file from Firebase
   (project outwit-37291, iOS app `io.github.tallytracker.outwit`).
2. Put its CLIENT_ID into `GIDClientID` and its REVERSED_CLIENT_ID into the
   `google-signin` URL scheme in `src/OutWit/Info.plist`.
3. App ID `io.github.tallytracker.outwit` must have Sign in with Apple and Push Notifications enabled.
4. APPLE_SIGNIN_ENABLED must already be true and live on the web app (Guideline 4.8).

The release workflow refuses to run while any placeholder remains.
