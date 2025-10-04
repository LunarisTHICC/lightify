# Lightify — Lightweight Spotify Player (Windows-first)

A minimal desktop Spotify player focused on low RAM/CPU while keeping core features:
- Auto-login via refresh token stored in the OS keychain (Windows Credential Manager)
- Playback controls (play/pause, next/prev, volume)
- Search (tracks, artists, albums, playlists, podcasts) with local metadata cache
- Save/like tracks
- Minimal UI with collapsible song/artist/album/playlist details
- Album art loads only for the currently playing track (optional toggle)

Important
- Requires Spotify Premium for playback via the Spotify Web Playback SDK.
- We never store your password; only a refresh token (securely).
- No audio caching or downloads (Spotify ToS).

## Quick start (Windows)

1) Prerequisites
- Windows 10/11
- Node.js 18+ and npm
- Rust (stable) + Cargo
- Visual Studio Build Tools with “Desktop development with C++” workload
- Microsoft Edge WebView2 runtime (installed by default on most Windows; if missing, install it)

2) Spotify Developer App
- Go to https://developer.spotify.com/dashboard and create an app
- Copy your Client ID
- Add Redirect URI: http://127.0.0.1:51789/callback

3) Configure
- Copy `src-tauri/.env.example` to `src-tauri/.env`
- Set:
  - `SPOTIFY_CLIENT_ID=your_client_id_here`
  - `REDIRECT_URI=http://127.0.0.1:51789/callback`

4) Run
- `npm install`
- `npm run tauri dev`
- Click “Login” the first time to authorize; afterwards the app auto-logs in with the stored refresh token.

## Keyboard shortcuts
- Space: Play/Pause
- Ctrl + Right / Left: Next / Previous
- Ctrl + Up / Down: Volume up / down

## Project layout
- `public/` minimal UI (no framework, no bundler)
- `src-tauri/` Rust backend (auth, API, cache, shortcuts)
- `.github/workflows/ci.yml` CI on Windows

## Notes on storage
- Refresh token is stored securely via the keyring crate (Windows Credential Manager).
- Metadata cache uses SQLite (bundled) with FTS5 for fast local search.
- Album art only fetched for the currently playing track when enabled.

## Roadmap
- System media keys integration (Windows-first), then macOS/Linux media APIs
- Tray controls
- Cross-platform support (macOS/Linux)