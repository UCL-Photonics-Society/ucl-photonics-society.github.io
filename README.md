# 💡 UCL Photonics Society — Website

This repository contains the source of the **UCL Photonics Society** website, live at
**<https://ucl-photonics-society.github.io>**.

The website is built with [Quarto](https://quarto.org) and hosted for free on [GitHub Pages](https://pages.github.com).
You **don't need to know how to code** to contribute: pages are written in Markdown, a very simple text format.

> [!TIP]
> New to all of this? Follow the sections **in order**. The setup is only done once (~30 minutes), and after that, updating the website takes a few minutes.

---

## 📁 Repository structure

```text
ucl-photonics-society.github.io/
├── _quarto.yml                  ← website settings: title, navigation bar, footer, theme
├── pyproject.toml / uv.lock     ← Python environment (managed by uv, don't edit by hand)
├── README.md                    ← this guide
├── .github/workflows/
│   └── publish.yml              ← automatic build & deployment (GitHub Actions)
└── website/                     ← ✏️ ALL THE PAGES LIVE HERE
    ├── home.qmd                 ← home page
    ├── projects/
    │   └── placeholder.qmd      ← projects page
    ├── annual_reports/
    │   ├── annual_report_25_26.qmd
    │   └── optica_annual_report_2526.pdf
    └── _assets/                 ← images, logos and the colour theme (theme.scss)
        ├── logos/               ← partner logos
        └── events/              ← event pictures
```

- Every `.qmd` file in `website/` becomes a page of the website (`home.qmd` → `home.html`).
- To add a page to the navigation bar, add it under `navbar:` in `_quarto.yml`.
- Colours and styles (cards, buttons, hero banner…) are defined in `website/_assets/theme.scss`.
- The built website goes to `.quarto_output/` — it is generated automatically, **never edit or commit it**.

---

## 🧑‍💻 Contributor guide

### 1. Setup steps (only once)

#### 1.1 Install the tools

| Tool | What it's for | Where to get it |
|------|---------------|-----------------|
| **Git** | Keeps track of every change to the files | <https://git-scm.com/downloads> — Windows users: this installs **Git Bash**, keep the default options |
| **VS Code** | The text editor you'll write pages in | <https://code.visualstudio.com> |
| **Quarto** | Turns `.qmd` files into web pages | <https://quarto.org/docs/get-started/> |
| **Quarto extension for VS Code** | Syntax highlighting + live preview button | In VS Code: *Extensions* tab (left bar, four squares icon) → search **"Quarto"** → *Install* |

You also need a free **GitHub account** (<https://github.com/signup>). Ask a committee member to add you to the [UCL-Photonics-Society](https://github.com/UCL-Photonics-Society) organisation.

#### 1.2 Open a terminal in VS Code

In VS Code, open the menu **Terminal → New Terminal**. A panel opens at the bottom: this is where you type the commands below (copy-paste them, then press <kbd>Enter</kbd>).

> [!NOTE]
> **Windows users:** in the terminal panel, click the small **˅** arrow next to the **+** and choose **Git Bash**, so that the commands below work as written.

#### 1.3 Tell Git who you are

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@ucl.ac.uk"
```

Use the same email as your GitHub account.

#### 1.4 Install uv (Python environment manager)

[uv](https://docs.astral.sh/uv/) installs the Python packages the website needs, in an isolated environment.

- **macOS / Linux / Git Bash:**

  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```

- **Windows (PowerShell)**, if the above fails:

  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```

Close and reopen VS Code afterwards, then check it worked with `uv --version`.

#### 1.5 Download (clone) the repository

```bash
cd ~/Documents
git clone https://github.com/UCL-Photonics-Society/ucl-photonics-society.github.io.git
```

Then in VS Code: **File → Open Folder…** and select the `ucl-photonics-society.github.io` folder. Open a new terminal (it now opens inside the project folder).

#### 1.6 Set up the Python environment

```bash
uv sync
```

This creates a `.venv/` folder with everything needed. ✅ You're ready!

#### 1.7 Preview the website on your computer

```bash
uv run quarto preview
```

Your browser opens the website at a local address (e.g. `http://localhost:4321`). Every time you **save** a file, the page refreshes automatically. Press <kbd>Ctrl</kbd>+<kbd>C</kbd> in the terminal to stop.

---

### 2. Quarto 101

[Quarto](https://quarto.org) is an open-source publishing system: you write **Markdown** files (`.qmd`), and Quarto converts them to a styled website.

Each `.qmd` file has two parts:

```markdown
---
title: "My page title"          ← the header ("front matter"): page settings
---

## A section title               ← the content, in Markdown

Some **bold** text, some *italic* text and a [link](https://www.optica.org).

- a bullet point
- another one

![An image](../_assets/events/thorlabs-bike.jpg)

::: {.callout-tip}
A coloured information box!
:::
```

Handy resources:

- 📘 [Markdown basics](https://quarto.org/docs/authoring/markdown-basics.html) — everything about formatting text
- 🧱 [Callouts](https://quarto.org/docs/authoring/callouts.html), [figures](https://quarto.org/docs/authoring/figures.html), [tables](https://quarto.org/docs/authoring/tables.html)
- 🌐 [Quarto websites](https://quarto.org/docs/websites/) — navigation, footer, site settings
- 🎨 [HTML themes](https://quarto.org/docs/output-formats/html-themes.html) — how `theme.scss` works
- 🔣 [Bootstrap icons](https://icons.getbootstrap.com) — icons used on the site, e.g. `<i class="bi bi-lightbulb"></i>`

> [!TIP]
> The home page uses a few custom blocks you can copy-paste: `::: {.card-grid}` with `::: {.photon-card}` inside (activity / event cards), `::: {.stats}` (big numbers), `::: {.logo-wall}` (partner logos) and `::: {.social-row}` (buttons). Look at `website/home.qmd` for examples.

---

### 3. GitHub Pages 101

[GitHub Pages](https://docs.github.com/en/pages) is a free service from GitHub that hosts static websites straight from a repository.

How our website gets online:

```text
 you edit a .qmd file  ──►  Pull Request to main  ──►  automatic build check ✅
                                                           │
                                     merge into main  ◄────┘
                                           │
                                           ▼
                       GitHub Actions renders the site with Quarto
                                           │
                                           ▼
                  🌐 published at https://ucl-photonics-society.github.io
```

- The automation lives in `.github/workflows/publish.yml` and runs on GitHub's servers — nothing to do on your side.
- You can follow it in the **Actions** tab of the repository. A green ✅ means the website was built (and, on `main`, published) successfully; a red ❌ means something is broken — click on it to read the error.
- Changes usually appear online **1–2 minutes** after merging.

> [!IMPORTANT]
> One-time admin setting: in the repository **Settings → Pages → Build and deployment → Source**, select **GitHub Actions**.

---

### 4. Contribution workflow

> [!WARNING]
> **Never work directly on `main`.** `main` is the live website. Always make your changes on a separate *branch*, then ask for them to be merged through a *Pull Request* (PR).

**① Create a branch on GitHub**
On the [repository page](https://github.com/UCL-Photonics-Society/ucl-photonics-society.github.io), click the branch dropdown (top-left, shows `main`), type a short name such as `update-committee-2026`, and click **Create branch: update-committee-2026 from main**.

**② Switch to your branch in VS Code** (terminal):

```bash
git fetch
git switch update-committee-2026
uv sync
```

**③ Make your changes**
Edit the `.qmd` files and check the result live with `uv run quarto preview`.

**④ Save your changes with Git**

```bash
git status                                   # see which files changed
git add website/home.qmd                     # pick the files to save (or "git add ." for all)
git commit -m "Add 2026-2027 committee"      # short message describing the change
git push                                     # send them to GitHub
```

> [!TIP]
> Prefer clicking to typing? VS Code's **Source Control** tab (left bar, branch icon) does the same: stage with **+**, write a message, click **Commit**, then **Sync Changes**.

**⑤ Open a Pull Request**
Back on GitHub, a yellow banner shows *"update-committee-2026 had recent pushes"* → click **Compare & pull request**. Make sure it goes **into `main`**, describe your changes, and click **Create pull request**.

**⑥ Check that the tests pass**
At the bottom of the PR, wait for the **Build & deploy website** check to turn green ✅. If it's red ❌, click **Details** to see the error, fix it on your branch, and push again (steps ③–④) — the PR updates automatically.

**⑦ Merge 🎉**
Once a committee member has reviewed it, click **Merge pull request**. The website is rebuilt and published automatically within a couple of minutes.

---

## 🆘 Need help?

Contact the committee at [photonics.society@ucl.ac.uk](mailto:photonics.society@ucl.ac.uk) or on [LinkedIn](https://www.linkedin.com/company/ucl-photonics-society/).
