# Shizuka (静か)

[![Hugo Version](https://img.shields.io/badge/Hugo-0.100.0+-blue)](https://gohugo.io/)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-brightgreen)](LICENSE)
[![GitHub Release](https://img.shields.io/github/v/release/carmelolg/shizuka)](https://github.com/carmelolg/shizuka/releases)
[![GitHub Stars](https://img.shields.io/github/stars/carmelolg/shizuka?style=social)](https://github.com/carmelolg/shizuka)

A minimal, clean Hugo blog theme inspired by the Japanese aesthetic of *shibui* — quiet elegance, nothing in excess.

**[Live Demo](https://carmelolg.github.io/shizuka/)**

---

## ✨ What is Shizuka?

Shizuka (静か) means "quiet" or "calm" in Japanese. This theme is built for writers and thinkers who value clarity and simplicity. 

**No sidebars. No distractions. Just clean typography and your words.**

---

## 🚀 Quick Start (5 minutes)

### 1. Install the theme

```bash
git submodule add https://github.com/carmelolg/shizuka themes/shizuka
```

### 2. Create your config

Copy this to `hugo.toml`:

```toml
baseURL  = "https://yourusername.github.io/"
title    = "My Blog"
theme    = "shizuka"
languageCode = "en"

[params]
  description = "A blog about writing and thinking"
  author      = "Your Name"
  tagline     = "Slow writing, clear thinking."
```

### 3. Create your first post

```bash
hugo new posts/hello-world.md
```

Edit `content/posts/hello-world.md`:

```yaml
---
title: "Hello World"
date: 2024-04-21
draft: false
summary: "My first post on Shizuka."
---

# Welcome

This is your first post. Write anything you want.
```

### 4. Preview locally

```bash
hugo server
```

Visit `http://localhost:1313/` 🎉

---

## 📚 Complete User Guide

### Features

- ✅ Clean, distraction-free reading layout
- ✅ Dark mode — auto-detect via `prefers-color-scheme` + manual toggle
- ✅ Reading time estimate on every post
- ✅ Archive page grouped by year
- ✅ RSS feed
- ✅ Tags and categories taxonomy
- ✅ Optional per-post table of contents (`toc: true`)
- ✅ Responsive design (mobile-first)
- ✅ i18n support (English and Italian built-in)
- ✅ No JavaScript frameworks — vanilla JS only

### Requirements

- [Hugo Extended](https://gohugo.io/installation/) v0.100.0 or later

### Installation Methods

#### Option A: Git Submodule (Recommended)

```bash
git submodule add https://github.com/carmelolg/shizuka themes/shizuka
```

Then set `theme = "shizuka"` in your `hugo.toml`.

#### Option B: Hugo Module

In your `hugo.toml`:

```toml
[module]
  [[module.imports]]
    path = "github.com/carmelolg/shizuka"
```

### Full Configuration Guide

Create or update your `hugo.toml` with these settings:

```toml
baseURL  = "https://yourusername.github.io/"
languageCode = "en"
title    = "My Blog"
theme    = "shizuka"
paginate = 5

[params]
  # Required
  description = "A short description of your blog"
  author      = "Your Name"
  tagline     = "Your tagline here"
  
  # Optional social links
  website = "https://yourwebsite.com"
  github  = "https://github.com/yourusername"
  
  # Appearance
  dateFormat = "January 2, 2006"
  ogImage    = "/images/og-default.png"
  rssLimit   = 20

[outputs]
  home    = ["HTML", "RSS"]
  section = ["HTML", "RSS"]

[taxonomies]
  tag      = "tags"
  category = "categories"
  series   = "series"

[menu]
  [[menu.main]]
    name   = "Blog"
    url    = "/posts/"
    weight = 1
  [[menu.main]]
    name   = "Archive"
    url    = "/archive/"
    weight = 2
  [[menu.main]]
    name   = "About"
    url    = "/about/"
    weight = 3
```

### Content Structure

Here's what your `content/` folder should look like:

```
content/
├── _index.md           ← Home page intro (optional)
├── about.md            ← About page
├── archive.md          ← Archive (with layout: archive)
└── posts/
    ├── _index.md       ← Posts index (required)
    ├── first-post.md
    └── second-post.md
```

### Writing Posts

Every post needs front matter:

```yaml
---
title: "My Post Title"
date: 2024-04-21
draft: false
summary: "Short summary shown in listings. Keep it under 160 characters."
tags:
  - writing
  - thoughts
categories:
  - meta
toc: false  # Set to true for long posts with headers
---

# Your post content

Write in Markdown. Hugo will handle the rest.
```

**Field Reference:**
- `title` — Post title (required)
- `date` — Publication date (required)
- `draft` — Set to `false` to publish (default: `true`)
- `summary` — Shown in post listings (optional but recommended)
- `tags` — Flexible categorization (optional)
- `categories` — Structured organization (optional)
- `toc` — Show table of contents (optional, default: `false`)

### Setting Up Special Pages

#### Home Page Intro

Create `content/_index.md`:

```yaml
---
---

# Welcome to my blog

This text appears at the top of your home page.
```

#### About Page

Create `content/about.md`:

```yaml
---
title: "About"
---

# About Me

Tell the world about yourself.
```

#### Archive Page

Create `content/archive.md`:

```yaml
---
title: "Archive"
layout: "archive"
---
```

This automatically groups posts by year.

### Languages & Translations

The theme comes with **English** and **Italian** built-in.

#### Using Italian

Set `languageCode = "it"` in `hugo.toml`:

```toml
languageCode = "it"
```

#### Adding Custom Languages

1. Copy `i18n/en.toml` → `i18n/[lang-code].toml`
2. Translate the values
3. Set `languageCode = "[lang-code]"` in your config

### Customizing Colors

Edit `assets/css/main.css` at the top of the file:

```css
:root {
  --color-text:    #1a1a1a;    /* Text color */
  --color-bg:      #fafaf8;    /* Background */
  --color-accent:  #2a6496;    /* Links & accents */
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-text:    #f5f5f5;
    --color-bg:      #1a1a1a;
    --color-accent:  #5b9bd5;
  }
}
```

---

## 🧪 Testing Locally

### Preview the exampleSite

```bash
cd exampleSite
hugo server --themesDir ../..
```

Open `http://localhost:1313/`

### Build for Production

```bash
hugo --minify
```

Output goes to `public/`

---

## 💡 Tips & Best Practices

### For Better Readability
- Use clear headings (##, ###)
- Keep paragraphs short
- Write summaries for posts

### For SEO
- Set a good `summary` on each post
- Use descriptive URLs
- Add `ogImage` for social sharing

### For Performance
- Keep images under 500KB
- Use Hugo's image processing
- Build with `--minify` for production

---

## ⚙️ Advanced Customization

### Adding Custom Fonts

Edit `layouts/partials/head.html` to add font imports.

### Modifying Layouts

Copy layouts from `layouts/` to your site root under `layouts/` and modify them.

### Adding JavaScript

Keep it minimal! Edit `layouts/partials/head.html` for `<head>` scripts or `layouts/partials/footer.html` for `</body>` scripts.

---

## 📄 License

[CC-BY-4.0](LICENSE) (Creative Commons Attribution 4.0) — © carmelolg

This work requires attribution in any redistribution or use.
