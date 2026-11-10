# جدول تدريب محمد – Mohammed's Training Plan

Project memory for Claude. Read this before changing anything here.

- Live app: https://mohammeee9d.github.io/training/ (GitHub Pages from `main`, root folder)
- First built: Nov 8, 2026 (Claude session: https://claude.ai/code/session_01Fh6CCsUGv488ShNf6h7iSU)
- Owner: Mohammed. Talk to him in Saudi Arabic, short and direct. He opens the app on an iPhone 13 Pro Max and an Honor Magic 5, saved to the home screen; rarely on a laptop.

## What the app is

One file: `index.html` (inline CSS + JS, no build step). Also `manifest.webmanifest` and `icon-*.png` for "Add to Home Screen". The plan the app starts from is in the `DEFAULT` object in `index.html`; `README.md` holds the same plan as plain text to copy.

Features he asked for (keep them working):
- Push / Pull / Legs / Rest cycle; suggests today's day from the last logged day.
- Every exercise shows the Arabic and English name, target sets × reps, and last time's weight × reps. Inputs are pre-filled (placeholders) from last time; ✓ logs a set.
- ✕ deletes a set logged by mistake. "+ more sets" works by logging past the target.
- Goals with a ✓ when met: per exercise, per day (iron, cardio, meals), morning weight, and 95.5 → 75 kg.
- Rest countdown starts automatically when a set is logged: compound 180 s, isolation 90 s (the top of each range). Beeps and vibrates at zero, then counts overtime. Tries to keep the screen awake.
- Weekly report: % for iron, cardio, meals and an overall % per day and per week, average weight vs the week before. Share (Web Share → WhatsApp), copy, CSV download. Days before the first logged day are not counted.
- "تعديل" (edit) mode edits everything in place, with no separate settings page: titles, start/goal weight, rest times, exercises (add, delete, reorder, sets, reps, compound flag), muscle groups, cardio, meals.
- YouTube technique button opens the YouTube app on phones (iOS `youtube://`, Android `intent://`) and the browser on a laptop.
- Sync between devices through a private GitHub Gist (`mohammed-training-data` / `training.json`) with a classic token that has only the `gist` scope, stored per device in localStorage. Merge rule: settings and plan by `ts`, each day's log by its own `ts`. The sync sheet shows the exact error text when it fails. Pasted tokens are cleaned of hidden characters (this broke the first try).

Data model (`localStorage["mtraining.v1"]` and the gist): `{v, settings:{ts,...}, plan:{ts, days:{push,pull,legs,rest}, cardio, restCardio, meals}, log:{"YYYY-MM-DD":{day, ts, sets:{exId:[{w,r}]}, notes, cardio, meals, weight}}}`. Exercise ids are stable keys for history; never rename an id.

## How to ship a change

1. Edit `index.html`, then `node --check` the extracted script.
2. Commit as `mohammeee9d` and push to `main`. Pages redeploys in about a minute; phones may keep the old copy for about 10 minutes, so tell him to fully close the home-screen app and reopen.
3. The session's GitHub proxy blocks the Pages settings API; he turned Pages on himself.

## His plan (as of Nov 2026)

- Goal: 95.5 kg → 75 kg as fast as possible while keeping muscle; fine with hard training. InBody Nov 2, 2026: 95.5 kg, 33.3% fat (31.8 kg), skeletal muscle 36.6 kg, visceral fat level 12.
- Cutting plan started Nov 9, 2026. Split agreed: main muscle 4–5 exercises, side muscles about 2.
  - Push: Bench 3×6–10, Incline DB 2×8–12, Machine Chest 2×10–12, Pec Deck 2×12–15, DB Lateral 2×12–15, Cable Lateral 2×12–15, Pushdown 2×10–15, Overhead Cable Ext 2×10–15
  - Pull: Lat Pulldown 3×8–12, Chest Supported Row 2×8–12, Seated Cable Row 2×10–12, Straight Arm Pulldown 2×12–15, Reverse Pec Deck 2×12–15, Barbell Curl 2×8–12, Hammer Curl 2×10–15, Cable Crunch 2×12–15
  - Legs: Squat 3×6–10, RDL 2×8–12, Leg Extension 2×12–15, Lying Leg Curl 2×10–15, Standing Calf 2×12–15, Seated Shoulder Press 2×8–12, DB Lateral 2×12–15, Hanging Leg Raise 2×10–15
  - Rest: light walk 30–45 min
  - Cardio after weights, 50 min: incline walk 20, bike 15, elliptical 15
- Warm-up: his usual 8 min brisk walk, 2 min joint mobility for the day, then 2 light ramp-up sets before the first compound lift.
- Effort: compounds stop with 1–2 reps left in the tank; isolation last set close to failure; add weight once the top of the rep range is hit on every set.
- Meals (his own plan, don't change it unless he asks): 2× quarter grilled chicken, skinless + 250 g cooked rice; tuna in water + Nada 0% Greek yogurt; chicken Caesar salad without dressing or cheese; whey with water. Estimated about 1,750–1,950 kcal and 185 g protein (unverified against labels). He has cut sugar completely; tea without sugar. He's fine eating the same meals for weeks.
- Swaps discussed: liver plate (about 200 g, light oil, one bread) or a restaurant burger can replace one or two of the rice + chicken meals; no fries, ketchup or soda.
- Watch: Xiaomi Redmi Watch 5 Active (no third-party apps). Advised turning on Mi Fitness → Apple Health sync. A real HealthKit link would need a native wrapper (Capacitor + Xcode); not built.

## Ideas he showed interest in, not built yet

- Body section: daily weight chart plus InBody entries (fat vs muscle over time).
- Fields for watch data per session (duration, average heart rate, calories).
