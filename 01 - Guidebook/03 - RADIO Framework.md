#source/greatfrontend #guide 

Source: [The RADIO Framework](https://www.greatfrontend.com/front-end-system-design-playbook/framework)
Back to: [[FE SD - MOC]]

---

## What is RADIO?

A framework to approach front end system design interviews in a structured way. "A good structure is half the battle won."

```
R — Requirements exploration
A — Architecture / High-level design
D — Data model
I — Interface definition (API design)
O — Optimizations and deep dive
```

> 💡 RADIO works for back end system design too — not just FE. But for BE you may need to cover additional areas beyond RADIO.

---

## Critical: RADIO is NOT a rigid linear sequence

> Do not follow R → A → D → I → O mechanically. RADIO is a **checklist**, not a script.

- The order can shift based on the product and conversation
- Some candidates prefer designing the data model (D) before architecture (A) — that's fine
- Interface (I) naturally follows A and D, but not always
- Interviewers may interrupt and ask for a deep dive mid-way — **follow their lead**, then resume
- **Backtrack freely:** if a new feature discovered in A breaks your D, go back and fix D immediately
- Write "RADIO" on the whiteboard to track what's left to cover — interviews are nerve-wracking

> 💡 **Do not force RADIO** onto every question. Some narrow, specific questions (e.g. "implement a mention feature in Slack") don't need the full framework.

---

## R — Requirements exploration

**Goal:** Understand the problem thoroughly and determine scope via clarifying questions. 
**Time:** ~10% of the session.

Treat the interviewer like a **product manager** on a new project. No two design interviews are the same even for the same question — interviewers have different priorities. Use this phase to find out what they care about.

### Functional vs Non-functional requirements

| Type               | Definition                                                                                            | Examples                                                                    |
| ------------------ | ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **Functional**     | Core requirements — the product cannot function without them. User can complete core flows correctly. | User can post, like, comment, scroll feed                                   |
| **Non-functional** | Improvements that aren't strictly required for the product to be usable.                              | Performance (page load speed), scalability (items before slowdown), good UX |

> 💡 Design must meet **all functional requirements** first. Only then move to non-functional requirements.

### How to define requirements (preferred approach)

**Take the initiative** — list out what you think the requirements are, then get feedback and alignment from the interviewer. Don't just ask "what are the requirements?" — they'll want you to define them.

### Core clarifying questions to ask

**1. What features to focus on?** "Design Facebook" is huge — news feed, profiles, friends, groups, stories. Ask which part to focus on. Jumping into an out-of-scope area (e.g. the befriending flow when they wanted the news feed) wastes your time and signals poor judgment.

**2. Core features vs good-to-have?** Even within a feature, scope it. For new Facebook posts: text only, or also photo uploads, video, polls, location check-ins? Clarify the MVP, then add extras if time allows.

**3. Standard list of things to ask:**

- What are the main use cases / core features to focus on?
- What devices/platforms need to be supported? (desktop/tablet/mobile)
- Who are the main users?
- Will the app be used offline?
- What are the performance requirements (if any)?
- Does it need to support multiple languages / RTL?
- Is there an existing API, or do I design it too?

> 💡 Write down the agreed requirements somewhere visible. Refer back to them throughout the interview to make sure you've covered everything.

---

## A — Architecture / High-level design

**Goal:** Identify the key components of the product and how they relate to each other. 
**Time:** ~20% of the session.

Draw a diagram. Components = rectangles. Arrows = data flowing between them. Label the arrows.

> 💡 Treat the server as a **black box**. Front end SD evaluates how you structure the client and its API boundary. Don't drift into database schemas, load balancers, or microservice topology — that's BE territory.

### The 4 standard client layers

|Layer|Responsibility|Examples|
|---|---|---|
|**Server**|Black box — exposes APIs via HTTP / GraphQL / WebSockets|—|
|**View layer**|What the user sees and interacts with. Handles presentation and **local** interaction state. Cross-cutting data should NOT live here.|React/Vue/Svelte components, pages|
|**Store / Model layer**|The application's data and derived state. Manages **cross-cutting** data shared between multiple views. Favors unidirectional data flow.|Redux Toolkit, Zustand, Jotai, MobX|
|**Data access layer**|Handles fetching, caching, and error management. Abstracts data origin — other layers don't care where data comes from. Offline storage lives here only, not above.|React Query, tRPC, Apollo Client|

> 💡 Not every layer is needed for every product. For small, single-page apps or UI components, data can live entirely in local component state — no store needed.

### Additional architecture considerations

**Separation of concerns:** Each component should encapsulate a specific set of functionality and data. Consider the purpose/functionality of each component, what data it should contain and how it can service the rest of the system (what it can do for the other components).

**Where should computation happen — client or server?** For example, filtering search results or calculating cart totals. Both have trade-offs. Make a decision and justify it.

After drawing the diagram, **verbally describe the responsibility of each box**.

### Example: News Feed architecture
![[News Feed architecture.png]]

| Component         | Responsibility                                                                                  |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| Server            | Exposes HTTP APIs to fetch feed posts and create new posts                                      |
| Store             | Contains data needed across the whole app — primarily server-originated data for the view layer |
| Data access layer | Makes network requests, passes data to the store, caches network data                           |
| Feed UI           | Contains the list of feed posts + the compose UI                                                |
| Feed post         | Presents a single post's data, contains like/react/share/comment buttons                        |
| Post composer     | UI for creating new posts                                                                       |

> 💡 Common diagram tools: **Excalidraw**, **diagrams.net**. Familiarize yourself with at least one before interviews.


---

## D — Data model

**Goal:** Describe the core entities, their data fields, and which component owns them. **Time:** ~10% of the session.

### Two kinds of data on the client

**1. Server-originated data** Comes from the database, meant to be shared across users/devices. Examples: user profile, feed posts, comments.

**2. Client-only data (UI state)** Lives only in the browser. Two subtypes:

|Subtype|Definition|Examples|
|---|---|---|
|**Data to be persisted**|Eventually sent to the server to be saved|Form inputs, profile settings|
|**Ephemeral data**|Acceptable to lose when tab closes|Form validation state, current nav tab, whether a section is expanded|

### How to present your data model

Use a **table format** showing source, entity, owner, and fields. List the data type for each field.

|Source|Entity|Belongs to|Fields|
|---|---|---|---|
|Server|`Post`|Feed post|`id`, `created_time`, `content`, `image`, `author` (User), `reactions`|
|Server|`Feed`|Feed UI|`posts` (Post[]), `pagination` (cursor metadata)|
|Server|`User`|Store|`id`, `name`, `profile_photo_url`|
|User input (client)|`NewPost`|Post composer|`message`, `image`|

> 💡 It's an iterative process — as requirements grow during the interview, you'll need to add fields. In the architecture diagram, list data fields **under the component that owns them**.


---

## I — Interface definition (API design)

**Goal:** Define the interface between all components — how they communicate, what they send, and what they return. 
**Time:** ~20% of the session.

Every API has three things regardless of type:

|Part|Server-client|Client-client|
|---|---|---|
|**Name / Functionality**|HTTP path|JS function name / Event name|
|**Parameters**|HTTP GET query params / POST body|Function / event parameters|
|**Return value**|HTTP response (usually JSON)|Return values (optional)|

### 1. Server ↔ Client communication

| Protocol                                                    | Direction                  | When to use                                                                                |
| ----------------------------------------------------------- | -------------------------- | ------------------------------------------------------------------------------------------ |
| **HTTP / REST**                                             | Request-response           | Default for most CRUD operations. Most common in interviews.                               |
| **WebSockets**                                              | Bidirectional, persistent  | Real-time apps: chat, collaborative editing, live dashboards, games                        |
| **Server-Sent Events (SSE)**                                | Server → Client only       | One-way live updates: notifications, stock tickers, live feeds. Simpler than WS.           |
| **Long polling**<br>*(not a protocol, more of a technique)* | Client polls, server holds | Simulates real-time over HTTP. Rarely used now — prefer WS or SSE.                         |
| **GraphQL**                                                 | Request-response           | Client queries exactly the data it needs. Unlikely you'll _need_ GraphQL in an interview.  |
| **WebRTC**                                                  | Peer-to-peer               | Low-latency media/data transfer (video calls, file sharing). Very specific use cases only. |

> 💡 For most FE SD interviews, you only need HTTP, WebSockets, and SSE.

**Example — News Feed REST API (full shape):**

```
GET /feed
  Params: { size: 10, cursor: "=dXNlcjpXMDdRQ1JQQTQ" }
  
  
  Response: {
    pagination: { size: 10, next_cursor: "=dXNlcjpVMEc5V0ZYTlo" },
    results: [
      {
        id: "123",
        author: { id: "456", name: "John Doe" },
        content: "Hello world",
        image: "https://example.com/img.jpg",
        reactions: { likes: 20, haha: 15 },
        created_time: 1620639583
      }
    ]
  }
```

### 2. Client ↔ Client (inter-component) communication

|Pattern|How it works|When to use|
|---|---|---|
|**Props + callbacks**|Data down via props, events up via callback functions|Foundational, for parent-child relationships|
|**Store dispatch**|Components dispatch actions to a central store; others subscribe to state changes. Actions have a name + payload.|Cross-cutting state, large apps, unidirectional data flow (Redux, Zustand, Pinia)|
|**Publish/subscribe (event listeners)**|Modules subscribe to events via `element.addEventListener`. Publisher has no knowledge of subscribers.|Decoupled, non-hierarchical communication. Most prevalent in the browser.|

> 💡 In modern web apps with a central store, the most common inter-client communication is **store actions + payload** and how they mutate the data model.

### 3. UI Component API (props)

For UI component design questions, "Interface" = **component props**. Categorize them:

|Prop category|Purpose|Examples|
|---|---|---|
|**Data props**|Data the component renders|`name`, `title`, `items`|
|**Event / Callback props**|Child notifies parent of an event|`onClick`, `onSubmit`, `onChange`|
|**Configuration / Behavior props**|Customize behavior without changing data|`isOpen`, `isDisabled`, `timeout`, `maxResults`|
|**Styling / Presentation props**|Influence visual output|`className`, `style`, `color`, `size`|
|**Render / Slot props**|Invert control — parent decides how to render parts|`renderItem`, `children`|

> 💡 Only spend time on component API design if the question specifically asks you to design a component (e.g. Autocomplete, Modal, Dropdown) or if a component is the dominant part of the product (e.g. Pinterest's masonry grid).


---

## O — Optimizations and deep dive

**Goal:** Discuss optimization opportunities and go deep on specific areas of interest. 
**Time:** ~40% of the session — the most important phase.

There's no fixed order here. You choose where to spend your time, guided by two principles:

**1. Focus on what's unique/important to this product.** E-commerce → SEO and performance. Collaborative editor → conflict resolution and real-time sync. Don't waste time on things that don't affect the architecture.

**2. Showcase your actual strengths.** If you know accessibility deeply, go there. If performance is your strength, dig into that. Aim to teach the interviewer something. Stay product-relevant.

### Available deep-dive areas

- [[Performance Optimization]] — Core Web Vitals, lazy loading, code splitting, virtualization, image optimization
- Networking techniques — caching, offline sync, retry logic → [[Caching Strategies]], [[Networking & APIs]]
- User experience — loading states, skeleton screens, error states, optimistic updates
- [[Accessibility (A11y)]] — keyboard nav, ARIA, focus management, screen reader support
- Search engine optimization — SSR, structured data, meta tags → [[Rendering Strategies]]
- [[Internationalization (i18n)]] — RTL, locale-aware formatting, dynamic locale loading
- Multi-device support — responsive design, touch interactions, PWA
- Security — XSS, CSRF, Content Security Policy

> Refer to our [Best Practices for Building User Interfaces Guide](https://www.greatfrontend.com/front-end-interview-guidebook/user-interface-questions-cheatsheet) for details on each topic.

### What to AVOID spending time on

These topics are generic, don't affect architecture, and waste interview time:

|❌ Avoid|Why|
|---|---|
|**JS framework debates** (React vs Vue vs Angular)|Interviewer cares about structure, not library preference|
|**CSS framework / design system choices** (Tailwind vs MUI)|Unless the question explicitly involves UI scalability or theming|
|**Generic performance advice** (minification, image compression)|Only mention if it's _core_ to the specific problem (e.g. rendering at scale)|
|**Logging, analytics, monitoring**|Doesn't affect core architecture|
|**DevOps / CI/CD** (Docker, GitHub Actions)|Irrelevant unless it directly impacts client perf or FE releases|
|**Build tooling** (Webpack vs Vite, linting, formatting)|Implementation detail, not architecture|

### When it IS OK to mention the JS framework

Only when the choice has **meaningful architectural implications**:

- **Rendering strategy depends on it** — e.g. "This is a content-heavy site so I'd use Next.js for SSR/SSG support and edge caching"
- **The problem domain dictates it** — highly dynamic dashboard → CSR framework; SEO-critical marketing site → Next.js / Remix / Nuxt
- **CDN/edge delivery is tied to the framework** — e.g. Vercel's Next.js ecosystem

Don't mention it when the discussion is about data flow, caching, APIs, or component communication — those are conceptual and framework-independent.

> 💡 Spend time on a topic **only when it changes architectural trade-offs** — not when it's just an implementation detail every app needs.

### Choosing which areas to focus on (heuristics)

|Question type|Focus on|
|---|---|
|News feed / social app|Performance, pagination strategy, real-time updates|
|Collaborative editor|WebSockets, conflict resolution (OT/CRDT), state sync|
|E-commerce|SEO (SSR/SSG), Core Web Vitals, image optimization|
|UI Component|Accessibility, component API design, theming/customization|
|Media-heavy app|Image/video optimization, streaming, upload chunking|

---

## Summary

|Step|Goal|Time|What to produce|
|---|---|---|---|
|**R** — Requirements|Clarify what you're building and its scope|~10%|Functional list, non-functional list, agreed scope|
|**A** — Architecture|Identify key components and their relationships|~20%|Diagram with labeled components and data flows|
|**D** — Data model|Describe entities, their fields, and ownership|~10%|Entity table or TypeScript interfaces per component|
|**I** — Interface|Define how components communicate|~20%|API endpoints, event shapes, component prop types|
|**O** — Optimizations|Deep dive into product-specific areas|~40%|Perf/a11y/SEO/real-time improvements with trade-offs|

---

## RADIO applied to News Feed (quick reference)

|Step|Answer|
|---|---|
|R|Core: infinite scroll feed, like + comment. Non-functional: fast load, mobile + desktop. Out of scope: groups, stories.|
|A|Server (black box) → Data access layer (React Query) → Store (Zustand) → Feed UI → FeedPost + PostComposer|
|D|Server: `Post { id, author, content, image, reactions, created_time }`, `Feed { posts[], pagination }`. Client: `{ isLoading, error, cursor }`|
|I|`GET /feed?cursor=X&size=10` → paginated posts. `POST /feed/posts` → new post. `POST /posts/:id/react` → reaction update|
|O|Virtualized list (react-virtual), cursor pagination, optimistic like updates, image lazy loading, skeleton screens, a11y on post actions|

See: [[Case Study - News Feed (e.g. Facebook)]]