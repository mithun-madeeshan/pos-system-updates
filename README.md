# POS updates

The update feed for the POS system. **This repository is public on purpose** and holds no code: only GitHub
**Releases**, each carrying the files every till and phone downloads.

| File in each release | Who reads it |
|---|---|
| `latest.yml` | the Windows till (electron-updater): newest version, size and checksum |
| `POS-Till-Setup-<version>.exe` + `.exe.blockmap` | the Windows till downloads and installs it on its own |
| `android.json` | the Android app's start screen: `{ version, versionCode, apk, notes }` |
| `POS-Mobile-<version>.apk` | the phone opens it in the browser; Android installs it over the app |

Tills and phones always read **the latest release**
(`https://github.com/mithun-madeeshan/pos-system-updates/releases/latest/download/<file>`), so **every release must
carry all the files** — the till and the Android ones — even when only one of them changed.

## Publishing an update

1. Build: `npm run dist` in `pos-system/till`, and `node scripts/build-apk.mjs` in `pos-mobile` (or `pos-system/mobile`).
2. In `pos-system`: `node scripts/release/make-release.mjs --notes "What changed"` → a folder in
   `D:\Mithun\Shared\POS Updates\v<version>` with all the files.
3. On github.com: this repository → **Releases → Draft a new release** → tag `v<version>` → drag in every file from
   that folder → **Publish release**. (With a `GITHUB_TOKEN` set, step 2 does this itself.)
4. Tills install it within 4 hours (or Settings → About → **Check for updates**); phones offer it on the next start.

Why public: a private repository's downloads need a password on every till. The installers are the same files the
shops are given; nothing secret is in them.

© 2026 Mithun Madeeshan. All rights reserved.
