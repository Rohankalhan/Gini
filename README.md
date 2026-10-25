# YouTube AI Agent Pro (Android starter)

A personal-use Android app starter for AI-assisted YouTube script planning and manually approved **private** video uploads.

## Included

- Compose UI
- Gemini API script/metadata generation through the Gemini Developer API
- Room database for saving generated project records
- MP4 picker
- Explicit approval checkbox and code-level approval guard
- YouTube Data API resumable-upload initiation and private-only metadata
- GitHub Actions workflow to build a debug APK in the cloud

## Important limitations

This is a starter implementation, not a finished end-to-end video factory. It does **not** automatically generate voice-over, create/edit/render video scenes, or generate a thumbnail. The upload function currently sends the selected MP4 as a single request after creating a resumable session; it does not implement retry/resume chunk logic for unstable networks. Upload may fail for very large files or interrupted connections.

The app asks for a Gemini API key and a YouTube OAuth **access token**. It does not implement the Google OAuth sign-in screen. Access tokens are short-lived. Never paste a token into public chats or share an APK containing your credentials. Credentials are stored in local app preferences in this personal-testing starter; that is not suitable for a public/distributed app. A production version should use the official OAuth flow and a trusted backend where needed.

## Free setup

1. Create a Gemini API key in Google AI Studio: https://aistudio.google.com/app/apikey
2. Check current model access, quotas and terms: https://ai.google.dev/gemini-api/docs/models and https://ai.google.dev/gemini-api/docs/rate-limits
3. In Google Cloud Console, create/select a project, enable YouTube Data API v3, configure OAuth consent, and authorize a token with `https://www.googleapis.com/auth/youtube.upload`.
4. Read YouTube upload API requirements: https://developers.google.com/youtube/v3/guides/uploading_a_video
5. Keep upload privacy private. The app UI and upload metadata both enforce `private`.

Free-tier availability, quotas, eligibility and YouTube API audit/testing restrictions can change. A successful build does not guarantee API access or successful uploads.

## Build APK from Android phone using GitHub

1. Create a GitHub repository.
2. Upload all files from this project, preserving folders (including `.github/workflows/build-apk.yml`).
3. Commit to `main` or `master`.
4. Open repository → **Actions** → **Build Android APK** → **Run workflow** (or wait for the push build).
5. When complete, open the workflow run and download artifact `YouTube-AI-Agent-Pro-debug-apk`.
6. Extract the ZIP artifact and install `app-debug.apk` on your Android phone. Android may ask you to allow installation from that browser/files app.

The workflow builds a debug APK for testing, not a Play Store release APK. This repository intentionally does not include API keys, OAuth secrets, or `google-services.json`.

## Local build requirements

- JDK 17
- Gradle 8.9
- Android SDK platform 35 and build tools installed

Run `gradle assembleDebug` from the project root.
