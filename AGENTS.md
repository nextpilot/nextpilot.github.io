# Agent Instructions for NextPilot Docs Center

This repository contains the NextPilot documentation website built with MkDocs.
Agents should treat it as a documentation site repository, not a software library or application codebase.

## Repository purpose

- Hosts the documentation website source for NextPilot.
- Uses MkDocs + Material theme and static site generation.
- Primary content lives under `docs/`.

## Key workflows

- Install dependencies: `pip install -r docs/requirements.txt`
- Build site locally: `mkdocs build`
- Preview locally: `mkdocs serve`
- Deploy site via GitHub Actions: `.github/workflows/mkdocs-gh-deploy.yml`

## Important files

- `mkdocs.yml` — MkDocs site configuration, plugins, theme, and i18n settings.
- `docs/` — site content directory.
- `docs/.nav.yml` — navigation structure for the site.
- `docs/requirements.txt` — Python dependencies for building the docs.
- `docs/overrides/` — theme customization templates.
- `docs/index.md`, `docs/intro`, and other `.md` files under `docs/` — actual page source.
- `build/gh-pages` — generated site output; do not edit directly.

## Project conventions

- The site uses `mkdocs-static-i18n` with language suffixes for Chinese and English.
- Navigation is managed via `docs/.nav.yml`; changes to page structure should keep the nav in sync.
- Chinese filenames and markdown content are used throughout; preserve file names and links when editing.

## Recommended agent behavior

- Focus on editing documentation content, navigation, or site config.
- Do not modify generated output in `build/gh-pages`.
- When adding pages, ensure they are referenced in `docs/.nav.yml` and exist under `docs/`.
- Use the existing README and `mkdocs.yml` as the source of truth for build/deploy commands.

## References

- [README.md](README.md)
- [mkdocs.yml](mkdocs.yml)
- [docs/.nav.yml](docs/.nav.yml)
- [.github/workflows/mkdocs-gh-deploy.yml](.github/workflows/mkdocs-gh-deploy.yml)
