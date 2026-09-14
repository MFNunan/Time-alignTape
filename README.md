# Time-alignTape — Delay Line

A small offline-first PWA that converts a linear throw distance (Imperial or
Metric) into a propagation delay in milliseconds, corrected for local
conditions.

## The math

Speed of sound uses the Bohn (1988) formula standard in AES live-sound
literature:

```
c = 331.3 + 0.606 * T + 0.0124 * RH
```

where `T` is air temperature in °C and `RH` is relative humidity in
percent. Temperature dominates; humidity is a small secondary correction.

Barometric pressure has a negligible *direct* effect on the speed of sound
in air — it cancels out of the ideal-gas relationship. Site altitude is
used only to estimate local barometric pressure via the International
Standard Atmosphere model, so you can log real site conditions with a
saved preset. Enter a live station reading to override the estimate.

Arrival time is throw distance ÷ corrected speed of sound.

Sources: D. Bohn, "Environmental Effects on the Speed of Sound," *J. Audio
Eng. Soc*, 1988 · ICAO Standard Atmosphere, 1993.

## Running locally

This is a static site — no build step.

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Installing as a PWA

Deploy `index.html`, `manifest.json`, `sw.js`, and `icons/` to any static
HTTPS host (GitHub Pages, Netlify, Vercel). Opening the deployed URL
directly (not embedded in an iframe) lets the browser offer "Add to Home
Screen" / "Install app", after which it works fully offline.

### GitHub Pages

1. Push this repo to GitHub.
2. Settings → Pages → Deploy from branch → `main` / root.
3. Visit the published `github.io` URL and install from there.
