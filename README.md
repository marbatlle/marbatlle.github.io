# marbatlle.github.io

Personal site built with [MkDocs](https://www.mkdocs.org/) and
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

## Structure

```
docs/
  index.md              Home: profile, experience, education, certifications, projects
  projects.md           Projects tab
  notes/                Notes tab (one folder per topic)
  images/               Avatar and note figures
  files/                PDFs (theses)
  stylesheets/extra.css Custom styling
mkdocs.yml              Site config and navigation
```

## Local preview

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open http://127.0.0.1:8000.

## Deploy

Pushing to `master` triggers `.github/workflows/deploy.yml`, which builds the
site and publishes it to GitHub Pages.
