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

## Tips for entering plant lists

When putting together a `plants.md` for a new garden:

- Use **cultivar names** when known (e.g., "Bobo Hydrangea" vs. just "Hydrangea") — care varies a lot between varieties of the same genus.
- If the planter has **receipts or plant tags**, those are the most reliable source of exact cultivars.
- For uncertain plants, describe **what you can see**: "small shrub, purple foliage, dome-shaped." Vague is fine — much better than guessing the wrong species.
- Mark uncertain ones with `(variety unknown)` or `?` so the catalog flags them rather than inventing details.
- Add quantities when known (`× 3`), container sizes if relevant (`3-gal pots`), and the year planted at the top of the file.

Example for a partly-known garden:

```markdown
# Martha's Garden

Zone: 6a
Planted: 2026 (new)

## Plants
- Bobo Hydrangea × 3 — small starts
- Hydrangea (variety unknown) × 1 — bigleaf, blue flowers
- "purple-leaf shrub, dome-shaped" × 1 — ? maybe ninebark or smokebush
```

## Viewing

Anyone with the URL can view a catalog — no GitHub account needed. Designed to be mobile-friendly.
