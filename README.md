# Poll Bot - onboarding site

A polished, fully static onboarding guide for **Poll Bot**, a Telegram scheduling
bot built in a Google Sheet (Google Apps Script). It walks a non-technical user
through setup in ~20 minutes.

Lives at: **https://pollbot.urbanalgorithm.com**

Plain HTML + CSS only - no frameworks, no build step (the Inter webfont loads
from Google Fonts). A tiny bit of optional vanilla JS (mobile nav toggle + copy
buttons) lives inline in `index.html` and degrades gracefully if JS is disabled.

## Folder contents

```
pollbot-site/
├── index.html              # the whole page
├── assets/
│   └── css/styles.css      # all styles
├── CNAME                   # custom domain for GitHub Pages
└── README.md               # this file
```

## Preview locally

Just open `index.html` in a browser - it works straight from disk.

Or serve it (closer to production, avoids any file-path quirks):

```bash
cd pollbot-site
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

This site is set up to host on **GitHub Pages** with the custom subdomain
`pollbot.urbanalgorithm.com` (the included `CNAME` file wires that up).

1. Create a GitHub repository (e.g. `pollbot-site`). Put these files at the repo
   **root**: `index.html`, the `assets/` folder, `CNAME`, and this `README.md`.
2. Commit and push to the `main` branch.
3. In the repo: **Settings → Pages → "Build and deployment" → Source:
   _Deploy from a branch_ → Branch: `main`, folder: `/ (root)` → Save.**
4. Still on **Settings → Pages → "Custom domain"**: enter
   `pollbot.urbanalgorithm.com` → Save. (The included `CNAME` file already sets
   this; GitHub will verify it.)
5. Wait for the DNS check to pass, then tick **Enforce HTTPS** (GitHub
   auto-provisions a free Let's Encrypt certificate - this can take a few
   minutes).

### DNS setup

At the DNS host for `urbanalgorithm.com`, add **one** record:

- **Type:** `CNAME`
- **Host / Name:** `pollbot`
- **Value / Target:** `natedesmond.github.io`
  - include the trailing dot if your provider requires it.
- **TTL:** default / automatic.

This is a subdomain, so a CNAME record is correct. (Only an apex/root domain
would need A records pointing to GitHub's IP addresses - not the case here.)

Propagation usually takes a few minutes to ~an hour. Verify with:

```bash
dig pollbot.urbanalgorithm.com +short   # should resolve to *.github.io
```

…or a checker like [whatsmydns.net](https://www.whatsmydns.net/). Once it
resolves, enable **Enforce HTTPS** as in step 5 above.

## TODO

- [ ] **Set the template sheet to “Anyone with the link → Viewer”** so the
      "Make a copy" link works for everyone who visits.

## The "Make a copy" link

The primary CTA links to:

```
https://docs.google.com/spreadsheets/d/1-Rb3YjKW17p5A1QzJ-YvjGC64wqtXET6XEJggYZOXBg/copy
```

The trailing `/copy` opens Google's "Make a copy" dialog. For it to work for
other people, the source sheet must be shared (see TODO above).
