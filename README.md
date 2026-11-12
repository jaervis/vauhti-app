# Vauhti

Two versions of the Vauhti marketing site, side by side:

- **`/`** — the first version: four ride classes (VauhtiX, Green, Comfort, XL), 12 % commission, Finnish. Kept as designed.
- **`/v2/`** — the second version: the fair 5 % commission story, three classes (Vauhti, Vauhti Perhe, Vauhti Lemmikki), in Finnish, English and Italian.

## Live

- First version: https://vauhti-app.pages.dev/
- Second version (FI): https://vauhti-app.pages.dev/v2/
- English: https://vauhti-app.pages.dev/v2/en/
- Italian: https://vauhti-app.pages.dev/v2/it/
- Interactive Flutter demo: https://vauhti-app.pages.dev/demo/
- Kiln editor sign-in: https://vauhti-app.pages.dev/kiln
- Kiln worker: https://kiln-auth.apps-saku.workers.dev
- GitHub: https://github.com/jaervis/vauhti-app
- Android APK: https://github.com/jaervis/vauhti-app/releases/tag/v1.0.0
- Cloudflare Pages project: `vauhti-app`

## What is here

| Path | What it is |
| --- | --- |
| `index.html` | First version, Finnish |
| `assets/` | First version assets, plus the shared Kiln scripts |
| `v2/index.html` | Second version, Finnish (source language) |
| `v2/en/`, `v2/it/` | Second version in English and Italian, localized app screenshots |
| `v2/assets/` | Second version tokens, CSS, fonts and screenshots |
| `demo/` | Prebuilt Flutter web demo (base path `/demo/`) |
| `_headers` | Security headers for Cloudflare Pages |
| `_redirects` | `/en/*` → `/v2/en/*`, `/it/*` → `/v2/it/*`, `/v1/*` → `/` |
| `kiln.html`, `assets/kiln*.js` | Self-hosted Kiln editor wiring |

## Deploy

- Host: Cloudflare Pages, connected to `jaervis/vauhti-app`
- Build command: leave empty
- Output directory: `/`
- Production branch: `main`
- Every push to `main` deploys (Cloudflare Workers and Pages GitHub App installed).
- The Android APK lives in a GitHub Release (Pages has a 25 MiB per-file limit and the APK is ~48 MB).

Node 22 is required for the current Wrangler CLI:

```bash
nvm use
```

Manual deploy if needed:

```bash
npx wrangler pages deploy . --project-name vauhti-app --branch main
```

## Preview locally

No build step. Serve the repository root:

```bash
python3 -m http.server 8080
```

- http://localhost:8080/ — first version
- http://localhost:8080/v2/ — second version (FI)
- http://localhost:8080/v2/en/ — English
- http://localhost:8080/v2/it/ — Italian
- http://localhost:8080/demo/ — Flutter demo

The demo accepts `?screen=/home` and `?lang=fi|sv|en|it`.

## Kiln

- Self-hosted **free** plan: the shared Cloudflare Worker `kiln-auth` plus the Kiln GitHub App.
- Copy is tagged with `data-cms` attributes on both the first version and `/v2/`; sign in at `/kiln` to edit.
- The site config lives in `assets/kiln-config.js` (`repo`, `branch`, `worker`, `siteName`).
- Editing commits straight to `main`, which redeploys Pages.

## Versions

- **v1** (root): four classes, 12 % commission, Finnish only.
- **v2** (`/v2/`): three classes, 5 % commission to Vauhti / 95 % to the driver, FI + EN + IT.

## Android demo

`vauhti-1.0.0.apk` is a signed universal build (arm64-v8a, armeabi-v7a, x86_64), package `fi.vauhti.vauhti_app`, Android 7.0+, no permissions, works offline. It is attached to the `v1.0.0` GitHub release.
