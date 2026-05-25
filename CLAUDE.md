# CLAUDE.md — leafnotes generator

This repo is a collection of garden plant catalogs. Each catalog lives in its own subfolder and is published as a static page via GitHub Pages.

## Your job when asked to "generate a catalog for `<name>`"

1. **Read `<name>/plants.md`** — the input. Format is loose markdown; see `brandon/plants.md` for the canonical example. Expect:
   - Garden name (h1).
   - `Zone: NNn` (e.g., `Zone: 6a`) — optional but recommended.
   - `Planted: YYYY` (or `YYYY-MM`) — the year the garden went in. Used to compute year-1 vs. established care (see step 4 below).
   - A list of plants with botanical names and quantities. Inline `(new)`, `(established)`, or `(established YYYY)` overrides per plant for mixed gardens.

2. **For each plant, gather:**
   - Common name + botanical (Latin) name.
   - Quick stats: sun (full/part/shade), water (low/avg/high), mature size, bloom time, **origin**, **maintenance level**, and quantity.
     - **Origin** examples: `🌎 NE Native`, `🌎 NA Native`, `🌎 Asia`, `🌎 Europe`, `🌎 Hybrid`, `🌎 Mixed origin`. Be honest — "Hybrid" or "Mixed origin" is fine when a plant doesn't trace cleanly to one place.
     - **Maintenance**: `🛠️ Easy` (set-and-forget), `🛠️ Moderate` (some seasonal attention), `🛠️ Demanding` (regular work — pruning, staking, pest control, winter protection).
   - 1–2 sentence "at a glance" description with personality.
   - **Check-in signs** — 3–5 diagnostic items in `symptom → likely cause` form. This is the signature feature. Examples: "drooping leaves → thirsty," "yellow leaves → check drainage or iron," "no growth by mid-May → late emerger, normal."
   - **Watch out for** — 1–3 pests, diseases, or hazards specific to this plant (e.g., "Japanese beetles," "powdery mildew if airflow is poor," "deer browse in winter").
   - **Care notes** — short paragraph: when to prune, fertilize, divide, mulch. Practical, not academic.

3. **Find images** — 1–3 representative photos per plant, following this slot pattern:
   - `plant_name.jpg` — **full plant / habit shot** (the whole shrub or clump, showing form and size).
   - `plant_name_2.jpg` — **closeup of distinguishing feature** (flower if showy; foliage texture/color otherwise).
   - `plant_name_3.jpg` — *optional* second feature (fall color, seed heads, in-garden context, alternate angle).

   Save to `<name>/images/` using snake_case filenames matched to the plant's common name. Sources: Wikimedia Commons, university extension pages (Missouri Botanical Garden, Cornell, NCSU, UMass Extension), or reputable garden center sites. Keep file sizes reasonable (under ~300KB each).

4. **Build the maintenance timeline** — 12 month-by-month task lists, customized to the actual plants in this garden. Don't just copy Brandon's timeline; tailor it. If a garden has no roses, drop the rose-specific tasks. If a garden has hibiscus, include the "patience, it emerges late" reminder in May.

5. **Build the "This Month" panel** — 5–8 of the most pressing tasks for the current calendar month, pulled from the timeline plus any seasonal urgency. Today's date is in the system prompt — use it.

   **Year-1 vs. established (important).** Compute the "growing season" for each plant: `current_year - planted_year + 1`. Plants in season 1 (i.e. just planted this year) need different care than established plants:
   - Water more frequently and deeply (regardless of mature water needs).
   - Do NOT fertilize the first year — let roots establish.
   - Mulch heavier (3–4").
   - Skip division/transplanting.
   - Extra winter protection for borderline-hardy plants.

   If **any** plant is year-1, add a `<section class="panel year-one">` callout above the plant cards titled **"First-year basics"** with the universal year-1 advice. Mark each year-1 plant card with a `🌱 Year 1` badge and add a brief "Year 1 watch" line to its care notes.

   If **all** plants are year-1 (typical for a brand-new garden), make the first-year callout prominent — it's the most important panel on the page that season.

6. **Generate `<name>/index.html`** — model the structure on `brandon/index.html` (the canonical fully-realized example). Use `_template/template.html` as a structural reference if helpful. Keep the styling/CSS identical across catalogs for consistency.

7. **Update the root `index.html`** to add a card linking to the new garden. Match the existing `.garden-card` pattern.

## Accuracy & honesty

Care info varies a lot by species and cultivar, so don't bluff.

- **Don't invent cultivars.** If `plants.md` says "Hydrangea (variety unknown)," write "variety unknown" in the catalog — don't promote it to "Bobo Hydrangea" based on a guess.
- **Cross-reference at least 2 sources** before writing care notes for an unfamiliar plant. University extension sites (Missouri Botanical Garden, Cornell, NCSU, UMass Extension) are the gold standard. Garden center marketing copy is the weakest source.
- **Never fabricate diagnostic signs.** For "check-in signs," only include symptom → cause pairs that are well-documented for the species. When in doubt, leave it out.
- **Mark uncertainty.** When a plant ID is ambiguous (e.g., "white flowering shrub"), add a `⚠️ Needs verification` badge to the card and write care notes for the most likely genus only — not a specific species.
- **Note when care depends on species.** Some genera (Hydrangea, Spirea, Clematis) vary dramatically in pruning needs across species. If care depends on which species, say so in the care notes rather than picking one and committing to it.

## Conventions

- **Folder names** — lowercase, URL-friendly (`martha`, not `Martha's Garden`).
- **Plant card IDs** — kebab-case anchors based on common name (e.g., `id="bobo-hydrangea"`).
- **Image filenames** — snake_case, matching the plant. Main: `plant_name.jpg`. Extras: `plant_name_2.jpg`, `plant_name_3.jpg`.
- **Tone** — friendly and practical, not academic. Write for someone who didn't plant the garden and may not know botanical Latin.
- **Mobile-first** — the catalogs are mostly read on phones. Test that cards stack cleanly.
- **Zone tag** — always include in the header if known. Zone affects which timeline advice is relevant.

## What NOT to include

- Invoice numbers, addresses, or other personal info beyond the optional zone.
- Long academic descriptions. The card is a quick reference, not a botany text.
- Hardcoded "Spring 2026 checklist" style sections — those are replaced by the dynamic "This Month" + 12-month timeline.

## Verifying

After generating, sanity-check:
- All images load (no broken `<img>` tags).
- All anchor links in the plant index resolve to a card with the matching `id`.
- The "This Month" tab is auto-selected (the JS does this — verify the month number is correct).
- The card grid looks good at narrow widths (one column on mobile).

## Adding a plant to an existing garden

Same flow, smaller scope. Read the existing `plants.md`, add the new plant, then regenerate `index.html` (or surgically insert a new card). Drop new images into the existing `images/` folder.
