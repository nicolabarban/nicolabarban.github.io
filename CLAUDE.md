# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Personal academic website for Nicola Barban (Professor of Demography, University of Bologna), deployed to **nicolabarban.com** via GitHub Pages (see `CNAME`). The repo is a fork of the Minimal Mistakes Jekyll theme that has been customized with the user's content; the upstream theme machinery still lives in the repo unchanged.

## What is upstream vs. user content

Treat these as **upstream theme files** — usually do not edit when changing site content:

- `_layouts/`, `_includes/`, `_sass/`, `assets/` — theme templates and styles
- `docs/`, `test/` — theme demo site and test fixtures (excluded in `_config.yml`)
- `CHANGELOG.md`, `README.md`, `minimal-mistakes-jekyll.gemspec`, `package.json`, `Rakefile`, `screenshot*.png` — upstream theme metadata (the `README.md` is the theme's, not the user's site)

Treat these as **user site content** — edit these for site changes:

- `index.md` — home page
- `about/`, `contact/`, `links/`, `news/`, `publications/`, `teaching/`, `photography/`, `laguna/` — top-level pages (each is an `index.md` or `index.html`)
- `_config.yml` — site configuration (title, author, social links, navigation defaults)
- `_data/navigation.yml` — masthead navigation links
- `_data/ui-text.yml` — translatable UI strings
- `Barban_cvOctober2020.pdf`, `assets/images/` (user-supplied images), `mailing.md`, `mailing_list_unibo.html`

## Common commands

This site is hosted on GitHub Pages, so production builds happen on GitHub's side; local commands are only for previewing changes.

```bash
bundle install                  # install Ruby/Jekyll dependencies (run once)
bundle exec jekyll serve        # serve the actual site at http://localhost:4000
bundle exec jekyll build        # one-shot static build into _site/
```

The repo's `Rakefile` provides `bundle exec rake preview`, but that task serves the **theme's `test/` demo site**, not this user's site. Use `jekyll serve` to preview real changes to `index.md`, the page directories, and `_config.yml`.

## Conventions to be aware of

- **Permalinks for top-level pages** are folder-based: a page lives at e.g. `publications/index.md` and is served at `/publications/`. The `permalink` in `_config.yml` (`/:categories/:title/`) only governs posts, not these pages — adding a new section means creating `<section>/index.md` with appropriate front matter.
- **Navigation** is driven by `_data/navigation.yml`, not by filesystem discovery. New top-level pages must be added there to appear in the masthead.
- **Author/social config** lives in `_config.yml` under `author:` and is rendered into every page via the author profile sidebar — change once there, not per-page.
- `_config.yml` is **not reloaded** by `jekyll serve`; restart the server after editing it.
- `docs/` and `test/` are explicitly excluded from the build (`_config.yml` `exclude:`); don't put site content there.
