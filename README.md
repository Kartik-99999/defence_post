# DefencePost.live

Independent Indian defence journalism platform covering military operations, strategic
policy, defence technology, naval affairs, intelligence, and geopolitics — analysed from
India's strategic perspective and updated daily.

🌐 **Live site:** [www.defencepost.live](https://www.defencepost.live)

## Overview

This repository holds the static front end for DefencePost.live. Articles are rendered
client-side into the templates below, and the whole site is deployed on Vercel.

## Coverage

- **Military** — Indian Armed Forces, DRDO, indigenous weapons systems
- **Geopolitics** — India–Pakistan and India–China dynamics, Indo-Pacific strategy
- **Naval** — fleet, shipbuilding, and maritime security
- **Cyber & Tech** — defence technology and cyber affairs
- **Intelligence** & **Policy** — strategic analysis and defence policy

## Project structure

```text
public/
├── index.html            Home / article renderer
├── about.html            About the platform
├── contact.html          Contact page
├── disclaimer.html       Editorial disclaimer
├── privacy-policy.html   Privacy policy
├── admin/                Admin interface
├── sitemap.xml           Full article index
├── robots.txt            Crawler directives
├── llms.txt              Machine-readable site summary for LLMs
├── ads.txt               Authorized ad sellers
└── vercel.json           Vercel deployment / routing config
```

## Tech stack

- Static HTML/CSS/JS
- [`@vercel/analytics`](https://vercel.com/analytics) and
  [`@vercel/speed-insights`](https://vercel.com/docs/speed-insights) for telemetry
- Hosted on [Vercel](https://vercel.com)

## Local development

The site is fully static — serve the `public/` directory with any static file server:

```bash
cd public
npx serve .        # or: python3 -m http.server 3000
```

To install the analytics dependencies:

```bash
cd public
npm install
```

## Deployment

Deployment is handled by Vercel using `public/vercel.json`. Pushing to `main`
triggers a production deploy.

## License

ISC (see `public/package.json`).
