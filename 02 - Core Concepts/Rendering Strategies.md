# Rendering Strategies

#concept #to-revise Back to: [[FE SD - MOC]] Used in: [[03 - RADIO Framework]] → A step and O step

---

## The four strategies

|Strategy|What happens|Pros|Cons|Best for|
|---|---|---|---|---|
|**CSR** — Client-side rendering|Browser downloads JS and renders everything|Rich interactivity, fast after load|Bad SEO, slow first paint|Dashboards, authenticated apps|
|**SSR** — Server-side rendering|Server renders HTML per request|Good SEO, fast first paint|Server load, slower TTFB under load|E-commerce, news, anything needing SEO|
|**SSG** — Static site generation|HTML built at build time|Fastest, CDN-cacheable|Stale data, slow builds for huge sites|Blogs, marketing, docs|
|**ISR** — Incremental Static Regeneration|SSG but pages regenerate after a timeout|SSG speed + fresh data|More complex|E-commerce product pages|

---

## When to choose which — interview decision tree

```
Does the page need SEO?
├── NO  → CSR (dashboard, app behind login)
└── YES → Does the content change frequently?
          ├── YES, per-user → SSR
          ├── YES, but shared → ISR
          └── NO → SSG
```

---

## Hydration

After SSR/SSG sends HTML, the browser loads JS and "hydrates" — attaching event listeners to the static HTML. Before hydration, the page looks correct but is non-interactive.

**Problem:** hydration mismatch → server HTML ≠ client render → React error **Solutions:** avoid Date.now(), Math.random() during render; use `suppressHydrationWarning`

---

## Used in these case studies

- [[Case Study - Airbnb SEO]] — SSR for search pages
- [[Case Study - Amazon E-commerce Performance]] — ISR/SSG for product pages
- [[Case Study - News Feed (e.g. Facebook)]] — CSR with skeleton screens