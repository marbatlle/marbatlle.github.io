# marbatlle.github.io

Source for [marbatlle.github.io](https://marbatlle.github.io/), built with
[MkDocs](https://www.mkdocs.org/) and the
[Material](https://squidfunk.github.io/mkdocs-material/) theme, deployed to
GitHub Pages via [.github/workflows/deploy.yml](.github/workflows/deploy.yml)
on every push to `master`.

## Local development

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open http://127.0.0.1:8000/.

## Structure

- `mkdocs.yml` — site config, nav, theme
- `docs/` — page content (Markdown)
