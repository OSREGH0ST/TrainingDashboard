# PPL-UL Workout Dashboard

Static PWA. No build step, no backend, no dependencies to install.

## Deploy (GitHub Pages)

```bash
git init
git add .
git commit -m "PPL-UL workout dashboard (PWA)"
git branch -M main
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```

Repo → Settings → Pages → Source: `main` branch, `/ (root)`.

## Install on Android (Poco X7 Pro / Chrome)

1. Open the Pages URL in Chrome.
2. Menu (⋮) → **Install app** / **Add to Home screen**.
3. Open it once more after install to let the service worker finish precaching.
4. From then on it runs fully offline — 0 MB of mobile data per session.

## Structure

```
.
├── index.html      # app shell + Alpine state + workout data + rest timer
├── manifest.json   # PWA metadata (name, icons, standalone display)
├── sw.js           # stale-while-revalidate cache, incl. Tailwind/Alpine CDN
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

## Notes

- Rest timer duration is read from each exercise's own `rest` field in
  `workoutData` (already varies 60s–180s by exercise), not a flat
  compound/isolation rule. Edit per-exercise if you want a different split.
- Progress (`completedSets`) is stored in `localStorage` — per device,
  per browser. No sync between phone and laptop without adding a backend.
- No Cloudflare Worker / backend in this build — everything here is static
  and client-side.
