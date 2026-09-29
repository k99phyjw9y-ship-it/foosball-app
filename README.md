# LCFC Manager

**Lake Champlain Foosball Club** tournament manager — a single-file web app for club nights.

**Current version:** v5.62 · Updated Sep 27, 2026

Run **Singles**, **Doubles (BYP)**, **DYP**, and **Monster DYP** with ranking rounds, double-elimination playoffs, club ranking, stats, coin toss / serve, conflict lock for parallel events, and a spectator TV board. All data stays in the browser (`localStorage`).

---

## Features

### Events
- **Singles**, **Doubles** (BYP fixed pairs), **DYP**, **Monster DYP**
- Ranking rounds with blank score entry (no suggested 0s)
- **Best of 1 / 3 / 5** series scoring (race-to per game; default race-to **5**)
- **Double-elimination** brackets on all playoff / bracket formats
- Bracket byes auto-expand for 6 / 10 / 14 players (no forced sit-outs for those sizes)
- Tiered Monster playoffs (top half × bottom half partners; always double elim; playoffs best of 3)
- Edit event name, date, tables count, race-to
- Mark tournament **finished** without a bracket if needed
- Sort events by creation date
- **Export / import** full backup JSON
- **Conflict lock** for parallel disciplines (Singles + DYP + BYP at once): only **live** matches block a player; waiting events get priority when a score is entered

### Monster DYP
- Fair partner rotation (avoid same partner until the pool cycles)
- Fair sit-out rotation when the field is not a multiple of 4
- Multiple of 4 (e.g. 12 players, 2 tables): **nobody sits** — matches fill in groups of 4 across tables
- Up to 3 sit-outs when 9–11 active players (2 tables)
- Optional **Forward / Goalie** random assignment on ranking draws
- Mark players **absent** (stats kept; skipped in draws / playoffs)
- Sit-out history preserved when the field changes; no one sits twice until everyone has sat once

### Brackets & playoffs
- View modes: **Tree**, **Columns**, **Stacked**, **Dual** (Winners | Losers), **List**
- Table assignment + on-deck queue; tables stay reserved until free
- Per-match **timer** (30s grace after draw / table goes live; not for pure on-deck until promoted)
- **Coin toss**: Heads/Tails assignment → Flip → serving team (match cards, score modal, TV board)
- Clear / delete matches; edit scores after the fact

### Club ranking
- Every player starts at **2000**
- Skill bands: Beginner → Rookie → Amateur → Expert → Pro → Master
- Points adjust on **bracket / playoff** results only (not ranking rounds)
- Partners on a podium team get **equal** 1st / 2nd / 3rd seed + bonus
- Rebuilds from existing and imported tournaments

### Stats
- Career leaderboard (all events; series goals = sum of each game, not series tally)
- Per-event leaderboards
- Standings sort: **points**, then **goal differential**
- Podium section (playoffs/brackets played + 1st / 2nd / 3rd counts)
- Designated position (F/G) stats when enabled
- Best / worst partners (including ranking rounds)
- Most improved, side-by-side player compare, last-10 form on player profile
- Fun awards (Sniper, Pin Cushion, **Hare** shortest match, **Tortoise** longest, and more)
- Charts on the stats page
- Projected match win % on score entry
- **Merge players** (e.g. typo duplicates) with full history rewrite

### Spectator / TV board
- Live + on-deck match cards; top-10 standings; room panel (playing / on deck / sitting out)
- Serve indicator on cards after coin toss
- Match timers; theme follows app color theme
- Auto-size names; compact layout for large screens
- **Cast tip:** open TV board in a **second browser tab/window** and Cast that window; keep score entry in the first (shared `localStorage` on the same device)

### UI
- Light mode; theme accents (green and related schemes)
- Mobile-friendly; add to iPhone Home Screen via Safari
- Version + last-updated watermark on the home screen
- Home event cards show 1st / 2nd / 3rd (horizontal, wrap/shrink names)
- Footer links to club / ITSF-related documents when configured

---

## Quick start

### Local
Open `index.html` in a browser, or serve the folder:

```bash
cd foosball-app
python3 -m http.server 8765
```

Visit `http://localhost:8765`.

### GitHub Pages (recommended for a shared club URL)

**Shortest URL** (`https://YOUR_USERNAME.github.io/`):

1. Create a repo named exactly **`YOUR_USERNAME.github.io`**
2. Put `index.html` at the **root**
3. **Settings → Pages → Deploy from a branch** → `main` / **/(root)**
4. Open `https://YOUR_USERNAME.github.io/`

**Repo URL** (`https://YOUR_USERNAME.github.io/REPO_NAME/`):

1. Push this project to any public repo  
2. **Settings → Pages → Deploy from a branch** (`main` + root or `/docs`)  
3. Open the URL GitHub shows  

Optional: **Custom domain** under Pages settings + DNS at your registrar.

### iPhone
1. Open the hosted site (or local URL) in **Safari**  
2. Share → **Add to Home Screen**  
3. Data stays on that device unless you Export / Import  

---

## Updating the app

1. Replace `index.html` with the new build (or `git pull` / push to Pages)  
2. Hard-refresh the browser (cache can keep an old file)  
3. Confirm the home watermark (e.g. `v5.62 · Updated Sep 27, 2026`)  
4. **Export** a JSON backup before major upgrades  

Import uses `LCFC_Manager_backup_YYYY-MM-DD.json` (or any prior export from this app).

### GitHub workflow
```bash
# after replacing index.html
git add index.html README.md
git commit -m "Update LCFC Manager to vX.XX"
git push origin main
```
Pages rebuilds in about a minute.

---

## Parallel events (conflict lock)

- Toggle **Conflict lock** on the event header when running more than one discipline.  
- A player is **busy** only while **live at a table** in another event (on-deck does not block).  
- Conflicted players stay in the bracket; their match shows **Waiting · conflict** (purple name highlight).  
- After a score is entered, **other events** claim free players first so one bracket does not monopolize the field.  

Each event still has its own **tables** setting — set capacity to match physical tables.

---

## Tech

| Item | Detail |
|------|--------|
| Stack | Single-page app: HTML + vanilla JS + Tailwind (CDN) |
| Storage | `localStorage` (players, tournaments, rankings, timers, preferences) |
| Server | None required for core use |
| Hosting | Any static host (GitHub Pages, Cloudflare Pages, Netlify, Vercel, …) |

No build step. Edit `index.html` and reload.

---

## Privacy & backups

All club data lives in the **browser on that device**. Clearing site data erases it.

- Use **Export** regularly (especially before major version upgrades).  
- Hosted sites do **not** sync devices automatically — Export on one device, Import on another.  

---

## Version notes (recent)

| Version | Highlights |
|---------|------------|
| **v5.62** | Tree bracket layout: larger non-overlapping slots, tappable Enter score |
| **v5.60–5.61** | Tree view for playoffs; layout fixes |
| **v5.57–5.59** | Virtual coin toss + serve (cards, modal, TV) |
| **v5.54–5.56** | Conflict lock fairness (live-only busy; multi-event priority) |
| **v5.48–5.53** | Parallel disciplines, hold-not-exclude, release after score |
| **Earlier 5.x** | Timers, Hare/Tortoise, merge players, TV room panel, series stats, tiered Monster playoffs |

---

## License

For Lake Champlain Foosball Club use. Adjust as needed for your organization.
