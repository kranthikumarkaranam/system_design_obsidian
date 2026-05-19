# State Management

#concept #to-revise Back to: [[FE SD - MOC]] Used in: [[03 - RADIO Framework]] → D step, [[Case Study - Autocomplete]]

---

## Two types of state in FE

|Type|Definition|Examples|Where it lives|
|---|---|---|---|
|**Server state**|Comes from the API, source of truth is the server|Posts, user profile, products|React Query / SWR / Redux|
|**Client / UI state**|Lives only in the browser, no server equivalent|Modal open, current tab, loading spinner|useState / Zustand / Redux|

> 💡 A common interview mistake is treating everything as server state (requires a fetch) or everything as client state (requires manual sync). Be explicit about which is which.

---

## State categories (more granular)

|Category|Examples|Solution|
|---|---|---|
|**URL state**|Current page, filters, search query|URL params (`?page=2&filter=recent`)|
|**Global UI state**|Theme, language, auth status|Context API, Zustand|
|**Server cache**|List of posts, user data|React Query, SWR|
|**Local component state**|Dropdown open, form input|`useState`|
|**Form state**|Field values, validation errors|React Hook Form, Formik|

---

## State shape design

Always define the shape of your state in the interview:

```typescript
// Feed state example
type FeedState = {
  // server data
  posts: Post[]
  cursor: string | null
  hasMore: boolean
  
  // UI state
  isLoading: boolean
  isLoadingMore: boolean
  error: string | null
  
  // optimistic state
  pendingLikes: Set<string>  // postIds being liked
}
```

---

## Key questions to ask about state in interviews

1. Does this data need to persist across page refreshes? → LocalStorage / URL
2. Does multiple components need this data? → Global store / Context
3. Does the data come from the server? → Server state management library
4. Is this just for one component? → Local `useState`

---

## Used in these case studies

- [[Case Study - News Feed (e.g. Facebook)]] — feed posts (server state) + like status (optimistic)
- [[Case Study - Google Docs]] — document state with real-time sync
- [[Case Study - Messenger Real-time Chat]] — message list + connection status