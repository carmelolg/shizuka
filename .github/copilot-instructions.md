# Copilot Instructions — Shizuka Hugo Theme

## What This Is

**Shizuka** is a Hugo blog theme (not a site). The source is in the repo root; the `exampleSite/` subdirectory is a self-contained demo site used for local testing, CI, and GitHub Pages deployment.

---

## Build & Preview

All commands that build/preview content use `exampleSite/` as working directory with `--themesDir ../..` to point Hugo at the theme root.

```bash
# Preview the demo site with live reload
cd exampleSite && hugo server --themesDir ../..

# Build the demo site (CI-equivalent)
cd exampleSite && hugo --themesDir ../..

# Production build (minified, used by deploy workflow)
cd exampleSite && hugo --minify --themesDir ../.. --baseURL="https://carmelolg.github.io/shizuka/"
```

**Requirement:** Hugo Extended v0.100.0+. CI tests against `latest` and `0.120.0`.

---

## Architecture

```
layouts/
  _default/         # Core templates: baseof, single, list, archive, terms
  partials/         # Reusable fragments: head, header, footer, meta, analytics, cookie-consent*
assets/css/
  main.css          # Single stylesheet, processed via Hugo Pipes with fingerprinting
i18n/
  en.toml           # English strings
  it.toml           # Italian strings
exampleSite/        # Demo site (content, config, themes/ symlink target)
```

The `baseof.html` template defines the full HTML shell. All page types (`single`, `list`, `archive`) use `{{ define "main" }}` blocks inside it. Inline JavaScript for dark-mode persistence lives directly in `baseof.html`.

CSS is loaded via Hugo Pipes:
```go
{{ $css := resources.Get "css/main.css" | fingerprint }}
<link rel="stylesheet" href="{{ $css.RelPermalink }}">
```

---

## Key Conventions

### i18n strings
Every user-visible string goes through `{{ i18n "key" }}`. When adding new UI text, add the key to **both** `i18n/en.toml` and `i18n/it.toml`.

### Theming (dark/light mode)
- CSS custom properties (`--color-text`, `--color-bg`, `--color-accent`) defined in `:root` and overridden with `[data-theme="dark"]`.
- The `data-theme` attribute is set on `<html>` via inline JS in `baseof.html`, reading from `localStorage` key `theme`.
- Do not use `prefers-color-scheme` media queries for logic — those are only fallbacks. Theme state is driven by `data-theme`.

### Analytics & Cookie Consent
- `analytics.html` receives the GA ID via `.` context (called as `{{ partial "analytics.html" . }}`).
- Cookie consent is gated on **both** `googleAnalyticsID` and `enableCookieConsent` being set.
- Consent state is stored in a cookie named `shizuka-cookie-consent` (value: `accepted` / `rejected`).
- The banner and the analytics script check this cookie; they are independent partials (`cookie-consent.html`, `cookie-consent-script.html`).

### Layout CSS classes
- `site-wrapper` — max-width container, used in `baseof.html`
- `content-narrow` — narrower reading-width container, used on `single.html` and other focused views

### Post front matter
Required: `title`, `date`. Optional but expected: `summary`, `tags`, `categories`, `toc` (bool), `comments` (bool — set to `false` to disable the comment section on a specific post).  
The Archive page requires `layout: "archive"` in its front matter to pick up `layouts/_default/archive.html`.

### Adding a new language
1. Copy `i18n/en.toml` → `i18n/[lang-code].toml` and translate all values.
2. No template changes needed — Hugo resolves strings via `languageCode` automatically.

### Comments (Cusdis)
Set `cusdisAppId` in `[params]` to enable comments sitewide. Comments render via a custom form + Cusdis REST API (no iframe). The partial is `layouts/partials/comments.html` and is included at the bottom of `layouts/_default/single.html`. Disable per-post with `comments: false` in front matter. The display name sent to Cusdis is `"First Last (nickname)"` if optional name fields are filled, otherwise just the nickname.

---

## CI Workflows

| File | Trigger | What it does |
|------|---------|--------------|
| `build.yml` | Every push/PR | Builds `exampleSite` with Hugo `latest` and `0.120.0` |
| `deploy.yml` | Push to `master` | Builds with `--minify` and deploys to GitHub Pages |
