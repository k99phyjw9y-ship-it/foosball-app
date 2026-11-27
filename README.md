# LCFC Manager v7.51

## Category Rankings (Option A)

Adds separate lifetime category leaderboards while retaining the existing Overall LCFC ranking:

- **Singles:** includes ranking-point deltas from Singles events only.
- **Doubles:** includes ranking-point deltas from Doubles, DYP, Monster DYP, and recognized Monster DYP naming variants.
- Existing event-awarded ranking deltas are reused (Option A); category-specific points are not independently recalculated.
- Category standings exclude imported-copy and sandbox tournaments and only credit deltas for player IDs present in the current player list.
- Playoff/bracket results are represented through the event's stored ranking deltas, inheriting the originating event's format.
- Doubles-team credit follows the IDs present in that event's ranking-delta records.

## Interface

The Ranking area includes a Category Rankings section with Singles and Doubles views. Category totals are accumulated and sorted descending, with player-name sorting used to break ties.

## Compatibility and cautions

- The Overall club ranking and its recalculation workflow remain the existing system.
- Category rankings are based on recorded `rankingDeltas`; they do not independently rebuild event scoring.
- Back up the current manager data before deploying or testing this version.

## Version

LCFC Manager v7.51. Build stamp in the HTML: `LCFC_MANAGER_BUILD v7.51`.
