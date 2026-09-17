# LCFC Manager

**Lake Champlain Foosball Club** tournament manager — a single-file web app for club nights.

**Current version:** v5.17 · Sep 16, 2026

Run Singles, Doubles, DYP, and Monster DYP events with ranking rounds, double-elimination brackets, club ranking, stats, and a spectator TV board. All data stays in the browser (`localStorage`).

---

## Features

### Events
- **Singles**, **Doubles**, **DYP**, **Monster DYP**
- Ranking / Swiss-style rounds with score entry
- **Best of 1 / 3 / 5** series scoring (race-to per game)
- **Double-elimination** brackets with byes (e.g. 6 / 10 / 14 players expand; no forced sit-outs for those sizes)
- Tiered Monster playoffs (high seed × low seed partners)
- Edit event name, date, tables, race-to (default **5**)
- Mark tournament finished without a bracket if needed
- Export / import full backup JSON

### Monster DYP
- Fair partner rotation (avoid rematches until the pool cycles)
- Fair sit-out rotation when the field is **not** a multiple of 4
- When the field **is** a multiple of 4 (e.g. 12 players), **nobody sits** — extra matches rotate across tables (T1 → T2 → T1…)
- Optional **Forward / Goalie** random assignment on ranking draws
- Mark players **absent** without wiping career totals

### Club ranking
- Every player starts at **2000**
- Skill bands (Beginner → Master)
- Ranking points adjust on **bracket / playoff** results only
- Partners on a podium team share equal place seed + bonus

### Stats
- Career leaderboard (all events; series goals = sum of games)
- Per-event and week-over-week standings
- Podium counts (1st / 2nd / 3rd)
- Designated position (F/G) stats when enabled
- Best / worst partners (including ranking rounds)
- Most improved, side-by-side player compare, last-10 form
- Crazy Stats awards (Sniper, Pin Cushion, etc.)
- Charts (line, radar, bar, and related views)
- Projected match win % (estimate on score entry)

### Spectator / TV board
- Live standings + now-playing match cards
- Auto-size names; compact layout for large screens
- **Cast tip:** open the TV board in a **second browser window** and Cast that window; keep editing in the first (same laptop, shared `localStorage`)

### UI
- Light mode, emerald accent
- Mobile-friendly; add to iPhone Home Screen via Safari
- Version watermark on the home screen

---

## Quick start

### Local
Open `index.html` in a browser, or serve the folder:

```bash
cd foosball-app
python3 -m http.server 8765
```

Visit `http://localhost:8765`.

### GitHub Pages
1. Push this repo to GitHub  
2. **Settings → Pages → Deploy from branch** (`main` / root, or `/docs` if you use that)  
3. Open `https://YOUR_USERNAME.github.io/REPO_NAME/`

### iPhone
1. Open the site in **Safari**  
2. Share → **Add to Home Screen**  
3. Data stays on the device (browser storage)

---

## Updating the app

1. Replace `index.html` with the new build (or pull from git)  
2. Hard-refresh the browser (cache can keep an old file)  
3. Confirm the home watermark version (e.g. `v5.17 · Updated Sep 16, 2026`)  
4. Optional: **Export** a JSON backup before major upgrades  

Import uses the same backup format (`LCFC_Manager_backup_YYYY-MM-DD.json`).

---

## Tech

| Item | Detail |
|------|--------|
| Stack | Single-page app: HTML + vanilla JS + Tailwind (CDN) |
| Storage | `localStorage` key `foosmanager_v1` |
| Server | None required |
| Charts | Client-side (bundled in the page) |

No build step. Edit `index.html` and reload.

---

## Weekly release highlights

**Sep 15–16, 2026 (v5.16–5.17)**  
- Sit-outs only for remainder-of-4; 12 players / 2 tables → 3 matches, no sit-outs  
- Score modal names wrap / auto-fit  

**Sep 12–14, 2026 (v5.8–5.15)**  
- Best-of series scoring  
- Career GF/GA sum all games in a series  
- Designated Position GF/GA columns; watermark sync  

**Earlier**  
- Full tournament engine, club ranking, stats suite, TV board, export/import  

---

## Privacy

All club data (players, events, scores) lives in the **browser on that device**. Clearing site data erases it — use **Export** for backups.

---

## License

For Lake Champlain Foosball Club use. Adjust as needed for your organization.
