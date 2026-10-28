# 📂 `website/projects/`

This folder holds the **Projects & Events** page and one folder per event.

```text
projects/
├── overview.qmd                         ← the "Projects & Events" page
├── README.md                            ← this file (not part of the website)
└── 2025-12-02-moku-delta-showcase/      ← one folder per event
    ├── _card.qmd                        ← the event's card
    └── banner.jpg                       ← optional event picture
```

## How it fits together

```text
 2025-12-02-moku-delta-showcase/_card.qmd
          │
          ├──► overview.qmd   {{< include 2025-12-02-moku-delta-showcase/_card.qmd >}}
          │
          └──► ../home.qmd    {{< include projects/2025-12-02-moku-delta-showcase/_card.qmd >}}
                              (only the 3 most recent events, under "Recent Highlights")
```

Each card is written **once** and inserted wherever it's needed with Quarto's
[`include`](https://quarto.org/docs/authoring/includes.html) shortcode.
Edit the `_card.qmd` file and every page showing it updates.

## Rules

| What | Rule | Why |
|------|------|-----|
| Folder name | `YYYY-MM-DD-short-name` (date of the event) | Folders sort in date order |
| Card file | Always named `_card.qmd` | The `_` stops Quarto from building it as a page on its own |
| Picture | Named `banner.jpg`, in the event folder | Keeps everything about an event in one place |
| Image path | Start at the repository root: `/website/projects/<folder>/banner.jpg` | The card works from any page that includes it |
| Order in `overview.qmd` | Under the right academic year, newest first | |

## Adding an event

See **"5. Adding an event"** in the [main README](../../README.md) for the step-by-step guide and a card template.
