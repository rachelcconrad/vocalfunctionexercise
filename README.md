# Vocal Function Exercises — Home Practice App

A progressive web app (PWA) for guided home practice of Vocal Function Exercises (Stemple Method), designed for use in a clinical voice therapy context. Built for the UC San Diego Center for Airway, Voice, and Swallowing (CAVS).

---

## What It Does

This app walks patients through all four Vocal Function Exercises in a single guided session. It uses the device microphone to provide real-time pitch monitoring and automatic exercise tracking — patients do not need to tap any buttons to log their practice.

### Exercises (Stemple Method)
1. **Warm-Up** — Sustain "eee" on a target pitch (F4 female / F3 male)
2. **Stretch** — Glide from lowest to highest pitch on "whoop" or "null"
3. **Contract** — Glide from highest to lowest pitch on "boom" or "null"
4. **Power** — Sustain each note of the C–D–E–F–G scale on "old" or "knoll"

Patients practice **2 sets of each exercise, twice daily, 5 days per week** for 5–8 weeks.

---

## Features

- **Guided sequential flow** — one exercise at a time, app advances automatically on completion
- **Real-time pitch monitoring** — live Hz readout, scrolling pitch trace, and color-coded pitch bar (green = on target, amber = close, red = off target)
- **Automatic phonation detection** — timer starts and stops based on voice activity; valid sets are logged without any button press
- **Tone reference** — tap any target note button to hear a 2-second sine tone at the correct pitch
- **Per-note Power tracking** — each of the 5 scale notes tracked independently with its own set counter
- **Personal best** — phonation time records stored locally per exercise
- **Session streak** — daily practice streak tracked across sessions
- **Twice-daily reminders** — optional browser push notifications at user-set AM and PM times
- **Offline capable** — service worker caches all assets for use without internet after first load
- **Installable PWA** — can be added to home screen on iPhone (Safari) and Android (Chrome)

---

## Validation Criteria

| Exercise | Valid Set Criteria |
|---|---|
| Warm-Up | ≥ 3 seconds of sustained phonation |
| Stretch | Pitch sweep spanning ≥ 8 semitones, upward direction |
| Contract | Pitch sweep spanning ≥ 8 semitones, downward direction |
| Power (each note) | ≥ 3 seconds of sustained phonation per note |

---

## Pitch Targets by Voice Type

| Exercise | Female | Male |
|---|---|---|
| Warm-Up | F4 (349 Hz) | F3 (175 Hz) |
| Power scale | C4–D4–E4–F4–G4 | C3–D3–E3–F3–G3 |

---

## File Structure

```
vfe-pwa/
├── index.html        # Full application (single-file)
├── manifest.json     # PWA manifest (name, icons, theme color)
├── sw.js             # Service worker (offline caching)
└── icons/
    ├── icon-192.png  # Home screen icon (192×192)
    └── icon-512.png  # Splash screen icon (512×512)
```

---

## Deployment (GitHub Pages)

1. Fork or create a new **public** repository on GitHub
2. Upload all files — `index.html`, `manifest.json`, `sw.js`, and the `icons/` folder — to the root of the `main` branch
3. Go to **Settings → Pages**, set source to **main / (root)**, and click Save
4. Your app will be live at `https://your-username.github.io/your-repo-name/` within ~60 seconds

### Pushing Updates

After any code change:
1. Replace the relevant file(s) in the GitHub repo (commit to `main`)
2. Bump the cache version in `sw.js` — change `vfe-v3` to `vfe-v4` (or increment) so installed users receive the update rather than serving stale cached files

---

## Installing on a Patient's Phone

**iPhone / iPad (Safari only):**
1. Open the app URL in Safari
2. Tap the Share button (box with arrow)
3. Tap "Add to Home Screen"
4. Tap "Add"

**Android (Chrome):**
1. Open the app URL in Chrome
2. Chrome will show an install prompt automatically, or tap the three-dot menu → "Add to Home Screen"

> **Note:** Microphone permission must be granted each session on iOS Safari. This is an Apple platform restriction and cannot be overridden by the app.

---

## Browser Compatibility

| Browser | Pitch monitoring | Tone playback | Notifications | Install as PWA |
|---|---|---|---|---|
| iOS Safari | ✓ | ✓ | ✓ | ✓ |
| Android Chrome | ✓ | ✓ | ✓ | ✓ |
| Desktop Chrome | ✓ | ✓ | ✓ | ✓ |
| Desktop Firefox | ✓ | ✓ | ✓ | — |
| Desktop Safari | ✓ | ✓ | — | — |

---

## Technical Notes

- Pitch detection uses **autocorrelation** on raw PCM audio from the Web Audio API. Works well for sustained vowels and glides; accuracy is best in quiet environments.
- All session data (sets completed, personal bests, streak) is stored in **localStorage** — it is device-local and never transmitted anywhere.
- The app has **no backend, no login, and no data collection**. It is a fully static client-side application.
- AudioContext is created fresh for each tone playback event to comply with iOS Safari's strict user-gesture requirements for Web Audio.

---

## Clinical Context

Developed for patient home practice support at the **UCSD Center for Airway, Voice, and Swallowing (CAVS)**. This is not an official UC San Diego Health product. For clinical questions about Vocal Function Exercises, refer to:

> Stemple JC, Lee L, D'Amico B, Pickup B. *Efficacy of vocal function exercises as a method of improving voice production.* Journal of Voice. 1994;8(3):271–278.

---

## Development

Built with vanilla HTML, CSS, and JavaScript — no frameworks or build tools required. To make changes, edit `index.html` directly in any text editor and re-upload to GitHub.
