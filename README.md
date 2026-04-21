# CSOM Global — csom.global

Single-file static website for **CSOM™ Global** — the Customer Success Operating Model.

- **Live:** https://csom.global
- **Source:** `index.html` (self-contained: inline CSS, inline JS, Google-Fonts CDN only)
- **Host:** Vercel (auto-deploys on every push to `main`)

---

## Edit → Publish flow

Every edit is a one-liner once the remote is wired up.

```bash
# 1. Open the file in any editor
code index.html          # or notepad, cursor, anything

# 2. Commit and push — Vercel rebuilds in ~15s
git add index.html
git commit -m "Update hero copy"
git push
```

That's it. Within ~20 seconds, https://csom.global reflects the change.

---

## Preview locally before publishing

```bash
# Option A — Python (already installed on most machines)
python -m http.server 8000
# → open http://localhost:8000

# Option B — Node
npx serve .
```

Hard-reload (**Ctrl+Shift+R**) if you don't see your edit — the browser caches aggressively.

---

## File layout

```
csom-global-site/
├── index.html      ← THE site. Everything lives here.
├── vercel.json     ← Host config (security headers, clean URLs)
├── .gitignore
└── README.md       ← this file
```

Zero build step. Zero dependencies. The file is ~120 KB and loads in under a second on 4G.

---

## Common edits — where to find what

Inside `index.html`, search for:

| You want to change…          | Search for…                              |
|-------------------------------|------------------------------------------|
| Hero headline                | `class="hero-title"`                     |
| The 7 disciplines + 2 orbits | `planets =` (JS array near bottom — first 7 items render as disciplines, last 2 as orbits) |
| "Why it fails" cards         | `class="fails-card"`                     |
| Contact email / socials      | `class="contact"`                        |
| Brand colors                 | `:root {` (CSS variables at top)         |
| Page title / meta SEO        | `<title>` and `<meta`                    |

---

## Rolling back

```bash
git log --oneline                # find the commit you want
git revert <commit-sha>          # safe: creates a new commit that undoes it
git push
```

Vercel auto-deploys the revert. Every past version is also available on the Vercel dashboard → Deployments → Promote to Production.

---

## DNS / domain notes (reference only — set once)

- Domain `csom.global` points to Vercel via:
  - `A` record: `76.76.21.21`
  - `CNAME` record: `www` → `cname.vercel-dns.com`
- **Do not modify MX records** (Google Workspace email lives there).

---

## Support

Drop a note in `git commit` messages or open an issue in this repo. Claude can pick up context from this README alone.
