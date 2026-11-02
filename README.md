# LCFC Manager

**Lake Champlain Foosball Club** — tournament operations, live TV board, stats, and club ranking in a single web app.

| | |
|--|--|
| **Current version** | v7.14 |
| **Stack** | Single-file HTML / CSS / JavaScript (Tailwind CDN, Chart.js) |
| **Data** | Browser `localStorage` + optional JSON import/export / GitHub Pages `data/latest.json` |
| **Hosting** | Static (GitHub Pages, any static host, or open `index.html` locally) |

---

## What it does

LCFC Manager runs weekly club nights end-to-end:

- Create **Singles**, **Doubles**, **DYP**, and **Monster DYP** events  
- Draw partners, assign tables, enter scores (including OT win-by-2)  
- Run **double-elimination** playoffs with seeds and brackets  
- Drive a **TV / spectator board** (castable, multi-event)  
- Track **career stats**, **club ranking points**, awards, and player profiles  
- Operator PIN protects scoring and admin actions; members can view published data  

---

## Event types

| Type | Description |
|------|-------------|
| **Singles** | 1v1 bracket (club ranking seeds when starting bracket-only) |
| **Doubles** | Fixed teams; club ranking team strength for bracket seeds |
| **DYP** | Draw Your Partner; random partners; bracket seeding by club ranking when no ranking rounds |
| **Monster DYP** | Ranking rounds (fair sit-outs, partner rotation) → **tiered** playoff partners → double-elim |

### Monster specifics

- Ranking rounds on limited tables (sit-out fairness: no one sits twice until everyone has sat once)  
- Partner draws avoid repeat partners until the field has cycled  
- **Tiered playoffs:** top half of standings pairs with bottom half (e.g. 1+6, 2+7, …)  
- Playoffs default to **best of 3**  
- Optional **absent** status so players leave before playoffs without wiping ranking history  

### Formats & scoring

- Race-to (default **5**)  
- Best-of-1 / best-of-3 / best-of-5 series  
- **OT toggle:** win-by-2 (e.g. 7–5, 8–6)  
- Quick-score chips + typed scores  
- Coin toss / serve indicator  
- Match timers (start after draw / table free; Hare & Tortoise awards)  

---

## Bracket & playoffs

- **Double elimination** tree (winners / losers / grand final)  
- Standard bracket placement (1 vs last, etc.)  
- Seeds shown on TV playoff cards  
- Table assignment + on-deck queue across matches  
- Multi-event **conflict lock** (player in a live match elsewhere)  
- Delete drawn matches when needed  

---

## Club ranking

Starts every player at **2000** points (bands: Beginner → Master).

### When points change

Only from **finished bracket / playoff** results (not ranking-round matches alone). Sandbox events are excluded.

### Formula (per player)

```
Δ = seed adjustment (±8 per placement tier) + podium bonus (1st / 2nd / 3rd only)
```

- **Seed adjustment:** expected place vs actual finish (tier bands: 1 · 2 · 3–4 · 5–8 · …)  
- **Playoff teams:** partners share the **same** Δ (team seed + shared bonus)  
- **Bonus pool:** locked at **playoff create** = **1%** of combined ranking points of the playoff field  
- **Split:** operator toggle **50/30/20** or **60/30/10** (shares always sum to the pool)  

Control center shows the **locked** pool and 1st/2nd/3rd shares once playoffs exist.

### Recalculate

Operator can **recalculate ranking from events** to rebuild points from history after logic changes.

---

## Operator mode

- PIN: **111784** (same PIN toggles on/off)  
- Enables import/export, destructive actions, ranking split toggle, recalculate  
- Members see read-only published club data with a clear viewing badge  

---

## TV / spectator board

- Open from **home** (all active events) or **inside an event**  
- Can open in a **separate tab** for casting while the operator scores on another tab  
- Color bands by event type (e.g. Monster orange, DYP yellow, …)  
- Live / on-deck cards, table numbers, serve indicator, seeds on playoffs  
- Match timers, projected win %, optional **sound on** + match announcements  
- Sandbox watermark when applicable  
- Auto-refresh; announcement flow can pause refresh while speaking  

---

## Stats & player experience

### Stats

- Career leaderboard (points, then goal differential)  
- Per-event leaderboards  
- Charts / graphs (form, volume, etc.)  
- Best / worst partners  
- Fun awards (defaults + Hare / Tortoise, etc.)  
- **Club DNA:** totals, champions, avg match length, goals/night, shutouts, geography  

### Player profile

- Rank, ranking points, form  
- Podiums, rivals (**player one rank below** + pts ahead)  
- State / geography  
- Share-oriented card layout  

### Home

- Tournament cards with 1st / 2nd / 3rd  
- Version + last backup / club file timestamps  
- Theme & font options (Pitch default; Tornado, Fog, Arena, etc.)  

---

## Event control center

Live ops strip on the event page:

- Roster / completed / remaining / tables  
- Match completion progress  
- **Bonus point pool** (after playoffs start): locked total + 1st/2nd/3rd shares  

---

## Data & hosting

| Action | Notes |
|--------|--------|
| **Export** | Full club JSON backup |
| **Import** | Restore / merge club file |
| **GitHub Pages** | Host `index.html`; optional `data/latest.json` for members |
| **localStorage** | Working state on the operator device |
| **Sandbox events** | Full play + TV; **excluded** from official stats & ranking |

---

## Score entry (paper scoresheet UI)

- Light “club scoresheet” modal (not dark)  
- Quick score chips  
- OT win-by-2 validation  
- Series support for best-of-3 / best-of-5  
- Estimated win chance  

---

## Multi-event

- Several events can run the same night  
- Shared tables with occupancy / on-deck  
- Conflict highlighting when a player is live elsewhere  
- Home TV board aggregates all active events  

---

## Keyboard / mobile

- Works on desktop and phone browsers  
- iPhone: add to Home Screen or use Safari; operator typically runs laptop + TV cast  

---

## Versioning

`APP_VERSION` is shown on the home watermark and in export metadata. Bump all of:

- `APP_VERSION`  
- HTML comment / `lcfc-build` meta  
- `<title>`  
- Home watermark  

---

## Privacy & safety

- No server-side accounts required for core use  
- Operator PIN is a light gate, not strong security  
- Do not put real passwords or private keys in the JSON backup  

---

## Quick start

1. Open `index.html` (or your GitHub Pages URL).  
2. Enable **operator mode** (PIN) to score and manage.  
3. Add players → **Create tournament** → draw / play → playoffs.  
4. Open **TV board** on a second tab or display.  
5. **Export** a backup after the night.  

---

## Feature map (summary)

```
Events: Singles · Doubles · DYP · Monster DYP · Sandbox
Play:   Ranking rounds · Fair sits · Partner rotation · Tables · Timers
Bracket: Double-elim · Seeds · Tiered Monster pairs · Conflict lock
Score:  Quick chips · OT win-by-2 · Series Bo3/Bo5 · Coin / serve
TV:     Multi-event · Color bands · Announce · Live / on-deck
Rank:   2000 start · Locked bonus pool · Seed ±8 tiers · Equal partner Δ
Stats:  Career · Event · DNA · Awards · Profiles · Rival below
Ops:    PIN · Import/export · Control center · Recalculate ranking
```

---

## Club

**Lake Champlain Foosball Club (LCFC)**  
Built for weekly in-person foosball — not a generic SaaS bracket tool.

---

*README aligned with LCFC Manager v7.14.*
