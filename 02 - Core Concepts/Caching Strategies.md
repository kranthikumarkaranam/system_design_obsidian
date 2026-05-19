# Caching Strategies

#concept #to-revise Back to: [[FE SD - MOC]] Used in: [[03 - RADIO Framework]] → O step,  [[Case Study - Autocomplete]]

---

## Layers of caching in FE

| Layer                        | What it caches                     | Tool                    |
| ---------------------------- | ---------------------------------- | ----------------------- |
| **CDN**                      | Static assets (JS, CSS, images)    | CloudFront, Cloudflare  |
| **HTTP cache**               | API responses, HTML pages          | `Cache-Control` headers |
| **Service Worker**           | Assets + API responses for offline | Workbox, custom SW      |
| **In-memory cache**          | Repeated API calls in same session | React Query, SWR        |
| **localStorage / IndexedDB** | Persisted client data              | Browser storage APIs    |

---

## HTTP Cache-Control headers

```http
Cache-Control: max-age=3600          # cache for 1 hour
Cache-Control: no-store              # never cache (sensitive data)
Cache-Control: no-cache              # cache but always revalidate
Cache-Control: stale-while-revalidate=60   # serve stale, refresh in background
```

> 💡 For static assets (JS/CSS with content hashes in filename), use `max-age=31536000, immutable`. For HTML, use `no-cache` so users always get fresh navigation.

---

## Service Worker caching patterns

|Pattern|Strategy|Use case|
|---|---|---|
|**Cache first**|Serve from cache, fall back to network|Static assets, app shell|
|**Network first**|Try network, fall back to cache|API responses where freshness matters|
|**Stale-while-revalidate**|Serve cache immediately, update in background|Feeds, content that can be slightly stale|

---

## React Query / SWR patterns

```javascript
// React Query — server state cache
const { data, isLoading } = useQuery({
  queryKey: ['feed', cursor],
  queryFn: () => fetchFeed(cursor),
  staleTime: 60_000,        // data is fresh for 1 min
  gcTime: 5 * 60_000,       // keep in cache for 5 min
})
```

---

## Used in these case studies

- [[Case Study - Amazon E-commerce Performance]] — CDN + SSG + HTTP cache
- [[Case Study - Airbnb SEO]] — cache search results
- [[Case Study - News Feed (e.g. Facebook)]] — React Query, stale-while-revalidate