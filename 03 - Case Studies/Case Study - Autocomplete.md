#source/greatfrontend #case-study #ui-component 

Source: [Autocomplete](https://www.greatfrontend.com/questions/system-design/autocomplete)
Back to: [[FE SD - MOC]]


---

## At a Glance

| RADIO Step    | Core decision                                                             |
| ------------- | ------------------------------------------------------------------------- |
| Requirements  | Generic + customizable; all devices; text/image/media results             |
| Architecture  | MVC: Input UI → Controller ↔ Cache ↔ Server; Results UI                   |
| Data model    | Normalize cache: `CacheEntry` (query → resultIds[]) + `Result` store      |
| Interface     | `apiUrl`, `renderItem`, `debounceMs`, `minQueryLength` as component props |
| Optimizations | Key responses by query string; debounce 300ms; WAI-ARIA combobox          |

> 💡 The entire design pivots on three choices: (1) centralize through a controller, (2) normalize the cache, (3) use the WAI-ARIA combobox pattern. Everything else flows from these.

---

## Requirements (R)

### Functional

- User types into a text field and a popup of suggestions appears.
- User can select a suggestion from the popup.
- Back end API is provided: returns a list of results given a search query.
- Component should be generic — usable by any website.
- Input field UI and results popup UI must be customizable.

### Non-functional

- All devices: laptop, tablet, mobile.
- Support result types: text, image (text + image), media.
- Accessible via keyboard and screen reader (WAI-ARIA combobox).
- Fast: cached results appear instantly; new queries debounced 300ms.

### Out of scope (initial version)

- Fuzzy search (Levenshtein distance — mention, defer).
- Server-side ranking or personalization logic.
- Offline-first persistence (localStorage/IndexedDB).

### Clarifying questions to ask

|Question|Answer|
|---|---|
|What result types?|Text, image, media — but must be extensible via render function|
|What devices?|All — laptop, tablet, mobile|
|Fuzzy search?|Not initial version; can add client-side Levenshtein later|
|Long-lived SPA or short page?|Determines cache shape (hash map vs normalized map)|
|Initial results on focus?|Yes — show trending/historical on empty query|

---

## Architecture (A)

```
┌──────────────────────────── Autocomplete Component ──────────────────────────────┐
│                                                                                    │
│   View / UI Layer                                                                  │
│   ┌───────────────────────┐          ┌───────────────────────┐                    │
│   │     Results UI        │          │      Input UI         │                    │
│   │  (Popup / Dropdown)   │          │   (Text field)        │                    │
│   │                       │          │                       │                    │
│   │  - Renders suggestions│          │  - Captures keystrokes│                    │
│   │  - Highlights active  │◄─Results─│  - Sends query up     │                    │
│   │  - Fires onSelect     │          │  - Query ────────────►│                    │
│   └───────────┬───────────┘          └───────────┬───────────┘                    │
│               │ Selection                         │ Query                          │
│               └──────────────┐  ┌────────────────┘                                │
│                              ▼  ▼                                                  │
│                    ┌─────────────────────┐                                         │
│                    │     Controller      │  ← "Brain" of the component (MVC)       │
│                    │                     │                                         │
│                    │  - Owns: input,     │                                         │
│                    │    activeIndex,     │                                         │
│                    │    isOpen,          │                                         │
│                    │    isLoading        │                                         │
│                    └────────┬────────────┘                                         │
│                             │  Query / Results                                     │
│                    ┌────────▼────────────┐                                         │
│                    │       Cache         │  ← Check before hitting server          │
│                    │  (in-memory store)  │                                         │
│                    └────────┬────────────┘                                         │
│                             │ Cache miss only                                      │
└─────────────────────────────┼────────────────────────────────────────────────────-┘
                              │ Query ↓   Results ↑
                    ┌─────────▼────────────┐
                    │       Server         │
                    │  GET /api/search     │
                    └──────────────────────┘
```

**Component responsibilities:**

|Component|Owns|Does|
|---|---|---|
|Input UI|—|Captures keystrokes, passes query to controller|
|Results UI|—|Renders suggestions from controller, fires `onSelect`|
|Controller|`input`, `activeIndex`, `isOpen`, `isLoading`|Routes all data flow; checks cache; fetches on miss|
|Cache|`entries` (query → resultIds), `results` (id → Result)|Instant recall for repeated queries; race-condition guard|

---

## Data Model (D)

### TypeScript types

```typescript
// ─── Result entity (server + cache store) ────────────────────────────────────
type ResultType = 'text' | 'image' | 'media' | 'organization' | 'person'

type Result = {
  id: string
  type: ResultType
  text: string
  subtitle?: string    // secondary label (e.g. "City in California")
  imageUrl?: string    // for image / media results
}

// ─── Normalized cache ─────────────────────────────────────────────────────────
// Each query entry holds IDs only; actual Result objects live in one shared map.
// This prevents duplicate Result objects across "fa", "fac", "face" cache entries.

type CacheEntry = {
  query: string
  resultIds: string[]   // ordered list of result IDs for this query
  fetchedAt: number     // Unix ms — used for TTL eviction
}

type AutocompleteCache = {
  entries: Record<string, CacheEntry>   // keyed by query string
  results: Record<string, Result>       // keyed by result ID — shared store
}

// ─── Controller state ─────────────────────────────────────────────────────────
type ControllerState = {
  input: string          // current text in the input field
  activeIndex: number    // index of highlighted suggestion (-1 = none)
  isOpen: boolean        // is the popup visible?
  isLoading: boolean     // is a network request in-flight?
}
```

### Cache structure — three options and when to use each

|Option|Structure|Lookup|Duplication|Best for|
|---|---|---|---|---|
|1. Hash map|`query → Result[]`|O(1)|High (same Result in "fa", "fac", "face")|Short-lived pages (Google search)|
|2. Flat list|Single `Result[]`, filter client-side|O(n) filter|None|Small datasets only|
|3. Normalized map|`query → resultIds[]` + `id → Result`|O(1)|None|Long-lived SPAs (Facebook)|

> 💡 Pick cache shape based on page lifetime. Hash map is fine for Google (page resets on navigation). Normalized map is better for Facebook — users spend hours on the page, and the same entity (e.g. a friend) appears across many queries; storing it once prevents unbounded memory growth.

### Controller vs Cache data ownership

```
Controller owns transient UI state          Cache owns persistent query history
────────────────────────────────           ──────────────────────────────────
input          → current query string      entries  → CacheEntry per query
activeIndex    → highlighted row           results  → shared Result pool
isOpen         → popup shown/hidden
isLoading      → request in-flight
```

---

## Interface Definition / API (I)

### Server API

```http
GET /api/search?query={q}&limit={n}&pagination={page}
→ 200 { results: Result[] }
```

Parameters:

|Param|Purpose|
|---|---|
|`query`|The search string typed by the user|
|`limit`|Max results per page (used when scrolling for more)|
|`pagination`|Page number — needed only when users can scroll beyond first page|

### Client Component API — Basic props

```typescript
type AutocompleteProps = {
  apiUrl: string                           // endpoint to hit per query
  numberOfResults?: number                 // max suggestions to show (default: 10)
  onSelect?: (result: Result) => void      // callback when user picks a suggestion
  onInput?: (value: string) => void        // fires on every keystroke
  onFocus?: () => void
  onBlur?: () => void
  onChange?: (value: string) => void
}
```

### Client Component API — Advanced props

```typescript
type AutocompleteProps = {
  // ...basic props above

  // ─── Performance ───────────────────────────────────────────────────────────
  minQueryLength?: number      // min chars before firing (default: 3)
  debounceMs?: number          // debounce window in ms (default: 300)
  timeoutMs?: number           // abort display after N ms with error state

  // ─── Customised rendering (three approaches, pick one) ─────────────────────
  // 1. Theming object — easiest, least flexible
  themeOptions?: Record<string, string>           // e.g. { textSize: '12px' }
  // 2. Class names — developer applies their own CSS
  classNames?: Record<string, string>             // e.g. { container: 'my-wrap' }
  // 3. Render function — full inversion of control, most flexible
  renderItem?: (result: Result) => React.ReactNode

  // ─── Cache ─────────────────────────────────────────────────────────────────
  initialResults?: Result[]                       // shown on focus (empty query)
  resultsSource?: 'network' | 'network-and-cache' | 'cache-only'
  mergeFn?: (server: Result[], cached: Result[]) => Result[]
  cacheDurationMs?: number                        // TTL per cache entry
}
```

> 💡 `renderItem` (render function / inversion of control) is the most flexible rendering approach. The component just calls `renderItem(result)` and the developer controls everything. Use this as the answer when asked "how would you make this customisable?"

---

## Optimizations and Deep Dive (O)

### Network

#### Handling race conditions (concurrent requests)

Autocomplete fires a request on nearly every keystroke. Responses can arrive out of order.

```
User types "fa"  → GET /search?q=fa  ─────────────────────►  Response "fa" arrives SECOND
User types "fac" → GET /search?q=fac ──────────────────────►  Response "fac" arrives FIRST
                                                              ↑ renders "fac" → CORRECT ✓
                                          Response "fa" arrives late
                                                              ↑ current input is "fac"
                                                              → query ≠ input → SKIP ✓
```

Fix: **key responses by the query string that issued them.**

```
if (response.query !== controller.currentInput) return  // stale — discard
cache.set(response.query, response.results)             // still populate cache!
```

> 💡 Do NOT use `AbortController` to cancel in-flight requests. The server has already done the work. The response can still populate the cache — if the user backtracks, the cache serves it instantly. Just ignore the response for rendering purposes.

**Two strategies to detect stale responses:**

|Strategy|How|Downside|
|---|---|---|
|Timestamp tracking|Tag each request with a sequence number; only render if latest|Extra state to manage|
|Query-keyed cache|Store response under query string; only render if cache key matches input|**Preferred** — also gives you the cache for free|

#### Failed requests and retries

- On failure: retry automatically. If server is offline, use **exponential backoff** to avoid overloading it.
- Show error state with a retry button in the popup.

#### Offline usage

When device has no network connection:

- Read from cache — serve whatever was already fetched.
- Do not fire new network requests (save CPU/battery).
- Show a "no network" indicator in the component.

---

### Cache (in-memory, client-side)

#### Purpose

Saves results of previous queries in memory. On repeated query → instant result, zero network latency.

#### Cache strategy config options

|`resultsSource` value|Behaviour|
|---|---|
|`network-only`|Always fetch; never read from cache|
|`network-and-cache`|Show cached results immediately, then overlay fresh network results|
|`cache-only`|Only read cache; useful for offline mode or pre-loaded datasets|

#### Initial results (empty string key)

Pre-populate the cache with `""` → trending/historical results. These show immediately on input focus, before the user types anything. Examples:

- Google: popular searches, trending topics
- Facebook: recent searches, friend suggestions
- Stock exchanges: historical queries, trending tickers

#### Cache eviction

|Application|Cache lifetime reasoning|
|---|---|
|Google search|Long TTL (hours) — search results don't change often|
|Facebook|Medium TTL (30 min) — social content updates moderately|
|Stock/crypto|No caching or very short TTL (seconds) — prices change every minute|

---

### Performance

#### Keystroke-to-render pipeline

```
  Keystroke
      │
      ▼
  Query length < minQueryLength?  ──YES──► Skip — do nothing
      │ NO
      ▼
  Debounce 300ms (wait for pause)
      │
      ▼
  Cache hit?  ──YES──────────────────────► Write to display → Render immediately
      │ NO (cache miss)
      ▼
  Fetch from server
      │
      ▼
  response.query === currentInput?  ──NO──► Discard (stale response)
      │ YES                                 ↑ Still write to cache!
      ▼
  Write to cache → Render results
```

#### Debouncing vs throttling

|Technique|How|Use for|
|---|---|---|
|Debounce|Fire only after N ms of silence|Typing → autocomplete queries ✓|
|Throttle|Fire at most once per N ms|Scroll, resize|

> 💡 Default to **300ms debounce** for typing. Fast typists collapse many keystrokes into one request. Throttle is wrong here — it would fire mid-word and waste server calls.

#### Memory management

Long-lived SPAs accumulate results in the cache. To prevent memory leaks:

- Purge cache when `requestIdleCallback` fires (browser idle).
- Purge when total entries exceed a configured threshold (e.g. 200 entries).

#### Virtualized lists

If results contain hundreds of items, rendering all DOM nodes is expensive. Use **list virtualisation** (react-window / react-virtual): render only visible nodes, recycle DOM nodes as the user scrolls.

---

### User Experience

|Concern|Solution|
|---|---|
|Autofocus|Add `autofocus` on `<input>` if high-intent page (e.g. Google home)|
|Loading state|Show spinner inside input or above popup|
|Error state|Show error message with retry button|
|No network|Show "no network" message, read cache only|
|Long result text|Truncate with ellipsis, no overflow outside popup|
|Mobile tap targets|Each result item large enough to tap; dynamic count by viewport|
|Mobile input|`autocapitalize="off"` `autocomplete="off"` `autocorrect="off"` `spellcheck="false"`|
|Keyboard shortcut|`/` (forward slash) to focus search — used by Facebook, X, YouTube|
|Popup positioning|Render below by default; flip above if input is near bottom of viewport|
|Typos|Client-side fuzzy match via Levenshtein distance (if in scope)|

---

### Accessibility

> 💡 Follow the **WAI-ARIA combobox pattern** exactly. Do not invent custom ARIA. Ad hoc roles result in inconsistent announcements and leave keyboard-only users unable to reach the popup.

#### ARIA roles and attributes

|Attribute|Element|Purpose|
|---|---|---|
|`role="combobox"`|`<input>`|Declares this as a combobox widget|
|`aria-haspopup="listbox"`|`<input>`|Signals a popup will appear|
|`aria-expanded`|`<input>`|`true` when popup visible, `false` when closed|
|`aria-label`|`<input>`|Provides accessible name (no visible label typically)|
|`aria-activedescendant`|`<input>`|ID of currently highlighted option|
|`aria-autocomplete`|`<input>`|`"list"` (FB, X) or `"both"` (Google)|
|`role="listbox"`|Results container|The popup list|
|`role="option"`|Each `<li>`|Each suggestion item|
|`aria-live`|Results region|Notifies screen reader when new results arrive|

**Google vs Facebook vs X comparison:**

|HTML Attribute|Google|Facebook|X|
|---|---|---|---|
|HTML element|`<textarea>`|`<input>`|`<input>`|
|Within `<form>`|Yes|No|Yes|
|`type`|`"text"`|`"search"`|`"text"`|
|`role`|`"combobox"`|Absent|`"combobox"`|
|`aria-autocomplete`|`"both"`|`"list"`|`"list"`|
|`aria-activedescendant`|Present|Absent|Present|
|`aria-haspopup`|`"false"`|Absent|Absent|
|`spellcheck`|`"false"`|`"false"`|`"false"`|
|`autofocus`|Present|Absent|Present|
|`autocomplete`|`"off"`|`"off"`|`"off"`|

> 💡 There is no single standardised practice across companies. Google, Facebook and X all differ. What matters is that your component is internally consistent and follows the WAI-ARIA spec.

#### Keyboard interactions

|Key|Action|
|---|---|
|Any character|Open popup, update query|
|`↓` / `↑`|Navigate suggestions; wrap at top/bottom|
|`Enter`|Select highlighted suggestion (or submit form)|
|`Escape`|Close popup|
|`Tab`|Close popup, move focus|
|`/`|(Global shortcut) Focus the search input|

#### Combobox lifecycle (state machine)

```
              ┌──────────────────┐
              │     Closed       │◄──── Escape / blur / selection
              └────────┬─────────┘
                       │ Focus / type / initial result
                       ▼
              ┌──────────────────┐
          ┌──►│      Open        │
          │   └──┬───────────────┘
          │      │ Typing
          │      ▼
          │   ┌──────────────────┐      Network error
          │   │    Loading       │──────────────────────►┌─────────────┐
          │   └──┬───────────────┘                       │  Error      │
          │      │ Response matches input                 └──────┬──────┘
          │      ▼                                               │ Retry
          │   ┌──────────────────┐                               │
          │   │  Results shown   │◄──────────────────────────────┘
          │   └──┬───────────────┘
          │      │ ↓ / ↑ arrows
          │      ▼
          │   ┌──────────────────┐
          │   │   Navigating     │
          │   └──┬───────────────┘
          │      │ Enter / click
          │      ▼
          └───┌──────────────────┐
              │    Selected      │──► onSelect(result) fired → popup closed
              └──────────────────┘
```

---

## Summary — The Three Key Decisions

|Decision|What|Why|
|---|---|---|
|Centralize through Controller|Single component owns `input`, `activeIndex`, `isOpen`|Race conditions and stale state have one place to be resolved, not spread across components|
|Normalize the cache|`CacheEntry` (query → resultIds[]) + shared `Result` store|Kills duplication on long-lived pages; query-keyed lookup doubles as the race-condition guard|
|Use platform primitives|300ms debounce + WAI-ARIA combobox pattern|Debounce collapses keystrokes into one request; WAI-ARIA gives keyboard + screen reader support for free|

---

## Concepts Used in This Case Study

- [[Component Architecture]] — MVC controller pattern; single controller as source of truth; inversion of control via `renderItem`
- [[State Management]] — controller owns transient UI state; cache owns persistent query history; separation is intentional
- [[Caching Strategies]] — client-side in-memory cache; normalized map structure; TTL eviction; `cache-only` / `network-and-cache` strategy options
- [[Performance Optimization]] — debouncing (300ms); list virtualisation for large result sets; memory purging on idle; cache-first serving
- [[Networking & APIs]] — race condition guard via query-keyed responses; retry with exponential backoff; offline detection; why NOT to use `AbortController`
- [[Accessibility (A11y)]] — WAI-ARIA combobox pattern; `role="combobox"`, `aria-expanded`, `aria-activedescendant`; full keyboard interaction model