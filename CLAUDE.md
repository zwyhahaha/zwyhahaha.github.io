# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Site Overview

This is a personal Jekyll blog (zwyhahaha.github.io) for Wanyu Zhang — an academic/research blog covering optimization, machine learning, and travel. It is deployed via GitHub Pages.

## Development Commands

**Local preview (requires Jekyll installed):**
```bash
jekyll serve
```

**Compile LESS to CSS (requires npm dependencies):**
```bash
grunt          # compile JS and LESS, add banners
grunt watch    # watch for changes
```

**Python-based static preview of built site:**
```bash
cd _site; python3 -m http.server 8020
```

## Content Architecture

- **`_posts/`** — Published blog posts (Markdown). Naming: `YYYY-MM-DD-title.md`
- **`_drafts/`** — Unpublished drafts (no date prefix needed)
- **`_layouts/`** — Page templates: `default.html` (base), `post.html` (blog posts), `page.html`, `keynote.html`
- **`_includes/`** — Reusable partials: `head.html`, `nav.html`, `footer.html`
- **`img/`** — Images organized by post/topic in subdirectories
- **`less/`** — LESS source files compiled to `css/`
- **`_config.yml`** — Site-wide configuration (title, social links, plugins, MathJax settings)

## Post Front Matter

Every post requires this front matter:

```yaml
---
layout:     post
title:      "Post Title"
subtitle:   "Optional subtitle"
date:       YYYY-MM-DD
author:     Wanyu Zhang
header-img: img/some-image.jpeg
catalog:    true   # enables sidebar table of contents
tags:
    - TagName
---
```

Set `catalog: false` for posts without a table of contents (e.g., travel/photo posts).

## Math Rendering

Posts use MathJax 3 (loaded in `post.html`). Use standard LaTeX syntax:
- Inline: `$...$` or `\(...\)`
- Display: `$$...$$` or `\[...\]`
- The `bm` package is available for bold math (`\bm{}`)

## Images in Posts

Reference images relative to site root:
```html
<img src="{{ site.baseurl }}/img/subfolder/image.jpeg" alt="description" style="width: 90%; height: auto;">
```

Store images in `img/<post-topic>/` subdirectories.

## Key Configuration

- Tags with more than 2 posts appear on the homepage (`featured-condition-size: 2` in `_config.yml`)
- Gitalk comments are disabled by default (`gitalk.enable: false`)
- PWA/service worker is enabled (`service-worker: true`)
- Markdown engine: kramdown with GFM input; syntax highlighting: rouge
