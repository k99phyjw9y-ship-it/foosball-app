# LCFC Manager v7.51

Lake Champlain Foosball Club manager and TV-board app.

## What's new in v7.51

### Separate Singles and Doubles ranking points
- Each player now has independent **Singles** and **Doubles** ranking points (both start at 2,000).
- **Combined** ranking = Singles + Doubles (shown on player list, profile, and the Combined ranking tab).
- Event mapping:
  - **Singles** events → Singles points only
  - **Doubles / DYP / Monster** events → Doubles points only
- Club Ranking tab has Combined / Singles / Doubles toggles.
- Seed order and bonus pool for an event use that event's discipline ranking list.
- Player add/edit modal has separate Singles and Doubles point fields.
- Recalculate from events resets both disciplines to 2,000 and replays history with the split rules.
- Existing single-pool totals are migrated into both disciplines on first load; run **Recalculate from events** (operator mode) to re-attribute historical results correctly by event type.
- No changes to match outcomes, standings, seeding rules inside an event, or playoff bracket structure.

## What's new in v7.50

### Unified tournament-aware player attribution
- Added a shared `resolveMatchPlayerIds(tournament, entity)` resolver for player-stat calculations.
- Resolution prefers valid explicit player IDs, then roster IDs resolved from the tournament's saved teams / playoff teams by team ID, and finally the existing entity/name resolution fallback.
- This fixes historical team-name spelling drift where a team ID was valid but one partner's name failed to match the current roster.
- Applied to player career, weekly, and event-type match stats; designated forward/goalie stats; best-single-night totals; close-win/loss and streak stats; and playoff win counts.
- Player attribution uses existing saved rosters and IDs. It does not change match outcomes or scores.

### Scope and safeguards
- No changes to ranking points, bonus points, standings, seeding, scoring, or playoff rules.
- Existing tournament data is not rewritten; stats are resolved when displayed/calculated.
- The earlier v7.49 Awards podium fix remains in place.

## What's new in v7.49

### Awards podium resolution fix
- Awards podium aggregation resolves historical team placements through saved tournament team rosters by team ID.
- Handles placement records containing only `{id, name}` and spelling variations in historical team names.

## What's new in v7.45

### Teams statistics
- Added a **Teams** section beside Club DNA and Awards in Club Stats.
- Tracks all-time partnerships using roster player IDs, independent of the order players appear on a team.
- Shows appearances, ranking-match and playoff appearances, wins, losses, win percentage, first played, and last played.
- Includes a player filter and match-history view.
- Best-of series count as one partnership appearance.

### Separation and counting rules
- Ranking / Swiss-round matches and bracket / playoff matches are counted separately.
- Only completed, non-void matches with valid results are included. Byes, unfinished matches, sandbox events, singles sides, and sides that do not resolve to exactly two roster players are excluded.
- Team stats are read-only and derived from existing tournament records. They do not change ranking points, bonus points, seeding, standings, or playoff calculations.

## Run the app

1. Download `index.html`.
2. Open it in a modern browser, or replace the existing app's `index.html` with this file where the app is hosted.
3. Use the app's existing backup/export workflow before replacing a live copy.
4. After upgrading to v7.51, open **Stats → Ranking** in operator mode and run **Recalculate from events** so historical Singles vs Doubles results are split correctly.

The app is a single-page HTML application. No separate build step is required.

## Version

- App version: **7.51**
- Build date: **November 27, 2026**
- Main file: `index.html`
