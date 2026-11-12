# LCFC Manager

**Lake Champlain Foosball Club** — single-file web app for running club nights, ranking rounds, playoffs, TV spectator boards, and career stats.

| | |
|--|--|
| **Version** | **7.42** |
| **Stack** | Single `index.html` (HTML / CSS / vanilla JS), Tailwind CDN, Chart.js |
| **Storage** | Browser `localStorage` (operator); optional published `data/latest.json` for members |
| **Lines (approx.)** | ~16,214 |

---

## Quick start

1. Open `index.html` in a modern browser (Chrome recommended for TV board + speech).
2. Or host via **GitHub Pages** (static site) — same origin can load `data/latest.json`.
3. **Operator mode** (PIN-protected) unlocks scoring, import/export, player edits, and ranking controls.
4. Members can view published club data in read-only mode when a club snapshot is loaded.

> Operator PIN is configured in the app; it is **not** documented in this README.

---

## Event types

| Type | Description |
|------|-------------|
| **Singles** | 1v1 bracket / playoff |
| **Doubles** | Fixed partnerships |
| **DYP** | Draw Your Partner |
| **Monster DYP** | Ranking rounds (swiss-style rotation) → tiered double-elim playoff |

Optional **Sandbox** flag: full play + TV board with sandbox marking; **excluded** from club ranking, career aggregates, and official awards.

---

## Core features

### Tournament operations
- Create / rename events, edit event date, set race-to (default **5**), best-of (1 / 3 / 5)
- Configurable **table count** (default **3**)
- Player roster add / multi-select quick-add; mark **absent** (preserves history)
- Ranking-round draws, sit-outs, table assignment, on-deck queue
- Double-elimination playoffs with tree view, seeds, byes for awkward field sizes (e.g. 6 / 10 / 14)
- Match timers (start after draw delay; on-deck waits for free table)
- Automatic coin toss on draw; serve side on match cards + TV
- Series scoring (best of 3 / 5) with per-game entry and OT (win by 2); quick-score chips **0–8** in OT
- Conflict lock across parallel events
- Export / import tournaments and full club backup JSON

### Fair ranking draws (Monster / DYP)
- Partner rotation prefers **new partners** until each active player has partnered with everyone else
- **Exact perfect matching** for small fields (≤ 10 active); heuristic search otherwise
- Sit-outs: minimum sits first, avoid back-to-back when possible, protect late joiners
- Sit count history kept when the field changes (add / absent)
- Debug blob on last draw: `tournament._lastPairingDebug` (rematches, pairs, sit counts)

### Club ranking points
- Applied from **bracket / playoff results only** (not ranking-round match wins)
- Start rating **2000**; seed-tier swing **±8** per tier band; podium **bonus pool**
- Bonus pool = **1%** of playoff field's combined club RP at **playoff create** (locked snapshot)
- Split modes: **50/30/20** or **60/30/10** (operator toggle)
- Partners on the same place receive the **same** seed + bonus delta
- Expected places frozen at playoff create (`expectedPlaceLocked`) so rebuilds don't drift
- Rebuild from stored event deltas after delete / merge / recalculate
- Sandbox events never apply ranking

### Stats & Club DNA
- Career and per-event leaderboards (points, GD, wins, etc.)
- Podium tracking (1st / 2nd / 3rd), awards (including Hare / Tortoise match timers)
- Best / worst partners, most improved, side-by-side compare
- Player profiles: rank, form (last 10), state/geography, shareable summary
- **Club DNA**: totals, titles vs unique champions, avg match length, goals/night, shutouts, geography

### TV / Spectator board
- Open from home (**all active events**) or from inside an event
- Live + on-deck cards, event **color bands**, seeds on playoffs, Live pill
- Optional **bar mode** + next-up ticker; table timers; sit-out / room panel (single-event)
- Announcer (Arena style + chime packs); sound toggle; manual mic on cards
- Theme-aware; auto-refresh (~5s) with multi-tab `localStorage` sync

### UI / UX
- Themes: Pitch, Lake, Tornado, Fog, Sunset, Grape, Night, Midnight, Arena (+ auto)
- Fonts: Inter (default), DM Sans, Plus Jakarta, IBM Plex
- Collapsible **finished** event cards on home (name, type, podium; expand for recap)
- Operator-only import/export and ranking tools when PIN mode is on
- Read-only banner when viewing published club data

---

## Multi-event & tables

- Parallel singles / DYP / Monster supported
- **Conflict lock** (optional): players in a live match are held in other events until that match finishes
- Global table occupancy when multiple events share tables; fair promote across events
- Ranking-round and playoff table assignment coordinated with free tables

---

## Data model (high level)

```text
state
├── players[]          id, name, skill band, rankingPoints, rankingDelta, homeState, …
└── tournaments[]
    ├── meta           name, type, date, tables, raceTo, bestOf, sandbox, status
    ├── playerIds / absentIds / sitOutQueue
    ├── rounds[]       ranking matches, sitOutIds, teams
    ├── playoffs       double-elim tree, placements, bonusPoolLocked, expectedPlaceLocked
    └── ranking*       rankingApplied, rankingDeltas, rankingDeltaDetail, …
```

Backups: full JSON export (`app`, `version`, `exportedAt`, `players`, `tournaments`).

---

## Hosting

| Option | Notes |
|--------|--------|
| **Local file** | Open `index.html` on the operator laptop |
| **GitHub Pages** | Push `index.html` (+ optional `data/latest.json`) for a public URL |
| **Club snapshot** | Publish `data/latest.json`; app can fetch on boot for members (read-only) |

No required backend. Optional future: Supabase / Firebase for shared live rooms.

---

## Operator vs member

| Capability | Operator (PIN on) | Member / PIN off |
|------------|-------------------|------------------|
| Score matches | Yes | No |
| Create / edit events | Yes | No |
| Import / export | Yes | Hidden |
| View stats / TV / profiles | Yes | Yes (published data) |
| Ranking recalculate | Yes | No |

---

## Version watermark

Home footer shows:

- App **version** (e.g. v7.42)
- Approximate **lines of code**
- Club file / backup timestamps when a snapshot is loaded

---

## Recent integrity work (v7.42)

- Safer HTML attribute escaping for ids; hardened load/boot path
- Ranking rebuild after **event delete**; no double-count on **import-as-copy**
- Stronger **player merge** reference rewrite + scrub
- **Locked** bonus pool + expected places at playoff create
- Exact partner matching for small Monster fields; pairing debug metadata

---

## Rules references

Club play should follow applicable table soccer rules. Useful external references (not bundled):

- ITSF Rules of Table Soccer (official ITSF publications)
- Local club house rules for Monster rotation and race-to

---

## Development notes

- One file deploy: replace `index.html` and hard-refresh (cache-bust meta is present).
- Keep `APP_VERSION`, `<meta name="lcfc-build">`, title, and `APP_LINES` in sync on each release.
- Prefer small, testable changes to ranking, draws, and bracket propagation.
- Sandbox paths must remain excluded from ranking and official stats aggregations.

---

## License / use

Built for **Lake Champlain Foosball Club** club operations. Adapt for other clubs as needed; no warranty.

---

*LCFC Manager v7.42 — Lake Champlain Foosball Club*
