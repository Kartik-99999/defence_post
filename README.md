# DefencePost.live

Independent Indian defence journalism platform covering military operations, strategic
policy, defence technology, naval affairs, intelligence, and geopolitics — analysed from
India's strategic perspective and updated daily.

🌐 **Live:** [www.defencepost.live](https://www.defencepost.live)

---

## Overview

This repository is the **static front end** for DefencePost.live. It's a lightweight,
dependency-free site (vanilla HTML/CSS/JS) served from the `public/` directory and
deployed on **Vercel**. Content is loaded at runtime from a separate backend API — the
front end fetches articles, stats, comments, and newsletter data on the client and
renders them into a single `index.html` shell.

> **Backend:** the content API is hosted separately at
> `https://defencepost-api.azurewebsites.net/api` (Azure) and is **not** part of this
> repository. This repo is the presentation layer only.

### How rendering works

- `index.html` is a client-rendered shell. On load, JavaScript calls the API for a
  paginated article feed (`/articles?page=&limit=10`), category filters, search, and
  homepage stats (`/articles/stats`).
- **Clean URLs** like `/article/:slug` and `/category/:slug` are rewritten to
  `index.html` by [`vercel.json`](./public/vercel.json); the client reads the path and
  fetches the matching article (`/articles/:slug`) or category feed.
- Each article view also loads and posts **comments**
  (`/newsletter/comments/:id`, `/newsletter/comment`) and supports **newsletter signup**
  (`/newsletter/subscribe`).
- An **admin panel** (`admin/index.html`) authors and publishes content against the same
  API and uploads cover images to **Cloudinary**. It is disallowed to crawlers via
  `robots.txt`.

---

## Project structure

```text
public/
├── index.html            Home + client-side article/category renderer (SPA-style)
├── about.html            About the platform
├── contact.html          Contact page
├── disclaimer.html       Editorial disclaimer
├── privacy-policy.html   Privacy policy
├── admin/index.html      Content authoring / publishing panel (crawler-disallowed)
├── favicon.png
├── sitemap.xml           Full article index for search engines
├── robots.txt            Crawler rules — AI answer-engines explicitly allowed
├── llms.txt              Machine-readable site summary for LLMs
├── ads.txt               Authorized digital ad sellers
├── vercel.json           SPA rewrites for /article/* and /category/*
├── package.json          Vercel Analytics + Speed Insights deps
└── package-lock.json
```

---

## SEO & discoverability

This site leans heavily into being cited by both search engines and AI answer engines:

- **`sitemap.xml`** exposes the full published-article index.
- **`robots.txt`** explicitly **allows AI/LLM crawlers** (GPTBot, OAI-SearchBot,
  ChatGPT-User, PerplexityBot, ClaudeBot, Google-Extended, CCBot, Bingbot, …) so
  DefencePost content can be retrieved and cited in ChatGPT, Gemini, Claude, and
  Perplexity — while `/admin/` is disallowed everywhere.
- **`llms.txt`** provides a concise, machine-readable summary of the site, its sections,
  and contact points for LLM consumption.

### Coverage sections

Military · Geopolitics · Naval · Cyber & Tech · Intelligence · Policy

---

## Local development

The site is fully static — serve the `public/` directory with any static file server:

```bash
cd public
npx serve .            # or: python3 -m http.server 3000
```

Note that article content requires the live API to be reachable; with the API up, the
homepage feed, article pages, search, comments, and newsletter signup all work against
`https://defencepost-api.azurewebsites.net/api`.

To install the analytics dependencies used in production:

```bash
cd public
npm install
```

---

## Deployment

Deployment is handled by **Vercel** using [`public/vercel.json`](./public/vercel.json),
which rewrites article and category routes to the SPA shell. Pushing to `main` triggers a
production deploy. Telemetry is provided by
[`@vercel/analytics`](https://vercel.com/analytics) and
[`@vercel/speed-insights`](https://vercel.com/docs/speed-insights).

---

## Tech stack

- **Front end:** vanilla HTML / CSS / JavaScript (no framework), Google Fonts
- **Media:** Cloudinary (admin image uploads)
- **Hosting:** Vercel (static + SPA rewrites)
- **Telemetry:** Vercel Analytics & Speed Insights
- **Content API:** external Azure-hosted service (separate repository)

## License

ISC (see [`public/package.json`](./public/package.json)).
