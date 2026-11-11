# LCFC Manager

**Lake Champlain Foosball Club** — tournament operations, live TV board, stats, and club ranking in a single web app.

| | |
|--|--|
| **Current version** | v7.32 |
| **Stack** | Single-file HTML / CSS / JavaScript (Tailwind CDN, Chart.js) |
| **Data** | Browser `localStorage` + JSON import/export / optional GitHub Pages `data/latest.json` |
| **Hosting** | Static (GitHub Pages, any static host, or open `index.html` locally) |
| **Size** | ~15.6k lines (see home watermark) |

---

## What it does

LCFC Manager runs weekly club nights end-to-end:

- Create **Singles**, **Doubles**, **DYP**, and **Monster DYP** events  
- Draw partners, assign tables, enter scores (including OT win-by-2)  
- Run **double-elimination** playoffs with seeds and brackets  
- Drive a **TV / spectator board** (castable, multi-event, optional **Bar mode**)  
- Track **career stats**, **club ranking points**, awards, and player profiles  
- Operator PIN protects scoring and admin actions; members can view published data  

---

## Event types

| Type | Description |
|------|-------------|
| **Singles** | 1v1 bracket (club ranking seeds when starting bracket-only) |
| **Doubles** | Fixed teams; club ranking team strength for bracket seeds |
| **DYP** | Draw Your Partner; fair partner rotation; bracket seeding by club ranking when no ranking rounds |
| **Monster DYP** | Ranking rounds (fair sit-outs, partner rotation) → **tiered** playoff partners → double-elim |

### Monster specifics

- Ranking rounds on limited tables (sit-out fairness: no one sits twice until everyone has sat once)  
- Partner draws prefer never-paired partners until the active field has cycled (`fairPairPlayers` / partnership history)  
- **Tiered playoffs:** top half of standings pairs with bottom half (e.g. 1+6, 2+7, …)  
- Playoffs default to **best of 3**  
- Optional **absent** status so players leave before playoffs without wiping ranking history  
- Absent players appear **faded + “Absent” chip** on the standings table  

### Formats & scoring

- Race-to (default **5**)  
- Best-of-1 / best-of-3 / best-of-5 series  
- **OT toggle:** win-by-2 (e.g. 7–5, 8–6)  
- Quick-score chips + typed scores  
- Coin toss / serve indicator (auto on draw)  
- Match timers (start after draw / table free; Hare & Tortoise awards)  
- Series game scores feed career stats **per game**, not series tally alone  

---

## Bracket & playoffs

- **Double elimination** tree (winners / losers / grand final)  
- Standard bracket placement  
- Seeds shown on TV playoff cards  
- Table assignment + on-deck queue across matches  
- Multi-event **conflict lock** (player in a live match elsewhere)  
- Multi-event **fair table promote** (longest wait / mild event alternate) when 2+ active events  
- Delete drawn matches when needed  
- Finish paths keep **`status` and `winner` in sync** (including byes)  

---

## Club ranking

Starts every player at **2000** points (skill bands: Beginner → Rookie → Amateur → Expert → Pro → Master).

### When points change

Only from **finished bracket / playoff** results (not ranking-round matches alone). **Sandbox** events are excluded.

### Formula (per player)

```
Δ = seed adjustment (±8 per placement tier) + podium bonus (1st / 2nd / 3rd only)
```

- **Seed adjustment:** expected place vs actual finish (tier bands: 1 · 2 · 3–4 · 5–8 · …)  
- **Playoff teams:** partners share the **same** Δ (team seed + shared bonus)  
- Seeds backfilled from bracket sides when `playoffTeams` seeds are missing (imports / older events)  
- **Bonus pool:** locked at **playoff create** = **1%** of combined ranking points of the playoff field  
- **Split:** operator toggle **50/30/20** or **60/30/10** (shares always sum to the pool)  
- Apply prefers **exact locked shares** from the playoff-create snapshot  

Control center shows the **locked** pool and 1st/2nd/3rd shares once playoffs exist.

### Recalculate

Operator can **recalculate ranking from events** to rebuild points from history after logic changes.

---

## Operator mode

- PIN-gated (configured in app code — **not documented here**)  
- Same PIN toggles operator mode **on and off**  
- Enables import/export, destructive actions, ranking split toggle, recalculate  
- Members see read-only published club data with a clear viewing badge  

---

## TV / spectator board

- Open from **home** (all active events) or **inside an event**  
- Can open in a **separate tab** for casting while the operator scores on another tab  
- Color bands by event type (thicker on TV cards)  
- Live / on-deck cards, **table plates**, pulsing **SERVE** indicator, seeds on playoffs  
- Match timers, projected win %, optional **sound on** + match announcements  
- Partner names **stacked** (one player per line) on team cards  
- Sandbox watermark when applicable  
- Auto-refresh; announcement flow can pause refresh while speaking  
- **Live** pill on playing cards  

### Bar mode

Toggle on the TV board toolbar (persisted in `localStorage`):

| On | Off |
|----|-----|
| Larger live match cards (2–4 table layouts) | Standard grid + on-deck cards |
| Sidebar (room / standings) hidden | Sidebar available |
| **Next up** single-line scrolling ticker | Ticker hidden |
| On-deck card grid hidden | Full on-deck section |

Ticker only rebuilds when the on-deck list **actually changes** (stable under auto-refresh).

### Series-safe live board

Matches leave **Playing** only when finished (`status === 'done'` and/or `winner`).  
Mid-series scores (e.g. Bo3 at 1–0) **stay on the board**.

---

## Stats & player experience

### Stats

- Career leaderboard (points, then goal differential)  
- Per-event leaderboards  
- Charts / graphs (form, volume, etc.)  
- Best / worst partners (includes ranking rounds)  
- Fun awards (defaults + Hare / Tortoise, etc.)  
- **Club DNA:** totals, champions, avg match length, goals/night, shutouts, geography  

### Player profile

- Rank, ranking points, form  
- Podiums, rivals (player one rank below + pts ahead)  
- State / geography  
- Share-oriented card layout  

### Home

- Tournament cards with 1st / 2nd / 3rd  
- Version + last backup / club file timestamps + **lines of code** watermark  
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

## Score entry

- Light “club scoresheet” modal  
- Quick score chips  
- OT win-by-2 validation  
- Series support for best-of-3 / best-of-5  
- Estimated win chance  

---

## Multi-event

- Several events can run the same night  
- **Shared tables** with global occupancy (always tracked when 2+ active events)  
- **Fair promote:** longest-waiting on-deck matches across the club; mild alternate-event bias  
- Conflict highlighting when a player is live elsewhere (conflict lock setting)  
- Conflict clears only when the match is truly finished (not mid-series)  
- Home TV board aggregates all active events  

---

## Versioning

`APP_VERSION` is shown on the home watermark and in export metadata. Bump **all** of:

- `APP_VERSION`  
- HTML comment / `lcfc-build` meta  
- `<title>`  
- Home watermark  
- `APP_LINES` (set to actual file line count)

---

## Recent hardening (v7.29–v7.32)

- TV live filter: series mid-scores no longer drop matches  
- Ranking apply prefers locked bonus shares  
- `ensureMatchFinishedFlags` keeps `status` + `winner` aligned (scores + byes)  
- Seed backfill for older imports without `playoffTeams` seeds  
- Multi-event fair table promote after bracket assign  
- Conflict release no longer fires on mid-series score tallies  
- Global ranking table free on `status` **or** `winner`  
- Multi-event table share independent of player conflict lock  
- Stronger partnership history for fair DYP/Monster draws  

---

## Privacy & safety

- No server-side accounts required for core use  
- Operator PIN is a light gate, not strong security — **do not publish the PIN** in docs or public repos  
- Do not put real passwords or private keys in the JSON backup  

---

## Quick start

1. Open `index.html` (or your GitHub Pages URL).  
2. Enable **operator mode** (PIN) to score and manage.  
3. Add players → **Create tournament** → draw / play → playoffs.  
4. Open **TV board** on a second tab or display; use **Bar mode** for wall TVs.  
5. **Export** a backup after the night.  

---

## Feature map (summary)

```
Events: Singles · Doubles · DYP · Monster DYP · Sandbox
Play:   Ranking rounds · Fair sits · Partner rotation · Tables · Timers
Bracket: Double-elim · Seeds · Tiered Monster pairs · Conflict lock
Score:  Quick chips · OT win-by-2 · Series Bo3/Bo5 · Coin / serve
TV:     Multi-event · Color bands · Bar mode · Next-up ticker · Announce
Rank:   2000 start · Locked bonus pool · Seed ±8 tiers · Equal partner Δ
Stats:  Career · Event · DNA · Awards · Profiles · Rival below
Ops:    PIN · Import/export · Control center · Recalculate ranking
```

---

## Club

**Lake Champlain Foosball Club (LCFC)**  
Built for weekly in-person foosball — not a generic SaaS bracket tool.

---

*README aligned with LCFC Manager v7.32. Operator PIN intentionally omitted.*
