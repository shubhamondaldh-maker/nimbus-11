# Nimbus Cloudworks Engineering Blog

A fast, lightweight, and maintainable engineering blog built with [Astro](https://astro.build) and Markdown Content Collections for the engineering team at Nimbus Cloudworks.

Zero heavy UI frameworks. Static-first. Designed for developer ergonomics and long-term maintainability.

---

## ⚡ How to Run It

```bash
# 1. Install dependencies
npm install

# 2. Start local development server (http://localhost:4321)
npm run dev

# 3. Build for production (builds cleanly with zero warnings into ./dist)
npm run build
```

*(Optional preview: run `npm run preview` to inspect the production bundle locally).*

---

## ✍️ How to Add a New Post (Under 5 Lines)

Create a new file in `src/content/blog/<slug>.md`:

```markdown
---
title: "Your Post Title"
description: "A concise one-line summary of the post."
pubDate: 2026-10-27
author: "Nimbus Engineering"
tags: ["devops", "cloud"]
---
Write your markdown content here.
```

That's it! Astro automatically:
1. Validates the frontmatter against the schema.
2. Generates the post page at `/posts/<slug>`.
3. Prepends it to the home page (newest first).
4. Generates and links the relevant tag pages at `/tags/<tag>`.
5. Updates the RSS feed (`/rss.xml`) and Sitemap (`/sitemap-index.xml`).

---

## 📁 Project Architecture

```text
.
├── public/                 # Static assets & SVG favicon
├── src/
│   ├── components/         # Reusable Astro UI components
│   │   ├── Header.astro    # Sticky navigation with active route highlights & RSS
│   │   ├── Footer.astro    # Footer with sitemap, topics, and copyright
│   │   └── PostCard.astro  # Post preview cards with reading time estimate
│   ├── content/
│   │   └── blog/           # Markdown blog posts
│   │       ├── why-we-moved-ci-from-25-to-6.md
│   │       ├── postgres-indexes-we-wish-we-had-added-earlier.md
│   │       └── our-incident-checklist-in-plain-words.md
│   ├── content.config.ts   # Astro 5 Content Collection schema (Zod validation)
│   ├── layouts/
│   │   └── BaseLayout.astro # Shared layout with SEO, OpenGraph & meta descriptions
│   ├── pages/
│   │   ├── index.astro     # Home page listing all posts sorted newest first
│   │   ├── about.astro     # About Nimbus Cloudworks engineering page
│   │   ├── 404.astro       # Custom 404 page
│   │   ├── rss.xml.js      # Automated RSS 2.0 feed generator
│   │   ├── posts/
│   │   │   └── [slug].astro # Dynamic post page generated from collections
│   │   └── tags/
│   │       ├── index.astro  # Tag index with post counts
│   │       └── [tag].astro  # Filtered posts by tag (newest first)
│   └── styles/
│       └── global.css      # Dark-mode design system & responsive layout styles
├── astro.config.mjs        # Astro configuration & sitemap integration
├── package.json
└── tsconfig.json
```

---

## 🛡️ Frontmatter Schema Validation

All posts are validated at build time via `src/content.config.ts` using Zod:

| Field | Type | Description |
| :--- | :--- | :--- |
| `title` | `string` | Headline of the dispatch |
| `description` | `string` | Summary used on post cards and SEO meta tags |
| `pubDate` | `Date` (coerced) | Publication date (e.g., `YYYY-MM-DD`), used for ordering |
| `author` | `string` | Post author (e.g., `"Nimbus Engineering"`) |
| `tags` | `string[]` | Array of tags (e.g., `["ci", "devops"]`) |

---

## 🎯 Deliverables & Requirements Checklist

- [x] **Home page**: Lists all posts with title, date, description, and clickable tags, sorted newest first.
- [x] **One page per post**: Dynamically generated from markdown files via Astro content collections.
- [x] **Shared layout**: `BaseLayout.astro` providing header, nav, footer, per-page `<title>`, canonical URLs, and OpenGraph meta descriptions.
- [x] **Content Collection Schema**: Defined and validated in `src/content.config.ts` with Zod.
- [x] **About page**: Dedicated `/about` highlighting Nimbus Cloudworks mission, values, and engineering leadership.
- [x] **Clean build**: `npm run build` succeeds with zero errors and zero unhandled warnings.
- [x] **README**: Complete setup guide and under-5-line post creation instructions.
- [x] **Bonus - Tag pages**: `/tags` index and dynamic `/tags/[tag]` archives.
- [x] **Bonus - RSS feed**: Automated `/rss.xml` generated via `@astrojs/rss`.
- [x] **Bonus - XML Sitemap**: Automated `/sitemap-index.xml` via `@astrojs/sitemap`.

---

## 🚀 Deployment

The site is built as a static site and can be deployed with one click:

- **Vercel / Netlify**: Connect the Git repository; set Build command to `npm run build` and Output directory to `dist`.
- **Cloudflare Pages / GitHub Pages**: Deploy the generated `dist/` directory.
