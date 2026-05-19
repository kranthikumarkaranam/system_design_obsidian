#concept #to-revise 
Back to: [[FE SD - MOC]] 
Used in: [[03 - RADIO Framework]] → I step, [[Case Study - Autocomplete]]

---

## Server ↔ Client protocols

|Protocol|Directionality|When to use|
|---|---|---|
|**HTTP / REST**|Client → Server (request-response)|Default for CRUD ops|
|**GraphQL**|Client → Server|Flexible queries, avoid over-fetching|
|**WebSockets**|Bidirectional|Chat, collaborative editing, live data|
|**Server-Sent Events (SSE)**|Server → Client only|Notifications, live feeds, one-way updates|
|**Long polling**|Client polls server repeatedly|Fallback when WebSockets unavailable|

---

## REST API design patterns

- Use nouns, not verbs: `/posts` not `/getPosts`
- Pagination: cursor-based preferred over offset for feeds
    
    ```
    GET /feed?cursor=abc123&limit=20→ { data: [...], nextCursor: "xyz" }
    ```
    
- HTTP status codes: 200 OK, 201 Created, 400 Bad Request, 401 Unauthorized, 404 Not Found, 429 Rate Limited

---

## WebSockets vs SSE

||WebSockets|Server-Sent Events|
|---|---|---|
|Direction|Bidirectional|Server → Client only|
|Protocol|ws://|HTTP|
|Reconnect|Manual|Automatic|
|Use case|Chat, collaborative editing|Notifications, live score|
|Complexity|Higher|Lower|

---

## Optimistic updates

Update the UI **before** the server confirms — then rollback if it fails.

```javascript
// 1. Optimistically update local state
dispatch({ type: 'LIKE_POST', postId })

// 2. Call API
try {
  await api.likePost(postId)
} catch (err) {
  // 3. Rollback on failure
  dispatch({ type: 'UNLIKE_POST', postId })
  showError()
}
```

Good for: likes, follows, form submissions, reordering

---

## Error handling patterns

- Retry with exponential backoff for transient errors
- Show meaningful error states (not just "Something went wrong")
- Distinguish: network error vs server error vs client error

---

## Used in these case studies

- [[Case Study - News Feed (e.g. Facebook)]] — cursor pagination, optimistic likes
- [[Case Study - Messenger Real-time Chat]] — WebSockets
- [[Case Study - Google Docs]] — WebSockets + conflict resolution
- [[Case Study - Netflix Media Player]] — streaming protocols