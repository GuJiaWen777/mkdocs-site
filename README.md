# Jiawen Gu - Academic Homepage

Personal academic website built with [MkDocs](https://www.mkdocs.org/) and [Material theme](https://squidfunk.github.io/mkdocs-material/).

🔗 **Live Site**: https://gujiawen777.github.io/mkdocs-site/

## Structure

```
docs/
├── index.md           # Home page
├── publications.md    # Publications list
├── research.md        # Research interests & projects
├── cv.md              # Curriculum vitae
├── notes/             # Learning notes
│   ├── index.md
│   └── transfer-learning.md
├── images/            # Profile photo & images
└── stylesheets/       # Custom CSS
```

## Commands

```bash
# Install dependencies
pip install mkdocs-material

# Local preview (port 8080 to avoid conflicts)
mkdocs serve -a 127.0.0.1:8080

# Build site
mkdocs build

# Deploy to GitHub Pages
mkdocs gh-deploy
```

## Tech Stack

- [MkDocs](https://www.mkdocs.org/) - Static site generator
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) - Theme
- GitHub Pages - Hosting
