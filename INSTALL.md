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

## Identity

Mark and wordmark are **traced from your own reference**, not set in a substitute typeface.
I isolated the crimson pixels from the screenshot, upscaled and smoothed them, and ran the
result through potrace; the vector reproduces the source at 98.2% pixel overlap for the S.
Both live in the page as inline SVG paths, so nothing downloads at runtime and they render
offline like everything else.

Palette sampled from the same screenshot: crimson `#B92022`, gold `#CDAB58`, ground
`#0A0A0C`. The gold lozenge sits at 53.4% across and 49.6% down the S, matching the
reference. Gold is reserved for the volume figure and nothing else.

Because the mark is now traced rather than set in UnifrakturCook, the SIL Open Font Licence
no longer applies to it. It's your artwork, so nothing is owed — but if the original letter
came from a commercial typeface, check that font's licence before putting the mark on
merchandise.

## Session summary and history

Finishing a session shows the summary: mark, wordmark, *Progress vaulted.*, the volume in
gold, then exercises / sets / duration, a Notes field and Save.

**Save only commits the note.** The session itself is written the moment you press Finish,
so quitting the app on the summary screen can never lose a workout.

In **History**, tapping any session opens it in full — every exercise with each set as
`weight × reps`, the set that set a record outlined in crimson, and your note at the end.

## Session card

Finishing a session lands on a summary screen — duration, volume, records, sets — with a
**Make card** button. That opens the camera or photo library straight away. Your photo is
the subject; the session data sits over it as an overlay: small mark and wordmark top left,
then day, date, and the three stats along the bottom.

- **9:16 / 4:5** toggles between an Instagram story and a feed post.
- **Retake** swaps the photo.
- **Share** hands the image to the iOS share sheet — Save Image, Instagram, Messages.
  If the sheet isn't available, press and hold the image to save it.

Legibility is handled with two soft gradients at fixed pixel offsets plus a shadow on every
glyph, so the type survives a white gym wall while the middle of the photo stays untouched.
Measured against a deliberately blown-out test image it holds 3.2:1 on the wordmark and
4.3:1 on the stats in both formats.

A **record** means you beat your own previous best on that exercise, measured by estimated
1RM (Epley), so an extra rep counts as progress the same way extra weight does. The first
time an exercise is logged counts too, which is how Hevy behaves — expect inflated numbers
for the first fortnight until you have history to beat.

## What changed from the old app

- Routine is the 3-day specialisation: Day I leads with chest, Day II with back, Day III
  with glutes, and every day opens with a shoulder movement while you're fresh. Seven
  exercises a day, 17 sets, roughly 64 minutes. Weekly: chest 14, back 14, glutes 14,
  shoulders 9.
- Weekly set counting credits the first listed muscle in full and any second muscle at a
  half set, so a hip thrust counts as a whole glute set rather than a shared one.
- Every exercise shows what you lifted last time, so progressive overload at 0–1 RIR
  has an actual reference point instead of memory.
- Rest timer starts automatically on each logged set, using the prescribed rest for that
  exercise (3 min on compounds, 2 min or 90s on accessories). It appears as a centred
  dialog with the countdown, +30s and Skip. Tapping outside hides it while the clock keeps
  running. It is driven by a timestamp, so it stays accurate when the screen locks.
- Weekly hard-set count per muscle on the home screen. Shared-target exercises
  (Bulgarian split squats, RDLs) count a half set to each muscle.
- Deload weeks are detected from the cycle start date and halve every prescription.
- A session with no completed sets can no longer be saved as "completed" — that was the
  bug behind the 20 July entry.
- Finishing a session needs a deliberate 1.1 second press on **Hold to finish**, with a
  fill that runs across the button as you hold. Releasing early, or sliding your thumb off
  the button, cancels it. A stray tap can no longer end a workout.
