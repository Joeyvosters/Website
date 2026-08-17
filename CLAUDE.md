# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

"Sideline & Shoreline" — a personal Jekyll blog (fishing/soccer/DIY/life notes), hosted on GitHub Pages with no local build step required (GitHub builds it on push). There is no local Jekyll install, Gemfile, or CI in this repo — GitHub Pages handles the build server-side.

## Commands

There is no local build/test tooling. To preview changes, either push to `main` and let GitHub Pages rebuild, or install Jekyll locally (`bundle exec jekyll serve`) — no `Gemfile` is currently checked in, so that requires setting one up first.

## Architecture

**Content model**: every post is a Markdown file in `_posts/`, filename `YYYY-MM-DD-title.md`, with required front matter:

```yaml
layout: post
title: "..."
category: Fishing   # or Soccer, DIY, Life — must match one of the four exactly
excerpt: "..."       # shown in feed listings, not auto-truncated from body
```

**Categories are wired in three places that must stay in sync**:
1. `_config.yml` → `categories_order` — defines the four categories, display order, and each one's accent color (hex).
2. `assets/css/style.css` → `--tab-fishing`, `--tab-soccer`, `--tab-diy`, `--tab-life` custom properties — must match the hex values in `_config.yml`.
3. `category/*.html` — one static page per category (`fishing.html`, `soccer.html`, `diy.html`, `life.html`), each just front matter (`layout: category`, `category: <Name>`) with no body content; the `category` layout does the actual listing via `site.categories[page.category]`.

Adding a fifth category means updating all three, plus adding a `.tab-<name>-bg` CSS class (the same `tab-<name>-bg` class is applied in layouts as `tab-{{ category | downcase }}-bg`, so the class name must be the lowercased category name).

**Layouts** (`_layouts/`):
- `default.html` — the shell (masthead, nav tabs generated from `site.categories_order`, footer). All other layouts render inside this one's `{{ content }}`.
- `post.html` — single post view. Computes a descending "entry number" (`No. N`) by finding the post's index in `site.posts` (which Jekyll orders newest-first) and subtracting from the total — so entry numbers count up from the oldest post, newest post always has the highest number.
- `category.html` — per-category archive; same entry-numbering logic as `post.html`, scoped to `site.categories[page.category]`.
- `index.html` (root) inlines the same entry-card feed markup again rather than reusing a layout — if you change the feed card markup, it currently needs to be updated in three places: `index.html`, `_layouts/category.html`, and implicitly wherever else a feed is rendered.

**Permalinks**: posts use `permalink: /log/:year/:month/:day/:title/` (set in `_config.yml`), not Jekyll's default `/category/year/...` scheme.

**baseurl**: `_config.yml` sets `baseurl: "/Website"` because this repo is not named `<username>.github.io` — it's served at `https://<username>.github.io/Website/`. If the repo is ever renamed, `baseurl` must be updated to match (or cleared if moved to a root `username.github.io` repo).
