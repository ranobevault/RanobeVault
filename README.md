# RanobeVault — Static Light Novel CMS

A fully static light novel reading website for GitHub Pages. No backend, no database — just JSON files and JavaScript.

## Quick Start

### 1. Fork / Upload to GitHub
Upload all files to a GitHub repository and enable GitHub Pages (Settings → Pages → Deploy from branch: `main`, folder: `/root`).

### 2. Configure Admin Panel
Open `admin.html` and fill in:
- **GitHub Username** — your GitHub username
- **Repository Name** — your repo name (e.g. `novashelves`)
- **Branch** — `main` (or `gh-pages`)
- **Personal Access Token** — [Create one here](https://github.com/settings/tokens) with `repo` scope

Click **Test** to verify, then **Save**.

### 3. Add Your First Series
Go to the **New Series** tab:
1. Enter title, author, genres, synopsis
2. Enter cover image URL (or use a placeholder)
3. Upload your first chapter as a `.json` or `.txt` file
4. Click **Upload & Publish**

The admin will automatically update all JSON files.

---

## File Structure

```
/
├── index.html          # Homepage
├── series.html         # Series info + chapter list
├── chapter.html        # Chapter reader
├── admin.html          # Admin CMS panel
├── data/
│   ├── series.json     # All series metadata
│   ├── update.json     # Recent updates feed
│   ├── hashmap.json    # Hash → chapter file mapping (anti-scraping)
│   └── chapters/
│       ├── f7n2x.json              # Chapter content (randomized names)
│       ├── q1r8p.json
│       ├── {series-id}-index.json  # Chapter list per series
│       └── ...
```

## Chapter File Format

**JSON format:**
```json
{
  "title": "Volume 1 Chapter 1 — Prologue",
  "volume": 1,
  "chapter": 1,
  "series": "your-series-id",
  "content": [
    "Paragraph one goes here.",
    "Paragraph two goes here.",
    "And so on..."
  ]
}
```

**Plain text format (.txt):**
Just write paragraphs separated by blank lines. The admin will convert it automatically.

## Adwall Setup

In `series.html`, find `handleLocked()` and update the URL:
```js
window.location.href = `https://your-adwall.com/?next=${returnUrl}`;
```

In `chapter.html`, find `showAdwall()` and update:
```js
link.href = `https://your-adwall.com/?next=${returnUrl}`;
```

## Anti-Scraping

- Chapter URLs use random hashes: `chapter.html?h=k3mX9pQrL`
- Chapter files have random names: `f7n2x.json`
- No sequential or predictable URLs
- All content loaded dynamically via JavaScript

## URL Structure

| Page | URL |
|------|-----|
| Homepage | `index.html` |
| Series | `series.html?id=my-series` |
| Chapter | `chapter.html?h=HASH` |
| Admin | `admin.html` |
