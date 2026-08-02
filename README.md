# Sideline & Shoreline

A simple personal blog built with Jekyll, ready to host free on GitHub Pages.
GitHub builds the site automatically — you never need to install anything
on your own computer.

## 1. Create a GitHub account

Go to https://github.com/join and sign up (free).

## 2. Create the repository

1. Click the **+** in the top right → **New repository**.
2. **Repository name** — this matters:
   - For a site at `https://<your-username>.github.io` (the simplest, root
     URL), name the repo exactly `<your-username>.github.io`
     (e.g. `joeyc.github.io`).
   - Or, pick any other name (e.g. `blog`) and your site will live at
     `https://<your-username>.github.io/blog/` instead. If you do this,
     open `_config.yml` after uploading and set `baseurl: "/blog"`
     (matching whatever you named the repo).
3. Set it to **Public**, leave "Add a README" unchecked, click **Create repository**.

## 3. Upload these files

On the new repo's page:

1. Click **Add file → Upload files**.
2. Drag in every file and folder from this project, keeping the folder
   structure intact (`_layouts/`, `_posts/`, `category/`, `assets/`, plus
   `_config.yml`, `index.html`, `about.md`).
3. Scroll down and click **Commit changes**.

(Folders will only upload correctly if your browser lets you drag a whole
folder in — if it flattens them, use GitHub Desktop or `git` from a
terminal instead: `git clone`, copy the files in, `git add .`,
`git commit -m "first commit"`, `git push`.)

## 4. Turn on GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to
   **Deploy from a branch**.
3. Set **Branch** to `main` (or `master`) and folder to `/ (root)`.
4. Click **Save**.

GitHub will build the site (takes 1-2 minutes). The Pages settings page
will show you the live URL once it's ready.

## 5. Write your first real post

Every blog post is a Markdown file in `_posts/`, named like:

```
YYYY-MM-DD-a-short-title.md
```

with this at the top:

```
---
layout: post
title: "Your post title"
category: Fishing   # or Soccer, DIY, Life
excerpt: "One or two sentences that show up in the feed."
---

Your post content goes here, in plain Markdown.
```

Delete or edit the three sample posts once you've got your own entries in.

## Structure

- `_config.yml` — site title, tagline, and category tab colors
- `_layouts/` — page templates (don't need to touch these)
- `_posts/` — your blog entries (add new ones here)
- `category/` — the four category archive pages (Fishing/Soccer/DIY/Life)
- `about.md` — your About page copy
- `assets/css/style.css` — all the styling, if you want to tweak colors or fonts
