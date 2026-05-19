# Jiawen Gu — Academic Homepage

Personal academic website built with [MkDocs](https://www.mkdocs.org/) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/). Automatically deployed via GitHub Actions.

**Live Site**: https://gujiawen777.github.io/homepage/

## Structure

```
docs/
├── index.md                 # Home page with profile & research overview
├── cv.md                    # Curriculum vitae
├── publications.md          # Publications list
├── research.md              # Research directions & projects
├── notes/
│   ├── index.md             # Notes overview
│   ├── transfer-learning.md
│   ├── GraphRAG.md
│   └── LightRAG.md
├── images/                  # Profile photo & images
└── stylesheets/             # Custom CSS
```

## Local Development

```bash
# Install dependencies
pip install mkdocs-material

# Start dev server
mkdocs serve -a 127.0.0.1:8080

# Build site
mkdocs build
```

## Deployment

Push to `main` — GitHub Actions builds and deploys to `gh-pages` automatically.

## Tech Stack

- [MkDocs](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- GitHub Pages + Actions
