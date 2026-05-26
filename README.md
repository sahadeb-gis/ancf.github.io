# Avayaranya Nature Conservation Foundation (ANCF)

Source for the ANCF website at [https://avayaranya.org/](https://avayaranya.org/).

Built with:

- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [mkdocs-jupyter](https://github.com/danielfrg/mkdocs-jupyter)
- GitHub Pages, deployed via GitHub Actions (`.github/workflows/deploy.yml`)

## Local preview

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open <http://127.0.0.1:8000>.

## Structure

```
docs/
├── index.md                 # Home
├── about.md                 # About ANCF
├── what-we-do.md            # Nine programme domains
├── team.md                  # Executive committee + coordinators
├── contact.md               # Contact and partnership channels
├── projects/                # One page per programme
│   ├── index.md
│   ├── community-plantation.md
│   ├── tree-tagging.md
│   ├── mapping-endangered-plants.md
│   ├── forest-bathing.md
│   └── science-in-conservation.md
├── stories/                 # Blog-style posts
│   ├── index.md
│   └── *.md
└── assets/
    ├── css/extra.css
    └── images/
```

Each Markdown page begins with a short HTML-comment checklist describing
what to update. Filenames use lowercase-and-hyphens (`tree-tagging.md`,
not `TreeTagging.md`).

## License

[MIT License](LICENSE)
