# AGENTS.md

## Cursor Cloud specific instructions

### Overview
This is "GET RICH — The Clicker", a single-file browser-based incremental/clicker game. The entire application lives in `index.html` (HTML + CSS + JS inline). There is no build step, no package manager, and no local dependencies.

### Running the dev server
Serve the project root with any static HTTP server:
```
python3 -m http.server 8000 --directory /workspace
```
Then open `http://localhost:8000` in Chrome. Click **"Play offline (no cloud save)"** to bypass the Supabase login screen.

### Lint / Test / Build
- **Lint**: No linter is configured. For ad-hoc checks, use `npx htmlhint index.html` or similar.
- **Tests**: No automated test suite exists.
- **Build**: No build step — the app is a single static HTML file.

### External dependencies
- **Supabase** (remote, `nhfzdofkbunpkpqtnbzx.supabase.co`): provides auth, cloud saves, leaderboard, and email subscribers. The app falls back to `localStorage` when Supabase is unavailable, so no credentials are needed for local development.
- **Google Fonts** and **Supabase JS SDK** are loaded via CDN at runtime.

### Key caveats
- Game state is serialised to `localStorage` under the key `getrich_save_v5`. Clearing browser data resets progress.
- The save key changed from `v4` to `v5` with the monetization update. State migration handles missing fields automatically.
- The login/auth screen appears first; always use the offline/guest mode button for local testing.
- The shop uses email capture instead of demo-mode free purchases. All paid items show the subscription form.
- Energy system: 100 max, 1 per click, refills 1 every 2 minutes. Flash events may bypass energy costs.
