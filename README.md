# Android apps — for every website

One repo, three Android apps. Each app loads its live website
inside the app, so the app has **the same features as the
website by construction** — no second codebase, no separate
app backend.

| App | Android package | Website it loads |
|---|---|---|
| LeadsForceGen | `com.leadsforcegen.app` | https://leadsforcegen.vercel.app |
| PDF Tools Hub | `com.pdftoolshub.app` | https://pdf-tools-hub-nine-lac.vercel.app |
| AI Studio | `com.aistudio.app` | https://ai-studio-sandy-sigma.vercel.app |

## How the app ↔ website integration works

There is nothing to sync, because there is nothing separate to
sync. The app opens the live site (Capacitor shell around the
real site). Login, accounts, data, payments and settings all run
on the site's own backend (Supabase for all three sites), so
something done in the app shows on the website immediately, and
the other way round. Signing in on the app is signing in on the
website — same account, same data.

## Install on a phone (once a release exists)

1. Open the repo's **Releases** page and download the APK for
   the app you want.
2. On the phone, allow "install unknown apps" once for the
   browser, then open the APK.
3. The app opens the live site. Sign in with the same account
   you use on the website.

Releases are built automatically: pushing a version tag
(`v1.0.0`, `v1.1.0`, …) runs the workflow in
`.github/workflows/android.yml`, which builds a debug APK for
each app and attaches all three to that tag's release.

## Build it yourself (Android Studio)

```sh
cd apps/leadsforcegen   # or pdf-tools-hub / ai-studio
npm install
npx cap sync android
npx cap open android
```

Then run on an emulator or a connected phone from Android
Studio. A local build needs the Android SDK + JDK 17; this repo
does not include them.

## Icons (placeholders)

`apps/*/assets/icon-1024.png` (and the launcher icons generated
from it) are simple letter icons made for this first version.
Replace them with the real brand icons before any Play Store
submission — the Play listing needs a proper 512×512 icon plus
screenshots.

## What is NOT done yet (his taps, later)

- **Play Store listing.** These APKs are direct-install builds.
  A Play Store release needs: a release signing keystore (create
  it once, back it up, never commit it here), a Play Console
  account, a privacy policy URL, screenshots, and a content
  rating. None of that is in this repo.
- **Website buttons.** Each website gets an "Android app"
  section linking to its release APK. Those links are added
  only after the first release exists, so no site ever links to
  a download that is not there yet.
- **Push notifications, offline mode, in-app purchases.**
  The apps are the websites, so anything the website does not
  do, the app does not do either. Those are separate features,
  not part of this first version.

## Repo layout

```
apps/
  leadsforcegen/     Capacitor app (LeadsForceGen)
  pdf-tools-hub/     Capacitor app (PDF Tools Hub)
  ai-studio/         Capacitor app (AI Studio)
.github/workflows/
  android.yml        Builds APKs + publishes releases on tags
```
