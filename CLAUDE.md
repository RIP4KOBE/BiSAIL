# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **static academic project page** — a single-page website for presenting a research paper. It is deployed via GitHub Pages with no build step required.

## Architecture

The entire site lives in `index.html`. All content changes (paper title, authors, abstract, figures, videos, links, BibTeX) are made directly in that file.

- `index.html` — all page content and structure
- `static/css/index.css` — custom styles using CSS variables (`--primary-color`, `--shadow-*`, etc.) defined in `:root`
- `static/js/index.js` — dropdown toggle, BibTeX copy, scroll-to-top, video carousel autoplay
- `static/css/bulma*.css` / `static/js/bulma*.js` — Bulma CSS framework with carousel and slider plugins
- `static/images/` — figures, tables, favicon
- `static/videos/` — demo/teaser videos
- `static/pdfs/` — paper poster PDF

## Key Patterns in index.html

**Commented-out blocks**: Many optional sections (YouTube embed, video carousel, PDF poster, image carousel) are present but commented out. Uncomment to enable them.

**TODO markers**: Search for `TODO` or placeholder text like `YOUR REPO HERE` / `ARXIV PAPER ID` to find fields that need to be filled in.

**More Works dropdown**: Populated in the `.more-works-dropdown` div — add `.work-item` entries linking to related papers.

**BibTeX section**: The `<pre id="bibtex-code">` block is copied to clipboard by `copyBibTeX()` in `index.js`.

**Meta tags / SEO**: `<head>` contains Open Graph, Twitter Card, and Google Scholar citation meta tags — update these alongside the visible content.

**JSON-LD structured data**: Two `<script type="application/ld+json">` blocks (ScholarlyArticle and Organization) appear in `<head>` and should match the paper metadata.

## Deployment

Push to the `master` branch — GitHub Pages serves the site directly from the repo root. The `.nojekyll` file disables Jekyll processing.

---

## Step-by-Step Guide: Adapting This Template for a New Paper

### How to use this guide

Work through Steps 1–6 in order. At each step, tell Claude what information or files you have and Claude will make the edits for you. You do not need to touch the HTML directly.

---

### Step 1 — Provide Paper Metadata (text only, start here)

Tell Claude the following information. Paste it as a message and Claude will fill in all matching fields in `index.html` and the meta tags in `<head>`.

**Required:**
- Paper full title
- Author names (in order)
- Author affiliations / institutions
- Abstract (full text)
- Venue / conference name and year (e.g. "CVPR 2025")
- Publication date

**Optional but recommended:**
- arXiv paper ID (e.g. `2401.12345`)
- GitHub repository URL
- Project page URL (the URL where this site will be hosted)
- Twitter handles for the lab and first author

> Claude will update: `<title>`, all `<meta>` tags, Open Graph/Twitter Card tags, Google Scholar citation tags, JSON-LD structured data, the hero section (title, authors, affiliations), the abstract section, and the venue badge.

---

### Step 2 — Provide Links

Tell Claude which of the following you have and share the URLs:

- [ ] arXiv PDF link
- [ ] GitHub repository link
- [ ] HuggingFace model/dataset link
- [ ] Demo / Colab link
- [ ] Video link (YouTube or direct)
- [ ] Poster PDF (place file at `static/pdfs/poster.pdf`)

> Claude will wire up the correct buttons in the hero section and uncomment/hide sections that are not applicable.

---

### Step 3 — Replace Media Files

Place your files in the correct folders. Tell Claude the filenames once they are copied.

| What | Where to put it | Notes |
|---|---|---|
| Teaser / overview figure | `static/images/` | shown at top of page |
| Method diagram | `static/images/` | shown in method section |
| Result figures / tables | `static/images/` | one or more images |
| Teaser video | `static/videos/` | MP4, shown as hero video |
| Demo videos | `static/videos/` | MP4, one per result row |
| Favicon | `static/images/favicon.ico` | replace the placeholder |
| Poster PDF | `static/pdfs/poster.pdf` | optional |
| Social preview image | `static/images/social_preview.png` | 1200×630px, for link previews |

> After you drop in the files, tell Claude: "I've added the following files: [list them]" and Claude will update all `src` / `href` references in `index.html`.

---

### Step 4 — Fill in the BibTeX

Paste your BibTeX entry and Claude will insert it into the `<pre id="bibtex-code">` block.

Example format:
```bibtex
@inproceedings{yourpaper2025,
  title     = {Your Paper Title},
  author    = {Last, First and Last2, First2},
  booktitle = {Conference Name},
  year      = {2025},
}
```

---

### Step 5 — Write the Content Sections

For each section below, provide the text and Claude will update the HTML:

- **Method description** — a few sentences or paragraphs explaining your approach (goes under the method figure)
- **Results description** — caption or explanation for each result figure/video
- **Acknowledgements** — funding sources, contributors to thank (optional)
- **More Works dropdown** — 2–4 related papers from your group: title, authors, thumbnail image, URL

---

### Step 6 — Enable Optional Sections

Tell Claude which of these you want turned on (they are commented out by default):

- [ ] YouTube embed
- [ ] Video carousel (multiple demo videos in a slider)
- [ ] PDF poster viewer (Adobe embed)
- [ ] Image carousel (multiple result images in a slider)

---

### Final Checklist Before Deploying

Claude will run through this automatically when you say "do a final review":

- [ ] All TODO markers removed from `index.html`
- [ ] All placeholder text replaced (no ALL_CAPS_PLACEHOLDERS remain)
- [ ] All image `src` paths point to real files in `static/images/`
- [ ] All video `src` paths point to real files in `static/videos/`
- [ ] BibTeX block is filled in
- [ ] Meta tags and JSON-LD match the visible content
- [ ] Favicon replaced
- [ ] Site URL in meta tags matches the actual GitHub Pages URL

---

## Claude Behavior Instructions

- When the user provides paper information, always update **both** the visible HTML content **and** the corresponding `<head>` meta tags / JSON-LD in one pass.
- Before editing, search for all instances of a placeholder (e.g. `PAPER_TITLE`) across the file to catch every occurrence.
- When the user says they have added a file, ask for the exact filename before updating `src` attributes.
- Do not remove commented-out sections unless the user explicitly asks — they may want them later.
- After each step, tell the user what was changed and prompt them with what to provide next.
