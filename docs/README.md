# SovBot Docs — Getting Started

## Prerequisites
- Python 3.8+
- pip

## Install
```bash
pip install mkdocs mkdocs-material
```

## Serve locally
```bash
mkdocs serve
```
Open http://127.0.0.1:8000 in your browser.

## Build static site
```bash
mkdocs build
```
Static files will be generated into the `site/` directory.

## Structure
- `mkdocs.yml` — site config and navigation
- `docs/` — content
  - `index.md` — Home
  - `workflows/onboarding.md` — Onboarding Workflow
  - `commands/*.md` — Command reference
  - `outstanding-decisions.md` — Team checklist
  - `change-log.md` — Chronological changes
  - `assets/` — Images and GIFs referenced by docs

## Notes
- Follow the SovBot Markdown Style Guide:
  - Use `#` for titles, `##` for sections, `###` for subsections.
  - Separate Current Behavior vs Expected Behavior on command pages.
  - Add Notes section to every page (even if empty).
