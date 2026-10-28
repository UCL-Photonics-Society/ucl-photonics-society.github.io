# 📂 `website/projects/`

This folder holds the **Projects & Events** page and one folder per event.

```text
projects/
├── overview.qmd                         ← the "Projects & Events" page
├── _metadata.yml                        ← settings shared by every page in this folder
├── README.md                            ← this file (not part of the website)
└── 2025-12-02-moku-delta-showcase/      ← one folder per event
    ├── index.qmd                        ← the event's page
    └── banner.jpg                       ← optional event picture
```

## How it fits together

```text
 2025-12-02-moku-delta-showcase/index.qmd
   header: title, date, description, venue, academic-year, image
          │
          ├──► overview.qmd   all events, one section per academic-year, newest first
          │
          └──► ../home.qmd    the 3 most recent events ("Recent Highlights")
```

Both pages use Quarto [listings](https://quarto.org/docs/websites/website-listings.html): they look for every
`*/index.qmd` in this folder and build a card from each page's header, using the card template
`../_assets/event-card.ejs.md`. **Adding a folder is enough.** Nothing else needs editing
(except for the first event of a new academic year, see below).

Clicking a card opens the event page itself (the body of `index.qmd`).

## Rules

| What | Rule | Why |
|------|------|-----|
| Folder name | `YYYY-MM-DD-short-name` (date of the event) | Folders sort in date order |
| Event page | Always named `index.qmd` | Listings look for `*/index.qmd` |
| `date` | `YYYY-MM-DD`, the (first) day of the event | Sorts events and picks the 3 latest for the home page |
| `date-display` | Optional, e.g. `"13 – 16 October 2026"` | Replaces `date` on cards for multi-day events |
| `academic-year` | e.g. `"2025-2026"` | Chooses the section on the overview page |
| Picture | `banner.jpg` in the event folder, ideally 2:1 | Cards show it in a 2:1 frame |

## New academic year

Each academic year is one listing in the header of `overview.qmd`. For the first event of a new year,
copy a block under `listing:`, change `id` and `academic-year`, and add the matching heading and
`::: {#events-YYYY-YYYY}` placeholder in the page.

## Adding an event

See **"5. Adding an event"** in the [main README](../../README.md) for the step-by-step guide and a template.
