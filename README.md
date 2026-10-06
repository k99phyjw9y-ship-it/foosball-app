# Club snapshot for GitHub Pages

## Where to put the file

Upload your **full backup** JSON as:

```
data/latest.json
```

Same level as this README. In the repo that hosts Pages:

```
your-repo/
  index.html          ← LCFC Manager
  data/
    latest.json       ← full backup from Export all
    README.md
```

If Pages is served from `/docs`, use:

```
docs/index.html
docs/data/latest.json
```

## How to create latest.json

1. In LCFC Manager, tap **Export all**
2. Rename the downloaded file to `latest.json` (or keep the name and rename on upload)
3. Upload into the `data/` folder on GitHub
4. Wait for Pages deploy, then hard-refresh the site

Members opening the site will auto-load this file (unless **Operator mode** is on).

## Format

Must be a full backup:

```json
{
  "app": "LCFC Manager",
  "type": "full",
  "exportedAt": "2026-10-06T...",
  "players": [ ... ],
  "tournaments": [ ... ]
}
```
