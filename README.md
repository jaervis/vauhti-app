# Vauhti

The Vauhti marketing site: a Finnish ride-hailing service with a 5 % commission. Three ride classes — Vauhti, Vauhti Perhe and Vauhti Lemmikki.

## Live

- Site (Finnish): https://vauhti-app.pages.dev/
- English: https://vauhti-app.pages.dev/en/
- Italian: https://vauhti-app.pages.dev/it/
- Interactive Flutter demo: https://vauhti-app.pages.dev/demo/
- First draft archive: https://vauhti-app.pages.dev/v1/
- Kiln editor sign-in: https://vauhti-app.pages.dev/kiln
- Kiln worker: https://kiln-auth.apps-saku.workers.dev
- GitHub: https://github.com/jaervis/vauhti-app
- Android APK: https://github.com/jaervis/vauhti-app/releases/tag/v1.0.0
- Cloudflare Pages project: `vauhti-app`

## What is here

| Path | What it is |
| --- | --- |
| `index.html` | Finnish site (source language) |
| `en/`, `it/` | English and Italian pages, same layout, localized app screenshots |
| `assets/` | Shared tokens, CSS, fonts, screenshots, Kiln assets |
| `demo/` | Prebuilt Flutter web demo (base path `/demo/`) |
| `v1/` | First website draft, kept for reference. `noindex`. |
| `_headers` | Security headers for Cloudflare Pages |
| `kiln.html`, `assets/kiln*.js` | Self-hosted Kiln editor wiring |

## Deploy

- Host: Cloudflare Pages, connected to `jaervis/vauhti-app`
- Build command: leave empty
- Output directory: `/`
- Production branch: `main`
- Auto-deploy: install the **Cloudflare Pages** GitHub App on this repository — https://github.com/apps/cloudflare-workers-and-pages/installations/new — then every push to `main` deploys.
- Until the app is installed, publish manually: `npx wrangler pages deploy . --project-name vauhti-app --branch main`
- The Android APK lives in a GitHub Release (Pages has a 25 MiB per-file limit and the APK is ~48 MB).

Node 22 is required for the current Wrangler CLI:

```bash
nvm use
```

## Preview locally

No build step. Serve the folder at the repository root:

```bash
python3 -m http.server 8080
```

- http://localhost:8080/ — Finnish
- http://localhost:8080/en/ — English
- http://localhost:8080/it/ — Italian
- http://localhost:8080/demo/ — Flutter demo
- http://localhost:8080/v1/ — first draft

The demo accepts `?screen=/home` and `?lang=fi|sv|en|it`.

## Kiln

- Self-hosted **free** plan: the shared Cloudflare Worker `kiln-auth` plus a GitHub App.
- Install the app on this repository before editing: https://github.com/apps/kiln-cms-handyman/installations/new
- Copy is tagged with `data-cms` attributes; sign in at `/kiln` to edit.
- The site config lives in `assets/kiln-config.js` (`repo`, `branch`, `worker`, `siteName`).
- Editing commits straight to `main`, which redeploys Pages.

## Business model shown on the site

- Vauhti takes a **5 % commission**; the driver keeps **95 %**.
- No start fee, no hidden deductions.
- Fixed price shown before the ride.
- Three classes: Vauhti, Vauhti Perhe (child seat), Vauhti Lemmikki (pets).

## Android demo

`vauhti-1.0.0.apk` is a signed universal build (arm64-v8a, armeabi-v7a, x86_64), package `fi.vauhti.vauhti_app`, Android 7.0+, no permissions, works offline. It is attached to the `v1.0.0` GitHub release.
