# LCFC Manager v7.54

## Fixes
- Corrected static browser-title and visible watermark fallback values that still displayed v7.51 on initial refresh. Dynamic metadata and `APP_VERSION` stamps are v7.54.
- Added lifetime Singles and Doubles category ranking-point cards to each player's Career profile tab, reusing recorded event ranking deltas (Option A). Singles events count toward Singles; Doubles, DYP, and Monster DYP variants count toward Doubles. Imported-copy and sandbox tournaments are excluded.
- Changed Club DNA, Teams, and Awards tab render scheduling to a short delayed callback to allow published/read-only layout and state transitions to settle.

## Validation
- Static build-stamp references updated and inspected.
- Permanent snapshot `index_v7.54.html` copied from `index.html`.
- JavaScript syntax/runtime and live GitHub Pages behavior are not independently browser-tested in this release.
