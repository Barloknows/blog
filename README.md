# Barloknows

Personal blog for the CPTS journey and beyond. Built with Hugo.

**Live at:** `https://yourusername.github.io/`

---

## Quick Start

### 1. Install Hugo

```bash
# macOS
brew install hugo

# Windows (winget)
winget install Hugo.Hugo.Extended

# Linux
snap install hugo
```

Verify: `hugo version` — needs v0.110.0+

---

### 2. Clone and set up

```bash
git clone https://github.com/yourusername/barloknows.git
cd barloknows
hugo server -D
```

Open `http://localhost:1313` — live reloads on save.

---

### 3. Configure the site

Edit `hugo.toml`:

```toml
baseURL = 'https://yourusername.github.io/'
title   = 'Barloknows'

[params]
  tagline  = "Notes from someone still figuring it out."
  bio      = "HTB writeups, CPTS module notes, tool breakdowns. Written in real time."
  github   = "https://github.com/yourusername"
  linkedin = "https://linkedin.com/in/yourusername"
  htb      = "https://app.hackthebox.com/users/YOUR_ID"
```

---

### 4. Write a new post

```bash
hugo new posts/htb-machinename.md
```

This creates `content/posts/htb-machinename.md` from the archetype template.

**Front matter fields:**

```yaml
---
title: "HTB: MachineName"
date: 2025-04-18
draft: false                    # set to false when ready to publish
categories: ["HTB Writeup"]    # HTB Writeup | Study Notes | Cheatsheet | Journal
tags: ["HTB", "Easy", "Linux"]
excerpt: "One sentence summary shown on the homepage."
---
```

Category values affect the colour label on the homepage:
- `HTB Writeup` → red
- `Study Notes` → green
- `Cheatsheet` / `Journal` → grey

---

### 5. Deploy to GitHub Pages

#### First-time setup

1. Push this repo to GitHub as `yourusername/yourusername.github.io` (or any repo name)
2. Go to **Settings → Pages**
3. Set **Source** to **GitHub Actions**
4. Push to `main` — the workflow in `.github/workflows/hugo.yml` handles everything

Every push to `main` automatically builds and deploys. Takes ~30 seconds.

#### Custom domain (optional)

1. Add a `CNAME` file to `static/` containing your domain: `barloknows.com`
2. Set the DNS records at your registrar
3. Update `baseURL` in `hugo.toml` to your domain

---

## File structure

```
barloknows/
├── hugo.toml                       ← site config (edit this)
├── archetypes/
│   └── default.md                  ← post template
├── content/
│   ├── about.md                    ← about page
│   └── posts/
│       └── your-posts.md           ← all blog posts go here
├── themes/
│   └── barloknows/
│       ├── layouts/                ← HTML templates
│       └── static/css/main.css    ← all styles
└── .github/workflows/hugo.yml      ← auto-deploy
```

---

## Writing tips

### Code blocks

Use fenced code blocks with a language identifier — Hugo syntax-highlights automatically:

````markdown
```bash
$ nmap -sV -sC -p- 10.10.10.1
```
````

### Callouts / notes

Use blockquotes for callout boxes:

```markdown
> **Note:** Use -c DCOnly first for a quick pass.
```

### Linking between posts

```markdown
[See my Nmap cheatsheet](/posts/nmap-cheatsheet/)
```

---

## Customisation

All styles live in `themes/barloknows/static/css/main.css`.

Key CSS variables at the top of that file:

```css
:root {
  --bg:    #18160f;   /* page background */
  --fg:    #ede8da;   /* primary text */
  --fg2:   #a09884;   /* secondary text */
  --red:   oklch(58% 0.20 25);  /* accent — change this to retheme */
  --w:     1060px;    /* max content width */
}
```

Change `--red` to any colour to retheme the entire site.

---

## License

MIT — do whatever you want with it.
