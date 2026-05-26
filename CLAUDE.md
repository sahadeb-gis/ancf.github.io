# CLAUDE.md

Project-specific guidance for Claude Code working in this repository.

## What this repo is

The website source for **Avayaranya Nature Conservation Foundation (ANCF)** — a
Bangladesh-based nonprofit working on community plantation, biodiversity
conservation, tree tagging, mapping, and climate action since 2013.

It is a **Material for MkDocs** static site that builds to GitHub Pages.
The scaffold was forked from the Spatial Thoughts geospatial-portfolio
workshop and reworked for an organisation site — coding conventions still
follow that template. Live site (post-migration): <https://avayaranya.org/>.

## Stack

- **Material for MkDocs** (`mkdocs-material>=9.5`) — theme, nav, palette, icons.
- **mkdocs-jupyter** — renders any `.ipynb` dropped into `docs/projects/`.
- **GitHub Actions** (`.github/workflows/deploy.yml`) — on every push to `main`
  runs `mkdocs gh-deploy --force`, publishing to the `gh-pages` branch.
- **GitHub Pages** serves `gh-pages`.

Python deps are pinned in `requirements.txt`; a conda env spec is in
`environment.yml`.

## Local preview

```powershell
mkdocs serve
```

Then open <http://127.0.0.1:8000/>. Edits to `docs/` or `mkdocs.yml` trigger a
live rebuild. For a strict CI-style check before pushing:

```powershell
mkdocs build --strict --site-dir _smoketest_site
```

`--strict` turns broken-link and missing-asset warnings into errors. Delete
`_smoketest_site` after — it is gitignored if you keep it under that name.

## Directory layout

```
docs/
├── index.md                 # Home — hero, mission, programmes, stats, story cards
├── about.md                 # About ANCF + mission/vision + history timeline
├── what-we-do.md            # Nine programme domains
├── team.md                  # Executive committee (grid cards) + coordinators
├── contact.md               # Contact and partnership channels
├── projects/                # One page per programme
│   ├── index.md             # Gallery
│   ├── community-plantation.md
│   ├── tree-tagging.md
│   ├── mapping-endangered-plants.md
│   ├── forest-bathing.md
│   └── science-in-conservation.md
├── stories/                 # Blog-style posts (one file per post)
│   ├── index.md             # Gallery
│   └── *.md
└── assets/
    ├── css/extra.css        # All custom CSS (hero, about, cards, footer, etc.)
    └── images/
        ├── ancf_logo.png    # Site logo + favicon
        ├── ancf_banner.png  # Home-page hero banner (2400×600, 4:1)
        ├── About ANCF.png   # Home-page About illustration
        ├── team/            # Team portraits
        ├── ancf_ one pager.png        # Source reference (programmes + stats)
        └── ancf_ project history.pdf  # Source reference (50+ projects 2013–)
```

## Conventions (do not violate)

### Filenames
- **Lowercase, hyphen-separated** (`tree-tagging.md`, not `TreeTagging.md`
  or `tree_tagging.md`).
- For new images, prefer lowercase-hyphen (`about-ancf.png`). The repo
  contains a few legacy spaces/capitals (`About ANCF.png`, `ancf_ one pager.png`)
  — when referencing them, URL-encode the space as `%20`.

### Page front matter
Top-level pages (Home, About, Team, Contact, Stories index, Projects index)
hide the right-hand TOC and left nav for a cleaner landing look:

```markdown
---
hide:
  - toc
  - navigation
---
```

Sub-pages (individual projects, individual stories) do **not** hide nav/toc
— readers benefit from seeing them.

### Checklist comments
Every editable page begins with an HTML-comment checklist describing what
to update. Pattern:

```markdown
<!--
CHECKLIST FOR THIS PAGE:
- [ ] Replace [PLACEHOLDER ...] paragraphs
- [ ] Add cover image at docs/assets/images/...
- [ ] ...
-->
```

Preserve this pattern when adding new pages. It is the user's primary cue
for what still needs editing.

### Placeholders
Unfilled content is marked `[PLACEHOLDER — short description]` (square
brackets, uppercase word `PLACEHOLDER`). Do not invent content to fill
these — leave them or ask the user.

### Component classes (defined in `docs/assets/css/extra.css`)
- `.hero` + `.hero-banner` — Home-page hero (banner image in a green-bordered card).
- `.about-section` / `.about-text` / `.about-image` — text + illustration row on Home.
- `.stats` / `.stat` / `.stat-number` / `.stat-label` — big-number stat strip.
- `.timeline` / `.timeline-entry` — vertical timeline (About page history).
- `.grid cards` (Material built-in) — programme/domain cards.
- `.project-card` — gallery cards on Projects and Stories index pages.
- `.team-card` — round-portrait team grid cards.
- `.md-button` / `.md-button--primary` — Material button styling.

### Material icon shortcodes
Use `:material-XXX:` and `:fontawesome-brands-XXX:` for inline icons; full
catalogue at <https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/>.

### Theme palette
Primary green / accent light-green. Header is solid green; logo sits in a
small white pill so it stays visible. Footer is overridden to match
(`var(--md-primary-fg-color)` + `var(--md-primary-fg-color--dark)`).
Do not change palette without asking — branding decision.

## Adding new content

### A new project
1. Copy `docs/projects/community-plantation.md` → `docs/projects/<slug>.md`.
2. Update title, hero image (under `docs/assets/images/projects/`), and the
   four section bodies (Overview / Methods / Findings / Links).
3. Add a card on `docs/projects/index.md` (copy an existing
   `<div class="project-card">` block).
4. Add a nav entry under `Projects` in `mkdocs.yml`.

### A new story
1. Create `docs/stories/<slug>.md` (lowercase-hyphen).
2. Add a card on `docs/stories/index.md`.
3. Add a nav entry under `Stories` in `mkdocs.yml`.
4. Keep stories in reverse-chronological order on the index.

### A new team member
1. Drop the portrait into `docs/assets/images/team/<first-last>.jpg`.
2. Add a `<div class="team-card">` block on `docs/team.md`.

### A new Jupyter-notebook project
Drop the `.ipynb` directly into `docs/projects/`, add a nav entry in
`mkdocs.yml`, and a card on `docs/projects/index.md`. `mkdocs-jupyter`
renders code, markdown, and outputs automatically.

## Source materials (for content mining)

When asked for specific ANCF content, prefer these over the live WordPress
site (which currently has generic placeholder text):

- `docs/assets/images/ancf_ one pager.png` — programmes, annual stats,
  founding statement, office address, Facebook page.
- `docs/assets/images/ancf_ project history.pdf` — 50+ named plantation
  projects 2013–2019 with dates, locations, seedling counts, coordinators,
  partner organisations.
- `docs/assets/images/plantation infographic.png` — 2013–2018 plantation
  summary stats.

## Deploy

Push to `main` and the GitHub Actions workflow does the rest. Site URL is
configured via `site_url` in `mkdocs.yml` (currently commented out —
uncomment and set when the custom domain or `*.github.io` URL is fixed).

For a custom domain (`avayaranya.org`), add a `CNAME` file at the repo
root containing the domain — the deploy workflow already copies it into
`docs/CNAME` during builds.

## Things to be careful about

- **Never commit the project-history PDF / one-pager PNG out of `docs/assets/`** —
  they are referenced by relative paths from multiple pages.
- **CRLF/LF warnings on `git add`** are expected on Windows; do not "fix"
  them by changing line endings — Git's auto-conversion handles it.
- **Force-push to `main` requires confirmation** — even if asked. The
  deploy workflow rewrites `gh-pages` on every push, so history rewrites
  on `main` are usually safe, but ask first.
- The repo's name is `ancf.github.io` (with the literal `.github.io`
  suffix as part of the name, not as a hostname segment) — this is the
  user's choice; do not rename.
