# SANCTVM — getting it onto the iPhone

All six files must sit together in one folder, served over **HTTPS**. iOS will not
register a service worker (no offline) from a `file://` URL, so opening `index.html`
straight from the Files app will not work properly.

## Deploy (GitHub Pages — free, ~5 minutes)

1. Create a new **public** repo on github.com, e.g. `sanctum`.
2. Upload all six files to the repo root (drag and drop into the web UI works).
3. Repo → **Settings** → **Pages** → Source: *Deploy from a branch* → branch `main`, folder `/ (root)` → Save.
4. Wait a minute. Your URL will be `https://<username>.github.io/sanctum/`.

Any static host with HTTPS works equally well — Netlify, Cloudflare Pages, Vercel.

## Install on the phone

1. Open the URL in **Safari** (not Chrome — only Safari can add to the home screen).
2. Share button → **Add to Home Screen** → Add.
3. Open it from the home-screen icon. It now runs full-screen with no browser chrome,
   and works with the phone in airplane mode.

## Bring your old data across

Settings → **Import backup** → pick `sanctum-backup-2026-07-28.json`.

The old format is read automatically. Your 2 July Push session comes across with all
12 sets intact. The 20 July session — every exercise skipped, zero volume — is imported
as *abandoned* rather than completed, so it stops inflating your history.

## Where the data lives

IndexedDB, on the phone, inside the web app's storage sandbox. Nothing leaves the device
and there is no account or server.

The trade-off: **delete the home-screen icon and the data goes with it.** Export a backup
now and then — Settings → Export backup — and drop it in iCloud Drive.

## What changed from the old app

- Routine is the 4-day Upper / Lower / Upper / Lower from Sanctum_V, with the
  chest 14 / back 14 / glutes 13 weekly set balance intact.
- Every exercise shows what you lifted last time, so progressive overload at 0–1 RIR
  has an actual reference point instead of memory.
- Rest timer starts automatically on each logged set, using the prescribed rest for that
  exercise (3 min on compounds, 90s on accessories). It is driven by a timestamp, so it
  stays accurate when the screen locks.
- Weekly hard-set count per muscle on the home screen. Shared-target exercises
  (Bulgarian split squats, RDLs) count a half set to each muscle.
- Deload weeks are detected from the cycle start date and halve every prescription.
- A session with no completed sets can no longer be saved as "completed" — that was the
  bug behind the 20 July entry.
