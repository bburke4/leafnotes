# 🌿 leafnotes

Plant catalogs with care info, diagnostic check-ins, and a year-round maintenance timeline. One catalog per garden, hosted on GitHub Pages.

## What's here

```
leafnotes/
├── index.html         landing page listing all gardens
├── _template/         reference template for new catalogs
├── brandon/             ← one garden, one folder
│   ├── plants.md      the input — your plant list
│   ├── index.html     the generated catalog
│   └── images/        plant photos
└── CLAUDE.md          instructions for Claude (the generator)
```

## Add a new garden

1. **Create a folder** with a short, URL-friendly name (e.g., `martha/`).
2. **Drop a `plants.md`** inside it. Keep it simple — list the plants, one per line, with botanical name and quantity if known. Include a `Planted: YYYY` line at the top — if it's the current year, the catalog adds a "First-year basics" callout and marks plants with a 🌱 badge. See `brandon/plants.md` for the format.
3. **Open Claude Code in this repo** and ask:
   > Generate the catalog for `martha`.
4. Claude reads `plants.md`, fetches care info, downloads images, and writes `martha/index.html` plus an `images/` folder.
5. Add a link to the new garden in the root `index.html`.
6. Commit and push — GitHub Pages updates automatically.

## What's in each catalog

- **This Month** — what to do right now, driven by the current date.
- **Plant index** — scannable list with jump links.
- **Year timeline** — 12-month maintenance tabs.
- **Plant cards** — one per plant:
  - 1–3 photos with a swipeable carousel.
  - Quick stats: sun, water, size, bloom time, quantity.
  - At-a-glance description.
  - **Check-in signs** — diagnostic: symptom → likely cause.
  - **Watch out for** — pests and diseases specific to that plant.
  - **Care notes** — when to prune, fertilize, divide.

## Viewing

Anyone with the URL can view a catalog — no GitHub account needed. Designed to be mobile-friendly.
