# 漢字クイズ · JLPT Study App

JLPT N5–N3 study app — kanji, kana, grammar, Pokémon quiz. Single-file PWA, installable on iOS and Android.

## Features

- Kanji flashcards (N5/N4)
- Hiragana & Katakana quiz
- Mixed kana rapid-fire
- Furigana (ruby text) kanji reading mode
- Grammar reference — particles, adjective conjugation, verb forms (15 forms), patterns (N5/N4/N3)
- Sentences / phrases flashcard bank
- Pokémon katakana quiz (image, katakana→English, English→katakana)
- My Words — custom vocabulary with AI register analysis
- PWA — installable, works offline

---

## Deploy to Vercel (recommended)

### Option A — Vercel CLI (fastest)

```bash
# 1. Install Vercel CLI globally if you haven't
npm i -g vercel

# 2. From this directory
vercel

# 3. Follow prompts:
#    - Link to your Vercel account
#    - Project name: jlpt-study (or whatever you want)
#    - Framework: Other
#    - Build command: (leave blank)
#    - Output directory: public
#    - Deploy!

# 4. Add custom domain in Vercel dashboard
#    e.g. jlpt.vespertene.com → add CNAME in Cloudflare
```

### Option B — GitHub + Vercel (recommended for ongoing updates)

```bash
# 1. Create a new GitHub repo
gh repo create jlpt-study --public
# or via github.com → New repository

# 2. Push this project
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/jlpt-study.git
git push -u origin main

# 3. Go to vercel.com → Add New Project → Import from GitHub
#    - Root directory: ./
#    - Framework: Other
#    - Build command: (leave blank)
#    - Output directory: public
#    - Deploy

# 4. Every git push to main auto-deploys
```

---

## Custom Domain (jlpt.vespertene.com)

Since vespertene.com is on Cloudflare:

1. In Vercel dashboard → your project → Settings → Domains
2. Add `jlpt.vespertene.com`
3. Vercel gives you a CNAME value like `cname.vercel-dns.com`
4. In Cloudflare DNS → Add record:
   - Type: `CNAME`
   - Name: `jlpt`
   - Target: `cname.vercel-dns.com`
   - Proxy: **DNS only** (grey cloud) — Vercel handles SSL
5. Done — HTTPS auto-provisioned by Vercel

---

## PWA Installation

**Android (Chrome)**
- Visit the site → Chrome shows "Add to Home Screen" banner
- Or: three-dot menu → "Install app"
- The app opens full-screen with no browser chrome

**iOS (Safari)**
- Visit the site in Safari (must be Safari, not Chrome on iOS)
- Tap the Share button → "Add to Home Screen"
- Name it and tap Add
- Opens as standalone app with dark status bar

**Desktop (Chrome/Edge)**
- Address bar shows an install icon on the right
- Click it → "Install"

---

## Local Development

```bash
npm install
npm run dev
# Open http://localhost:3000
```

---

## Updating the App

The app is a single file: `public/index.html`

After editing:
```bash
git add public/index.html
git commit -m "Update: describe what changed"
git push
# Vercel auto-deploys in ~30 seconds
```

---

## Structure

```
jlpt-study/
├── public/
│   └── index.html      # The entire app — HTML + CSS + JS
├── vercel.json          # Vercel routing + cache headers
├── package.json         # Dev server (serve)
├── .gitignore
└── README.md
```

---

## Tech

- Pure HTML/CSS/JS — zero dependencies, zero build step
- Sprites: embedded as base64 data URIs (no external requests)
- Storage: localStorage for My Words, Sentences, progress
- AI: Anthropic Claude API for register analysis (requires API key in browser)
- PWA: inline manifest blob + service worker blob (works from single file)
