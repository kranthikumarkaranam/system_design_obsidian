# Performance Optimization

#concept #to-revise Back to: [[FE SD - MOC]] Used in: [[03 - RADIO Framework]] → O step, [[Case Study - Autocomplete]]

---

## Core Web Vitals (memorize these)

|Metric|What it measures|Good threshold|
|---|---|---|
|**LCP** — Largest Contentful Paint|Loading speed — when is the main content visible?|< 2.5s|
|**INP** — Interaction to Next Paint|Responsiveness — how fast does the page respond to input?|< 200ms|
|**CLS** — Cumulative Layout Shift|Visual stability — does content jump around?|< 0.1|

> INP replaced FID (First Input Delay) as the responsiveness metric in March 2024.

---

## Loading performance techniques

### Code splitting

Load only the JS needed for the current page/view.

```javascript
// React lazy loading
const HeavyChart = React.lazy(() => import('./HeavyChart'))
```

### Lazy loading

- Images: `<img loading="lazy" />` or IntersectionObserver
- Components: load on scroll-into-view or on interaction

### Prefetching / preloading

- `<link rel="preload">` — load resources early that are needed for current page
- `<link rel="prefetch">` — load resources for the _next_ page in background

### Tree shaking

Remove unused code at build time. Requires ES modules.

### Image optimization

- Use modern formats: **WebP**, AVIF
- Serve responsive images: `srcset` + `sizes`
- Compress images at upload time
- Use a CDN for images (Cloudinary, imgix, AWS CloudFront)

---

## Runtime performance techniques

### List virtualization

Only render items in the viewport. For long lists of 1000+ items. Libraries: `react-virtual`, `react-window`, `TanStack Virtual`

### Memoization

```javascript
// Avoid re-renders
const MemoComponent = React.memo(Component)
const memoizedValue = useMemo(() => expensiveCalc(), [deps])
const memoizedCallback = useCallback(() => handler(), [deps])
```

### Debounce & throttle

- **Debounce**: Wait until user stops typing before firing (search input)
- **Throttle**: Fire at most once per time interval (scroll handler, resize)

---

## Network performance

- **HTTP caching** — see [[Caching Strategies]]
- **Pagination** — don't load all data at once
    - Offset: simple but slow at large offsets
    - Cursor: better for feeds and large datasets
- **Compression** — gzip / Brotli for text assets
- **CDN** — serve static assets from edge nodes close to users

---

## Rendering performance

See [[Rendering Strategies]] for SSR, SSG, CSR tradeoffs.

Key for interviews:

- SSR → faster first paint, good for SEO
- SSG → fastest, for static content
- CSR → good for authenticated dashboards (no SEO need)

---

## Used in these case studies

- [[Case Study - News Feed (e.g. Facebook)]] — list virtualization, image lazy load, pagination
- [[Case Study - Amazon E-commerce Performance]] — Core Web Vitals, image optimization, SSG
- [[Case Study - Airbnb SEO]] — SSR, preloading, structured data
- [[Case Study - Netflix Media Player]] — streaming, video optimization
- [[Case Study - Instagram Media Upload]] — chunked uploads, compression