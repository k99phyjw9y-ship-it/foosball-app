# LCFC Manager v7.49

Lake Champlain Foosball Club manager and TV-board app.

## What's new in v7.49

### Awards podium resolution fix
- Awards podium aggregation now resolves historical team placements through the tournament's saved team roster by team ID.
- This handles placement records containing only `{id, name}` and avoids losing team members when historical names have spelling variations.
- The fix is limited to Club Stats podium/playoff appearance aggregation and does not alter ranking points, bonus points, seeding, match results, or playoff calculations.

## What's new in v7.45

### Teams statistics
- Added a **Teams** section beside Club DNA and Awards in Club Stats.
- Tracks all-time partnerships where the same two roster players appear together on one side of a completed match.
- Partnership identity uses the two player IDs in sorted order, so reversing the team-side order does not create a second partnership.
- Shows total appearances, ranking-match appearances, playoff appearances, wins, losses, win percentage, first played, and last played.
- Includes a player filter and a match-history view for each partnership.
- Best-of series count once as one partnership appearance, not once per game.

### Separation and counting rules
- Ranking / Swiss-round matches and bracket / playoff matches are counted and displayed separately.
- Only completed, non-void matches with a valid result are included. Byes, unfinished matches, sandbox events, singles sides, and sides that do not resolve to exactly two roster players are excluded.
- Team statistics are read-only and derived from existing tournament records. They do **not** change ranking points, bonus points, seeding, standings, or playoff calculations.
- The Teams page summary counts partnership appearances across all qualifying sides. A completed doubles match can therefore add one appearance to each of its two partnerships.

## Run the app

1. Download `index.html`.
2. Open it in a modern browser, or replace the existing app's `index.html` with this file where the app is hosted.
3. Use the app's existing backup/export workflow before replacing a live copy.

The app is a single-page HTML application. No separate build step is required.

## Version

- App version: **7.49**
- Build date: **November 25, 2026**
- Main file: `index.html`
