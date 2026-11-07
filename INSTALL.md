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

**Calendar** shows the month with every trained day outlined in crimson — one dot per
session, so a double day is visible at a glance. Tapping a day opens that session; if there
were two, it offers both. Totals for the month sit underneath, and the arrows move between
months.

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

A **record** means your best single set on that exercise, by weight × reps — see
*Best set, not estimated 1RM* below for the full rule. The first time an exercise is
logged counts too, which is how Hevy behaves — expect inflated numbers for the first
fortnight until you have history to beat.

## Swap, notes, delete

**Swap** — a button on every exercise during a session, for when a machine is taken. It
offers the same-muscle exercises from your *other two* workouts of the same kind (a back
exercise in Upper A offers the back exercises from Upper B and C; Lower works the same
way). The like-for-like slot comes first under *Closest match*, the rest under *Other …
exercises*. A swap is for that session only: your program is never changed, the swapped
exercise shows *In place of …*, and History records what you actually did and what it
replaced. The substitute counts toward the same muscle in Volume, brings its own reps and
rest from its home workout, and keeps its own last-time reference and records.
Swap disappears once you've logged a set on that exercise — untick the set to bring it
back — and *Restore original* is always the first option on a swapped exercise. Adductors,
calf raises and cable crunches have no Swap because all three lower days use the same one.

**Notes** — a *Note* button on every exercise. A note belongs to the exercise, not the
workout: write "seat 4, pad on 3rd hole" once and it shows under that exercise every time
it appears, in any workout. Tap the note to edit it; empty it to remove it. Notes are
stored separately from sessions, so deleting a session never touches them, and they are
included in **Export backup** and restored by **Import backup** (a note already on the
phone is never overwritten by a backup). The session-wide note on the summary screen is
separate and unchanged.

**Delete session** — open any session from History or Calendar and press-and-hold
**Hold to delete** for 1.5 seconds. A tap, an early release, or sliding your thumb off
cancels it. Deleting removes the session from Volume, from the baseline records are
measured against (a stray heavy set can no longer raise the bar), and from the queue —
if it was the most recent upper or lower, the queue steps back one, so an accidental
session doesn't advance your rotation. It can't be undone, so export a backup first if
you're unsure.

## Custom workouts and cardio

**Custom workout** — a button on the home screen, next to *Log cardio*. Choose Upper or
Lower, and it drops you straight into a session with no exercises in it. From there,
**+ Add exercise** works exactly like it does mid-session below: pick a muscle group, pick
an exercise, set sets/reps/rest, repeat. A custom workout is invisible to the Upper/Lower
queue — it never advances or interrupts the A/B/C rotation — but it counts fully toward
Volume, History and Calendar, because the sets you log are real.

**Add exercise** — the same picker, now also available at the bottom of *every* session,
prescribed or custom. Choose a muscle group, choose an exercise from that muscle's list
(your program's own exercises across all three variants, plus the exercise catalog below),
then confirm or adjust the sets/reps/rest before it's added. An exercise added this way
isn't swappable — Swap only applies to the program's own prescribed slots — but everything
else about it (logging, notes, last-time, best-set) works the same as any other exercise.

**Log cardio** — pick an activity (Walking, Martial arts / boxing, Cycling, Swimming, Yoga,
or Other with your own name) and enter the minutes spent. It saves straight away — no
session screen, no sets. A cardio entry shows up in History and on the Calendar like any
other day, but it's left out of Volume entirely (no muscle, no sets, no tonnage — that tab
is specifically about lifting).

## Best set, not estimated 1RM

A **record** now means the best single *set* you've ever logged for that exercise, ranked
by weight × reps: 12 kg × 12 beats 12 kg × 11, and either beats 10 kg × 20, full stop — no
Epley estimate folding weight and reps together behind the scenes. This shows up three
places: the live crimson highlight while you're training, the record list on the session
summary and share card (now shown as the actual weight × reps, not "+X est. 1RM"), and the
crimson-outlined set in History detail.

Every exercise during a session now shows two reference lines — **Last**, the most recent
time you logged it, and **Best**, the highest-volume set you've ever logged for it — both
searched across every workout it appears in, not just the one you're doing today. Do
Machine Chest Press as a swap in Upper B today, then again as a swap in Upper A next month,
and Best still reflects the true all-time number either way.

## Exercise catalog and renames

Twelve new exercises are in the database for Add exercise and Swap, filed under their
muscle (not added to any day's prescribed routine): **Glutes** — DB Walking Lunges, Single
Leg Step Ups, Reverse V Squat, Single Leg 45° Hyperextensions, Pit Shark RDL, B-Stance Hip
Thrust, Plate Loaded Abductor Machine, Machine Glute Kickback; **Back** — Plate Loaded Lat
Pulldown, Plate Loaded Pronated Chest Supported Row, Plate Loaded Neutral Chest Supported
Row. They show up as Swap options too, always under *Other … exercises* since they have no
natural "closest slot" in your routine.

Barbell Hip Thrust is now **Machine Hip Thrust**, and the three separate Abductor Machine
variants (Upright / Lean Forward / Lean Back) are now one **Abductor Machine** — all your
history, notes and records carry over under the new names. In Lower C, FFE Barbell Reverse
Lunge is now **FFE DB Reverse Lunge**; this one is tracked as a distinct exercise rather
than merged with the old barbell version, since the load isn't comparable.

Twelve more exercises joined the catalog in v20, same treatment — Swap and Add exercise
only, no prescribed routine slot changed: **Shoulders** — Machine Shoulder Press, Plate
Loaded Machine Shoulder Press, DB Lateral Raises; **Chest** — Plate Loaded Machine Chest
Press, Plate Loaded Incline Chest Press; **Back** — Neutral Grip Pull Ups, Chin Ups;
**Glutes** — KAS Glute Bridges, 1/4 Machine Hip Thrusts, Leg Press - Feet High and Wide,
Reverse Hack Squats.

## Unilateral exercises and per-side volume (v20/v21)

Some exercises are logged one side at a time — a single dumbbell, one arm on a cable, one
leg — and the number you type doesn't always mean the same thing. For the 17 exercises
below, the weight field is now labeled **kg/side** instead of kg: you keep typing the same
number you always have (the load on one arm/dumbbell), but behind the scenes the app now
counts both sides for Volume, tonnage, and personal records. Your entered weight and reps
still display exactly as logged everywhere in the app — only the record-keeping math
changed.

**kg/side exercises** (finalized from the exercise-review sheet): Single-Arm Lat Pulldown,
Bayesian Cable Curls, Dumbbell Hammer Curl, Incline DB Bicep Curls, High-to-Low Cable Fly
w/ Press, Low-to-High Cable Fly, B-Stance Romanian Deadlift, DB Walking Lunges, Machine
Glute Kickback, Single Leg Step Ups, Single-Leg Leg Extension, Cable Lateral Raises, DB
Lateral Raises, Dumbbell Y-Raises, Single Arm Rear Delt Fly, DB Skull Crushers, Single Arm
Tricep Pushdown. Everything else (B-Stance Hip Thrust, DB Bulgarian Split Squat, and the
rest) was deliberately marked *not* unilateral-for-volume-purposes — either the weight you
log there is already a shared/total reading (a barbell, a machine stack), or you confirmed
it should stay as-is.

## Bringing the corrected historical data across (one-time, v21)

The exercise-review sheet also carried **weight corrections**: several exercises had been
logged under the old "total, not per-side" convention, so their historical weight entries
needed halving to match the new kg/side convention — e.g. Cable Lateral Raises' logged
46 kg becomes the true per-side 23 kg. B-Stance Romanian Deadlift's sets had both weight
*and* reps halved (60×24 → 30×12), since the old entries combined both sides into one
number on both counts. One exercise was also **reclassified**: the 160×20 sets logged as
Machine Hip Thrust on 2026-11-03 were actually a KAS Glute Bridges substitution, so that
entry now lives under its own exercise, and the stale note is gone.

This can't go through the normal **Import backup** — that only fills in sessions by ID that
don't already exist on your phone, so it would skip every one of these corrected sessions
since you already have them logged. To bring the corrected numbers across:

1. Settings → **Export backup**, just as a fresh safety copy of what's on your phone right now.
2. Settings → **Erase all data** (this clears sessions, notes, and the cycle — that's expected).
3. Settings → **Import backup** → pick the corrected file I sent you.

Everything comes back exactly as before except the exercises named above, which now carry
their corrected numbers — and the Volume tab's totals for any affected session are
recalculated to match.

**One thing I didn't touch:** Single-Arm Lat Pulldown's most recent session (2026-11-02,
second set) is logged as **100 kg × 100 reps**, which both the pre- and post-correction
data carry forward as-is — that's an existing typo in your logging, not something the
correction touched, and with the new doubling it'll show up as an inflated all-time Best
until you fix it (edit that set in History, or just log a clean one to overtake it).

## What changed from the old app

- Routine is six workouts — Upper A/B/C and Lower A/B/C. Upper sessions reorder three
  body-part blocks (chest, back, shoulders); Arms always close. Each set owns a lead:
  **Upper A opens with chest, Upper B with back, Upper C with shoulders.** Sets go
  A → B → C every upper session, so the lead rotates evenly — any three uppers in a row
  have three different leads, and a week of two uppers never repeats one.
- What varies is the order of the other two blocks. It flips direction every lap (each
  time Upper A comes round again): one lap goes chest → back → shoulders style, the next
  reverses it. That gives six distinct upper sessions — every ordering of the three
  blocks — repeating every six uppers. The queue shows the full order, e.g.
  *Upper A · Chest → Shoulders → Back*.
- The app doesn't need to know about two-upper and three-upper weeks. The queue simply
  runs on across them.
- Five sessions a week, alternating upper and lower, same as before. Everything is derived
  from your actual session history, so overriding the suggestion (jumping to any workout in
  the queue) doesn't need a reset — the next suggestion just branches from whatever you
  actually did.
- The home screen shows **Next up** as before, and below it a numbered **Queue** — a
  forecast of the next five sessions in order, assuming you follow the suggestion each
  time. Any row starts that session directly, same as the old alternates grid, just
  vertical instead of a 2-up grid.
- Tracking is now one-set-one-set, no half credit. Every exercise names exactly one
  muscle. On the four opening exercises of every Lower day (hip thrust, the squat/lunge
  variant, the hinge variant, the abductor variant) that muscle is Glutes, even where the
  movement is quad- or hamstring-dominant — Belt Squat and Bulgarian Split Squats both
  show GLUTES on screen and in the Volume tab, by design. Rear-delt exercises are folded
  into Shoulders the same way.
- Volume tracks ten muscles: Chest, Back, Shoulders, Biceps, Triceps, Glutes, Quads,
  Adductors, Calves, Abs. Hamstrings and Rear Delts are no longer tracked separately.
- Sessions logged before this change still say "Rear Delts" or "Hamstrings" in their
  stored data — that's an honest record of what the exercise was tagged at the time, so
  it isn't rewritten. Instead, anywhere a target is read or displayed, those two retired
  names are folded live into Shoulders and Glutes: the Volume tab counts them correctly,
  and History shows the current name rather than the old one. Nothing before this point
  needs re-logging.

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

A **record** means your best single set on that exercise, by weight × reps — see
*Best set, not estimated 1RM* above for the full rule. The first time an exercise is
logged counts too, which is how Hevy behaves — expect inflated numbers for the first
fortnight until you have history to beat.

## What changed from the old app

- Routine is six workouts — Upper A/B/C and Lower A/B/C — eight exercises each, two sets
  each, sixteen sets a session, roughly 50 minutes. 6-10 reps with 3 min rest on the heavy
  lifts, 10-15 (12-15 on lowers) with 2 min on the rest.
- Five sessions a week, alternating upper and lower. The A/B/C queues run continuously
  rather than resetting each week, so a week holding three uppers is followed by one
  holding two. The home screen computes what's next from your history and shows it as
  **Next up**; the other five sit below it if you want to override.
- Barbell Hip Thrust opens all three lower days, and Machine Hip Adduction, Seated Calf
  Raise and Cable Crunch close all three. The "last time" reference prefers the same
  workout letter, falling back to another and labelling it "other day".
- **Volume** is its own tab: hard sets per muscle over a rolling seven days, plus sessions,
  sets and tonnage for that window. Bars scale to your highest muscle, not to a target.
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

- Older sessions that recorded a lead as a number rather than a full order still read
  correctly, and a workout that was mid-session when the app updated resumes with its
  original exercise order.
