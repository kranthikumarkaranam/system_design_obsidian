# CLAUDE.md — FE System Design Obsidian Vault

## Agent Instruction File

> **Read this entire file before doing anything.** Every section is mandatory. Do not skip sections. Do not guess conventions — every convention is explicitly defined here.

---

## 1. PROJECT CONTEXT

**Who:** A frontend engineer preparing for FE system design interviews at FAANG-level companies.

**What:** An Obsidian knowledge vault for FE System Design interview prep.

**Source material:** GreatFrontend (https://www.greatfrontend.com/front-end-system-design) — structured FE SD study guide by Yangshun Tay (Sr. Meta Staff Engineer, formerly at Facebook/ByteDance).

**Why Obsidian:** The graph view visualizes how concepts connect. Every `[[wikilink]]` between notes draws an edge in the graph. The goal is for the graph to become a full visual map of the FE SD knowledge domain — case studies cluster around core concept nodes, and everything routes back to the central MOC.

**Interview framework used:** RADIO — Requirements, Architecture, Data model, Interface, Optimizations.

**Two question types:**
- **Applications** — e.g. News Feed, Google Docs, Messenger
- **UI Components** — e.g. Modal, Dropdown, Image Carousel

**Deep-dive topics that matter:** Performance, Accessibility, Rendering, Caching, Networking, State Management, Internationalization, Component Architecture.

---

## 2. VAULT FOLDER STRUCTURE

```
📁 system_design_obsidian/       ← Root (open this folder in Obsidian)
  📁 00 - MOC/                   ← Central index — entry point to everything
  📁 01 - Guidebook/             ← GreatFrontend guidebook notes, in sidebar order
  📁 02 - Core Concepts/         ← Technical concept notes
  📁 03 - Case Studies/          ← One note per case study, RADIO-structured
  CLAUDE.md                      ← This file (always at vault root)
```

### Folder rules

- **Never create new folders.** The 4-folder structure is fixed.
- **Never place files at vault root** except `CLAUDE.md`.
- **Never nest subfolders** inside the 4 main folders.

---

## 3. FILE NAMING CONVENTIONS

### Strict naming rules — no exceptions

| Folder | Pattern | Example |
|---|---|---|
| `00 - MOC/` | `FE SD - MOC.md` | Fixed name, never changes |
| `01 - Guidebook/` | `NN - FE SD - [Topic Name].md` | `03 - RADIO Framework.md` |
| `01 - Guidebook/` (sub-note) | `[Topic Name].md` | `FE vs BE System Design.md` |
| `02 - Core Concepts/` | `[Concept Name].md` | `Rendering Strategies.md` |
| `03 - Case Studies/` | `Case Study - [System Name].md` | `Case Study - Facebook News Feed.md` |
| `03 - Case Studies/` (template) | `_Case Study Template.md` | Underscore sorts it to top |

### Guidebook prefix numbers

Obsidian sorts files alphabetically. Prefix numbers enforce the GreatFrontend sidebar order:

```
01 - FE SD - Introduction.md
02 - FE SD - Types of Questions.md
03 - RADIO Framework.md
04 - FE SD - Evaluation Axes.md
05 - FE SD - Common Mistakes.md
06 - FE SD - Cheatsheet.md
FE vs BE System Design.md          ← sub-note, no prefix
```

### Naming rules

- Use title case for all file names
- No special characters except hyphens `-` and parentheses `()`
- Parentheses allowed for abbreviations: `Accessibility (A11y).md`, `Internationalization (i18n).md`
- Never abbreviate in file names unless the abbreviation is the canonical term (A11y, i18n)

---

## 4. COMPLETE FILE REGISTRY

`[EXISTS]` = note has been written and filled.
`[STUB]` = file must exist but content not yet written. When user provides source material for a stub, generate its full content using the correct template from Section 6.

### 00 - MOC/

| File | Status |
|---|---|
| `FE SD - MOC.md` | [EXISTS] |

### 01 - Guidebook/

| # | File | Status |
|---|---|---|
| 1 | `01 - FE SD - Introduction.md` | [EXISTS] |
| 2 | `02 - FE SD - Types of Questions.md` | [EXISTS] |
| 3 | `03 - RADIO Framework.md` | [EXISTS] |
| 4 | `04 - FE SD - Evaluation Axes.md` | [EXISTS] |
| 5 | `05 - FE SD - Common Mistakes.md` | [EXISTS] |
| 6 | `06 - FE SD - Cheatsheet.md` | [STUB] |
| — | `FE vs BE System Design.md` | [EXISTS] |

### 02 - Core Concepts/

| File | Status |
|---|---|
| `Rendering Strategies.md` | [EXISTS] |
| `State Management.md` | [EXISTS] |
| `Caching Strategies.md` | [EXISTS] |
| `Performance Optimization.md` | [EXISTS] |
| `Networking and APIs.md` | [EXISTS] |
| `Accessibility (A11y).md` | [EXISTS] |
| `Component Architecture.md` | [STUB] |
| `Internationalization (i18n).md` | [STUB] |

### 03 - Case Studies/

| File | Status |
|---|---|
| `_Case Study Template.md` | [EXISTS] |
| `Case Study - Facebook News Feed.md` | [EXISTS] |
| `Case Study - Autocomplete.md` | [EXISTS] |
| `Case Study - Google Docs.md` | [STUB] |
| `Case Study - Netflix Media Player.md` | [STUB] |
| `Case Study - Instagram Media Upload.md` | [STUB] |
| `Case Study - Messenger Real-time Chat.md` | [STUB] |
| `Case Study - Airbnb SEO.md` | [STUB] |
| `Case Study - Amazon E-commerce Performance.md` | [STUB] |
| `Case Study - Lexical Rich Text Editor.md` | [STUB] |
| `Case Study - Dropdown Menu Component.md` | [STUB] |
| `Case Study - Image Carousel Component.md` | [STUB] |
| `Case Study - Modal Dialog Component.md` | [STUB] |

---

## 5. TAG SYSTEM

Tags go on **line 2 of every note** — immediately after the H1 title, before any other content. No blank line between H1 and tags.

### Tag definitions

| Tag | Applied to | Meaning |
|---|---|---|
| `#moc` | MOC notes only | Central index hub |
| `#guidebook` | All `01 - Guidebook/` notes | Source: GreatFrontend guidebook |
| `#framework` | RADIO Framework note | A process or methodology |
| `#concept` | All `02 - Core Concepts/` notes | Standalone technical concept |
| `#case-study` | All `03 - Case Studies/` notes | A system to design end-to-end |
| `#source/greatfrontend` | Any note from GreatFrontend | Tracks content origin |
| `#to-revise` | Any note worth reviewing | Flag for pre-interview sessions |

### Tag placement — exact format

```markdown
# Note Title

#concept #source/greatfrontend #to-revise
Back to: [[FE SD - MOC]]
```

### Rules

- Tags on ONE line only, space-separated, no commas
- No blank line between H1 and the tag line
- Always include `#source/greatfrontend` for any note derived from GreatFrontend content
- Always include `#to-revise` on every note that contains exam-relevant content
- Never put tags anywhere else in the note

---

## 6. WIKILINK CONVENTIONS

Wikilinks are the core mechanic. Every `[[Note Name]]` draws an edge in the Obsidian graph. Broken links (wrong name, wrong case) create orphaned nodes — this breaks the graph.

### Canonical wikilink names

These are the exact strings to use inside `[[...]]`. They must match filenames exactly, case-sensitive, without the `.md` extension.

```
[[FE SD - MOC]]
[[01 - FE SD - Introduction]]
[[02 - FE SD - Types of Questions]]
[[03 - RADIO Framework]]
[[04 - FE SD - Evaluation Axes]]
[[05 - FE SD - Common Mistakes]]
[[06 - FE SD - Cheatsheet]]
[[FE vs BE System Design]]
[[Rendering Strategies]]
[[State Management]]
[[Caching Strategies]]
[[Performance Optimization]]
[[Networking and APIs]]
[[Accessibility (A11y)]]
[[Component Architecture]]
[[Internationalization (i18n)]]
[[Case Study - Facebook News Feed]]
[[Case Study - Autocomplete]]
[[Case Study - Google Docs]]
[[Case Study - Netflix Media Player]]
[[Case Study - Instagram Media Upload]]
[[Case Study - Messenger Real-time Chat]]
[[Case Study - Airbnb SEO]]
[[Case Study - Amazon E-commerce Performance]]
[[Case Study - Lexical Rich Text Editor]]
[[Case Study - Dropdown Menu Component]]
[[Case Study - Image Carousel Component]]
[[Case Study - Modal Dialog Component]]
```

### Mandatory linking rules

1. **Every note must link back to MOC** — place `Back to: [[FE SD - MOC]]` on the line directly after the tag line.
2. **Concept notes must list case studies** — every concept note has a "Used in these case studies" section linking every case study that uses it.
3. **Case studies must link all concepts** — every case study ends with a "Concepts used in this case study" section listing every concept it touches.
4. **Link inline in prose** — when a concept is mentioned naturally in text, make it a wikilink: `[[Performance Optimization]]`.
5. **Link on first mention** — link a concept the first time it appears in a note. Do not link the same concept more than once per note.
6. **Never use display aliases** — `[[Performance Optimization]]` not `[[Performance Optimization|perf]]`.

---

## 7. FORMATTING RULES

These rules apply to every note in every folder without exception.

### Structure

- **H1** (`#`) — note title only. Exactly one per note. Always at the very top.
- **H2** (`##`) — major sections only.
- **H3** (`###`) — subsections within an H2.
- **H4 and below** — never use.
- **Horizontal rules** (`---`) — separate every major section.

### Text formatting

- **Bold** (`**text**`) — key terms and things to memorize. Never for decoration.
- *Italic* — sparingly, for emphasis or new term introduction only.
- `Inline code` — for: file names, property names, CSS class names, method names, short values.
- Never underline.

### Callouts

Use `> 💡` for key insights, things to memorize, and interview tips. Never use Obsidian's native callout syntax (`> [!note]`).

```markdown
> 💡 RADIO is a checklist, not a rigid sequence. Backtrack freely between steps.
```

### Code blocks

Always specify the language. Use these language identifiers:

| Content | Identifier |
|---|---|
| TypeScript types/interfaces | ` ```typescript ` |
| JavaScript | ` ```javascript ` |
| HTTP endpoints | ` ```http ` |
| Bash / terminal | ` ```bash ` |
| Plain text / ASCII diagrams | ` ```text ` |

### Tables

- Use for comparisons, decision guides, and structured data.
- Never use tables for content that reads naturally as prose or bullet points.
- Always include a header row.

### Lists

- Use bullet points for unordered collections with no meaningful sequence.
- Use numbered lists only when order or sequence matters.
- Maximum 2 levels of nesting. Never nest deeper.
- Never use bullet points where prose flows naturally.

### Emoji

- Allowed only in MOC section headers: 📌 📚 🔧 🏗️ 🏷️
- Allowed inside `> 💡` callouts only.
- Never use emoji anywhere else in any note.

### Line spacing

- One blank line between paragraphs.
- No blank line between H1 and the tag line.
- One blank line between the tag/backlink block and the first `---`.

---

## 8. NOTE TEMPLATES — EXACT ANATOMY

This is the most critical section. Every note type has a mandatory structure. Deviating from these templates will break graph consistency and interview usability.

---

### 8.1 MOC Note

**File:** `00 - MOC/FE SD - MOC.md`
**Tags:** `#moc`

```markdown
# FE SD — Map of Content

#moc
> Central hub for the FE System Design interview prep vault. Start here.

---

## 📌 Start Here

- [[01 - FE SD - Introduction]] — What FE SD interviews are and why they're hard
- [[FE vs BE System Design]] — Key differences between FE and BE system design
- [[03 - RADIO Framework]] — The 5-step framework used in every answer

---

## 📚 Guidebook

- [[01 - FE SD - Introduction]] — Overview and guide structure
- [[02 - FE SD - Types of Questions]] — Applications vs UI Components, 16 question types
- [[03 - RADIO Framework]] — Requirements, Architecture, Data model, Interface, Optimizations
- [[04 - FE SD - Evaluation Axes]] — 7 axes interviewers score you on
- [[05 - FE SD - Common Mistakes]] — 7 mistakes that cost candidates the role
- [[06 - FE SD - Cheatsheet]] — Interview-day quick reference

---

## 🔧 Core Concepts

- [[Rendering Strategies]] — CSR, SSR, SSG, ISR — when to use each
- [[State Management]] — Server state vs client state, state shape design
- [[Caching Strategies]] — CDN, HTTP cache, Service Worker, in-memory, IndexedDB
- [[Performance Optimization]] — Core Web Vitals, loading, runtime, network
- [[Networking and APIs]] — Protocols, REST design, WebSockets, SSE, optimistic updates
- [[Accessibility (A11y)]] — POUR, ARIA, keyboard navigation, focus management
- [[Component Architecture]] — Component hierarchy, composition, separation of concerns
- [[Internationalization (i18n)]] — i18n patterns, RTL, locale, formatting

---

## 🏗️ Case Studies

- [[Case Study - Facebook News Feed]]
- [[Case Study - Autocomplete]]
- [[Case Study - Google Docs]]
- [[Case Study - Netflix Media Player]]
- [[Case Study - Instagram Media Upload]]
- [[Case Study - Messenger Real-time Chat]]
- [[Case Study - Airbnb SEO]]
- [[Case Study - Amazon E-commerce Performance]]
- [[Case Study - Lexical Rich Text Editor]]
- [[Case Study - Dropdown Menu Component]]
- [[Case Study - Image Carousel Component]]
- [[Case Study - Modal Dialog Component]]

---

## 🏷️ Tags used in this vault

| Tag | Meaning |
|---|---|
| `#moc` | Central index hub |
| `#guidebook` | GreatFrontend guidebook note |
| `#framework` | A process or methodology |
| `#concept` | Standalone technical concept |
| `#case-study` | A system to design end-to-end |
| `#source/greatfrontend` | Content sourced from GreatFrontend |
| `#to-revise` | Flag for pre-interview review |
```

---

### 8.2 Guidebook Note (01 - Guidebook/)

**Tags:** `#guidebook #source/greatfrontend #to-revise`

The RADIO Framework note also gets `#framework`.

```markdown
# [Article Title — matches GreatFrontend page heading exactly]

#guidebook #source/greatfrontend #to-revise
Back to: [[FE SD - MOC]]
Source: [Full URL of the GreatFrontend page]
Author: Yangshun Tay — Sr. Staff Engineer, Meta

---

## [Section heading — paraphrase from article, do not copy verbatim]

[Content as prose or structured bullet points. Paraphrase all content — never copy verbatim from source.]

> 💡 [Key insight or interview tip as a callout]

---

## [Next section heading]

[Content with inline wikilinks wherever a concept is named naturally.]

See: [[Related Note]]

---

## Summary

[2–4 sentence summary of the key takeaway from this note. Written as prose.]
```

**Rules specific to Guidebook notes:**
- The H1 title must match the GreatFrontend page heading as closely as possible.
- Always include the source URL and author attribution.
- Every concept mentioned by name must be wikilinked on its first appearance.
- End every Guidebook note with a "Summary" section.

---

### 8.3 RADIO Framework Note

**File:** `01 - Guidebook/03 - RADIO Framework.md`
**Tags:** `#guidebook #framework #source/greatfrontend #to-revise`

This note gets its own stricter template because it is the most referenced note in the entire vault.

```markdown
# RADIO Framework

#guidebook #framework #source/greatfrontend #to-revise
Back to: [[FE SD - MOC]]
Source: https://www.greatfrontend.com/front-end-system-design
Author: Yangshun Tay — Sr. Staff Engineer, Meta

> 💡 RADIO is a checklist, not a rigid linear sequence. Move between steps freely. Write "RADIO" on the whiteboard and check off each letter as you cover it.

---

## Overview

| Step | Full Name | Time allocation |
|---|---|---|
| R | Requirements | ~10% |
| A | Architecture | ~20% |
| D | Data Model | ~10% |
| I | Interface | ~40% |
| O | Optimizations | ~20% |

---

## R — Requirements

**Goal:** Clarify what to build before touching architecture.

**Two types:**

- **Functional requirements** — what the system must do (features)
- **Non-functional requirements** — how well it must do it (performance, a11y, SEO, offline, i18n)

**Approach:** Take initiative. List requirements yourself, then get alignment. Do not wait to be fed requirements.

**Core questions to ask:**
- Which features to focus on?
- What is core vs good-to-have?
- What devices/browsers must be supported?
- Offline support required?
- Performance targets?
- SEO required?
- Accessibility standard (WCAG 2.1 AA)?

**Output:** Write agreed requirements on the whiteboard before moving on.

---

## A — Architecture

**Goal:** Identify the major components and how they connect.

**The 4-layer client architecture (always use this — do not invent other layers):**

| Layer | What it contains | Example tools |
|---|---|---|
| **Server** | Black box — APIs only. HTTP/GraphQL/WebSocket. | REST, GraphQL, WebSocket |
| **View layer** | Components and pages. Presentation + local state only. | React, Vue |
| **Store / Model layer** | Cross-cutting shared data. Unidirectional data flow. | Redux Toolkit, Zustand, Jotai, MobX |
| **Data access layer** | Fetching, caching, error management. The only layer that touches offline storage. | React Query, tRPC, Apollo Client |

> 💡 Not every product needs all 4 layers. A simple UI Component may only need the View layer and no store at all.

**Separation of concerns:**
- View layer handles presentation and local component state only.
- Never put network calls directly inside components — that belongs in the Data access layer.
- Never put UI logic inside the Store layer — that belongs in the View layer.

**After drawing the architecture diagram:**
- Verbally describe what each box is responsible for.
- Identify where computation happens: client vs server trade-off.

**Tools for drawing:** Excalidraw, diagrams.net.

---

## D — Data Model

**Goal:** Define the shape of the data flowing through the system.

**Two categories of data:**

| Category | Description | Examples |
|---|---|---|
| **Server-originated** | Comes from the API. Persisted on the server. | User profile, posts, messages |
| **Client-only** | Lives only in the browser. Two subtypes: | |
| — Persisted | Will be sent to server eventually | Draft message, form input |
| — Ephemeral | OK to lose on tab close | UI state, modal open/closed |

**Output format:**
- Use TypeScript interfaces for all data types.
- Always separate server types from client UI state types.
- List each field with a comment explaining its purpose.
- Iterate — add fields as requirements evolve during the session.

```typescript
// Server data (from API)
type Post = {
  id: string;           // unique post identifier
  authorId: string;     // references User.id
  content: string;      // post body text
  createdAt: number;    // unix timestamp
  likeCount: number;    // denormalized for display speed
};

// Client UI state
type FeedState = {
  posts: Post[];         // ordered list from API
  cursor: string | null; // pagination cursor
  isLoading: boolean;    // loading indicator
  error: string | null;  // error message if fetch failed
};
```

---

## I — Interface

**Goal:** Define exactly how every component communicates with everything else.

**Three interface types:**

### Server ↔ Client (API protocols)

| Protocol | When to use |
|---|---|
| HTTP/REST | Default for most reads and writes |
| WebSockets | Bidirectional real-time (chat, live collaboration) |
| SSE (Server-Sent Events) | Server → client only, one-directional streaming |
| Long polling | Fallback when WebSockets unavailable |
| GraphQL | Flexible queries, unlikely needed in interviews |
| WebRTC | P2P media (video calls), very specific use case |

**REST endpoint format:**

```http
GET /api/v1/feed?userId={userId}&cursor={cursor}&limit=10
→ {
    posts: Post[],
    nextCursor: string | null,
    hasMore: boolean
  }
```

### Client ↔ Client (component communication)

| Pattern | When to use |
|---|---|
| Props + callbacks | Parent-child, foundational default |
| Store dispatch | Cross-component, global shared state |
| Pub/sub event listeners | Decoupled components, most common in browser APIs |

### UI Component props API

Only define this if the question is specifically about a UI Component (not an application).

```typescript
type DropdownProps = {
  // Data props
  options: Option[];               // list of selectable items
  value: string | null;            // currently selected value

  // Event/Callback props
  onChange: (value: string) => void;   // fires on selection
  onClose?: () => void;                // fires on dismiss

  // Configuration/Behavior props
  disabled?: boolean;              // disable interaction
  multiSelect?: boolean;           // allow multiple selections

  // Styling/Presentation props
  placeholder?: string;            // text shown when nothing selected
  className?: string;              // consumer-provided class override

  // Render/Slot props
  renderOption?: (option: Option) => React.ReactNode;  // custom option renderer
};
```

---

## O — Optimizations

**Goal:** Demonstrate depth in areas most relevant to this specific product.

**Guiding principle:** Do not give generic advice. Every optimization must be justified by the specific product being designed.

**Available optimization areas:**

| Area | Focus on when |
|---|---|
| [[Performance Optimization]] | Feeds, e-commerce, media-heavy apps |
| [[Networking and APIs]] | Real-time apps, large data transfers |
| UX | Any consumer-facing product |
| [[Accessibility (A11y)]] | Any public-facing product — always mention |
| SEO | Public pages, marketing sites, e-commerce |
| [[Internationalization (i18n)]] | Global products |
| Multi-device | Mobile web, cross-platform |
| Security | Auth flows, user data, payment |

**What to always avoid discussing in O:**
- JS framework debates (React vs Vue vs Angular)
- CSS framework choices (Tailwind vs CSS Modules)
- Generic performance advice not tied to the product
- Logging, analytics, monitoring setup
- DevOps, CI/CD, build tooling
- Infrastructure (servers, load balancers, databases) — that is BE SD

> 💡 Exception: mention frameworks only when the choice changes architectural trade-offs — e.g. Next.js when SSR/SSG strategy is a core part of the answer.

---

## RADIO Applied to Facebook News Feed

| Step | Answer |
|---|---|
| Requirements | Infinite scroll feed, like/comment, real-time updates, mobile web |
| Architecture | Data access layer (React Query) → Store (feed slice) → Feed UI (FeedList, PostCard) |
| Data Model | `Post`, `User`, `FeedState` TypeScript types |
| Interface | `GET /api/v1/feed?cursor=` with cursor pagination |
| Optimizations | List virtualization, image lazy loading, optimistic like updates |

See: [[Case Study - Facebook News Feed]]

---

## Summary

RADIO gives structure to an open-ended interview. Use it as a checklist to ensure coverage, not as a rigid script. The Interface step (I) deserves the most time — this is where technical depth shows. Always tailor the Optimizations step to the specific product being designed.
```

---

### 8.4 Concept Note (02 - Core Concepts/)

**Tags:** `#concept #source/greatfrontend #to-revise`

```markdown
# [Concept Name]

#concept #source/greatfrontend #to-revise
Back to: [[FE SD - MOC]]
Used in: [[03 - RADIO Framework]] → [which RADIO step this concept appears in]

---

## What is [Concept Name]?

[2–4 sentence definition. What problem does this concept solve? When does it become relevant in a system design interview?]

---

## [Core section — named for the main content, e.g. "Strategies", "Patterns", "Techniques"]

[Main technical content. Use tables for comparisons. Use code blocks for code. Use callouts for things to memorize.]

> 💡 [Key insight]

---

## [Second major section — e.g. "When to Use", "Decision Guide", "Trade-offs"]

[Decision table or if/then guide for choosing between options.]

| Option | Use when | Avoid when |
|---|---|---|
| [Option A] | [condition] | [condition] |
| [Option B] | [condition] | [condition] |

---

## [Third major section if needed — e.g. "Implementation Notes", "Code Example"]

```typescript
// Code with comments explaining every non-obvious line
```

---

## Used in these case studies

[This section is mandatory. It creates bidirectional edges in the graph.]

- [[Case Study - X]] — [one sentence on how this concept applies to that case study]
- [[Case Study - Y]] — [one sentence on how this concept applies to that case study]
```

**Rules specific to Concept notes:**
- The "Used in these case studies" section is mandatory. If no case studies exist yet, write `(None yet — add as case studies are created)`.
- The "Used in:" line after Back to MOC must specify which RADIO step (R, A, D, I, or O) this concept most often appears in.
- Every concept note must have at least one code example if the concept has any technical implementation detail.

---

### 8.5 Case Study Note (03 - Case Studies/)

**Tags:** `#case-study #source/greatfrontend #to-revise`

```markdown
# Case Study - [System Name]

#case-study #source/greatfrontend #to-revise
Back to: [[FE SD - MOC]]
Question type: [[02 - FE SD - Types of Questions]] → [Application / UI Component]
Framework: [[03 - RADIO Framework]]

---

## Requirements (R)

### Functional requirements

- [Specific feature 1 — written as a user-facing capability]
- [Specific feature 2]
- [Specific feature 3]

### Non-functional requirements

- [Performance requirement — e.g. "Feed loads within 2s on mobile 4G"]
- [Accessibility — e.g. "WCAG 2.1 AA compliant"]
- [Device/browser target — e.g. "Mobile and desktop web, Chrome/Safari/Firefox"]
- [Scale target if relevant — e.g. "Millions of concurrent users"]

### Out of scope

- [Thing 1 not being designed in this session]
- [Thing 2 not being designed in this session]

---

## Architecture (A)

**Question type:** [Application / UI Component]

**Major components:**

| Component | Responsibility |
|---|---|
| [Component 1] | [What it renders or manages] |
| [Component 2] | [What it renders or manages] |

**4-layer breakdown:**

| Layer | What lives here for this product |
|---|---|
| Server | [API endpoints used — e.g. REST feed API, WebSocket for notifications] |
| View layer | [Main components — e.g. FeedList, PostCard, LikeButton] |
| Store / Model layer | [Global state — e.g. feedSlice (posts, cursor), userSlice (currentUser)] |
| Data access layer | [Fetching strategy — e.g. React Query for feed, SWR for user profile] |

**Data flow:**

[1–3 sentences describing how data moves from server to screen. Be specific — name the actual components and layers.]

**Architecture diagram:**

```text
[Server API]
     ↓ HTTP / WebSocket
[Data Access Layer]  ← React Query / tRPC
     ↓
[Store / Model Layer] ← Redux / Zustand
     ↓
[View Layer]
  ├── [ParentComponent]
  │     ├── [ChildComponent A]
  │     └── [ChildComponent B]
  └── [SiblingComponent]
```

---

## Data Model (D)

```typescript
// ── Server data (from API) ──────────────────────────────────────

type [Entity1] = {
  id: string;          // [description]
  [field]: [type];     // [description]
};

type [Entity2] = {
  id: string;          // [description]
  [field]: [type];     // [description]
};

// ── Client UI state ─────────────────────────────────────────────

type [State] = {
  [field]: [type];     // [description — note if ephemeral or persisted]
};
```

**Server state:** [List the server-originated entities and where they come from]

**Client state:** [List the UI-only state and which component owns it]

---

## Interface (I)

### Server API

```http
[METHOD] /api/v1/[resource]?[params]
Request:  { [request body shape if POST/PUT] }
Response: { [response shape with field names and types] }
```

[Add more endpoints if the system needs them. One code block per endpoint.]

### WebSocket events (only include if the product is real-time)

```text
Client → Server: { type: "[event-name]", payload: { [fields] } }
Server → Client: { type: "[event-name]", payload: { [fields] } }
```

### Component props API (only include if question type is UI Component)

```typescript
type [ComponentName]Props = {
  // Data props
  [prop]: [type];      // [description]

  // Event/Callback props
  [onEvent]: ([args]) => void;  // [when it fires]

  // Configuration/Behavior props
  [prop]?: [type];     // [description, default value]

  // Styling/Presentation props
  className?: string;  // consumer-provided class override

  // Render/Slot props
  [renderProp]?: ([args]) => React.ReactNode;  // [description]
};
```

---

## Optimizations (O)

### Performance

- [Specific optimization technique] — [why it matters for this specific product]
- [Another optimization] — [why it matters]

Links: [[Performance Optimization]]

### Accessibility

- [Specific a11y consideration for this product]
- [Keyboard interaction that must be handled]
- [ARIA role or attribute required]

Links: [[Accessibility (A11y)]]

### [Third area — choose the most relevant for this product: Networking, Caching, SEO, i18n, Security]

- [Specific consideration]

Links: [[Relevant Concept Note]]

---

## Concepts used in this case study

[Mandatory. Every concept this case study touches must be linked here. This section builds bidirectional graph edges.]

- [[Rendering Strategies]] — [one sentence on how it applies here]
- [[State Management]] — [one sentence on how it applies here]
- [[Networking and APIs]] — [one sentence on how it applies here]
- [[Performance Optimization]] — [one sentence on how it applies here]
- [[Caching Strategies]] — [one sentence on how it applies here]
- [[Accessibility (A11y)]] — [one sentence on how it applies here]
```

**Rules specific to Case Study notes:**
- TypeScript types in the Data Model section are mandatory. Never write this section in prose only.
- At least one real API endpoint example is mandatory in the Interface section.
- The "Concepts used in this case study" section is mandatory, even if some links are stubs.
- The architecture diagram (text/ASCII) is mandatory. Do not skip it.
- Do not include the WebSocket events block unless the product actually requires real-time communication.
- Do not include the Component props API block unless the question type is explicitly "UI Component".

---

### 8.6 Case Study Template Note

**File:** `03 - Case Studies/_Case Study Template.md`

This is a blank version of the Case Study template (Section 8.5) with all placeholder text intact but no content filled in. It exists so the user can duplicate it for each new case study. Generate it exactly as the template in 8.5 but with every `[bracketed placeholder]` left as-is and no real content filled in.

---

### 8.7 Evaluation Axes Note

**File:** `01 - Guidebook/04 - FE SD - Evaluation Axes.md`
**Tags:** `#guidebook #source/greatfrontend #to-revise`

Each axis uses this sub-structure:

```markdown
## N. [Axis Name]

**What interviewers check:**
- [Specific observable behavior 1]
- [Specific observable behavior 2]

**Links:** [[Related Concept Note]] → [which part of the concept is relevant]
```

---

### 8.8 Common Mistakes Note

**File:** `01 - Guidebook/05 - FE SD - Common Mistakes.md`
**Tags:** `#guidebook #source/greatfrontend #to-revise`

Each mistake uses this sub-structure:

```markdown
## ❌ Mistake [N] — [Mistake name]

**What happens:** [Behavioral description — what the candidate does]

**Why it hurts:** [Specific impact on interview score]

**Fix:** [Concrete, actionable correction — written as an instruction to the candidate]

See: [[Related Note]]
```

---

## 9. GRAPH DESIGN INTENT

The Obsidian graph is the primary output of this vault. Every wikilink is an intentional edge.

### Target graph topology

```
FE SD - MOC (center hub — highest degree node)
    │
    ├── 03 - RADIO Framework (second-highest degree)
    │
    ├── Core Concepts (satellite cluster)
    │     ├── Performance Optimization  ← most-linked concept node
    │     ├── Networking and APIs
    │     ├── State Management
    │     ├── Rendering Strategies
    │     ├── Caching Strategies
    │     ├── Accessibility (A11y)
    │     ├── Component Architecture
    │     └── Internationalization (i18n)
    │
    └── Case Studies (dense cluster — each links to 4–8 concept nodes)
          ├── Case Study - Facebook News Feed ──► Performance, State, Networking, Caching
          ├── Case Study - Google Docs ──────────► Networking (WS), State, A11y, Performance
          ├── Case Study - Messenger ────────────► Networking (WS), State, Performance
          ├── Case Study - Netflix ──────────────► Performance, Networking, Caching, Rendering
          ├── Case Study - Airbnb SEO ───────────► Rendering (SSR), Performance, i18n
          ├── Case Study - Amazon ───────────────► Performance, Caching, Rendering, State
          ├── Case Study - Instagram Upload ──────► Performance, Networking, State
          ├── Case Study - Autocomplete ──────────► Performance, Networking, A11y, State
          ├── Case Study - Dropdown ─────────────► A11y, Component Architecture, State
          ├── Case Study - Modal ────────────────► A11y, Component Architecture, State
          ├── Case Study - Image Carousel ────────► A11y, Performance, Component Architecture
          └── Case Study - Lexical Rich Text ─────► State, Networking, Performance, A11y
```

**Performance Optimization** must be the most-linked concept node — it is relevant to virtually every case study.

**Accessibility (A11y)** must appear in every case study, at minimum in the Optimizations section.

---

## 10. HOW TO PROCESS NEW SOURCE MATERIAL

When the user provides a new article, screenshot, or URL from GreatFrontend, follow these steps in exact order.

### Step 1 — Identify the note type

| Source content | Note type | Folder | Filename |
|---|---|---|---|
| Intro / overview article | Guidebook note | `01 - Guidebook/` | `01 - FE SD - Introduction.md` |
| Types of questions article | Guidebook note | `01 - Guidebook/` | `02 - FE SD - Types of Questions.md` |
| RADIO framework article | Framework note | `01 - Guidebook/` | `03 - RADIO Framework.md` |
| Evaluation / scoring article | Guidebook note | `01 - Guidebook/` | `04 - FE SD - Evaluation Axes.md` |
| Common mistakes article | Guidebook note | `01 - Guidebook/` | `05 - FE SD - Common Mistakes.md` |
| Cheatsheet | Guidebook note | `01 - Guidebook/` | `06 - FE SD - Cheatsheet.md` |
| A specific system to design | Case study note | `03 - Case Studies/` | `Case Study - [Name].md` |
| A technical concept | Concept note | `02 - Core Concepts/` | `[Concept Name].md` |

### Step 2 — Extract from the source

- **Main topic** → H1 title and H2 section headings
- **Key facts, rules, patterns** → prose and bullet points
- **Comparisons** (X vs Y) → tables
- **Code examples or APIs** → fenced code blocks with language identifier
- **Decision guides** (when to use X) → decision tables
- **Interview tips, things to memorize** → `> 💡` callouts
- **Concepts mentioned by name** → inline wikilinks on first mention

### Step 3 — Apply the correct template from Section 8

Match the note type identified in Step 1 to the template in Section 8. Fill every section of the template. Do not skip sections — write `(Not applicable for this product)` if a section genuinely does not apply.

### Step 4 — Add all wikilinks

- `Back to: [[FE SD - MOC]]` — mandatory in every note
- Link every concept mentioned in the text on its first appearance
- For case studies: fill the "Concepts used in this case study" section completely
- For concept notes: fill the "Used in these case studies" section completely

### Step 5 — Add tags

Apply tags from Section 5. Tags on line 2, one line, space-separated.

### Step 6 — Update bidirectional links

If a new case study was created:
- Go to every concept note it links to
- Add this case study to the "Used in these case studies" section of each concept note

If a new concept note was created:
- Go to every existing case study that is relevant
- Add a link to this concept in its "Concepts used in this case study" section

### Step 7 — State the output path

Always state the complete folder path when outputting a file:

```
01 - Guidebook/03 - RADIO Framework.md
02 - Core Concepts/Rendering Strategies.md
03 - Case Studies/Case Study - Facebook News Feed.md
```

---

## 11. ABSOLUTE RULES — NEVER VIOLATE

These are hard constraints. There are no exceptions.

- ❌ Never create a note without `Back to: [[FE SD - MOC]]`
- ❌ Never mention a concept in prose without linking it `[[Concept Name]]` on first mention
- ❌ Never create a case study without TypeScript types in the Data Model section
- ❌ Never create a case study without at least one real API endpoint in the Interface section
- ❌ Never create a case study without the "Concepts used in this case study" section
- ❌ Never create a concept note without the "Used in these case studies" section
- ❌ Never put tags anywhere except line 2 of the note
- ❌ Never use Obsidian native callout syntax `> [!note]` — always use `> 💡`
- ❌ Never use H4 (`####`) or deeper
- ❌ Never use emoji outside of MOC section headers and `> 💡` callouts
- ❌ Never create new folders
- ❌ Never place a file at the vault root (except `CLAUDE.md`)
- ❌ Never skip the architecture diagram in a case study note
- ❌ Never write a case study architecture using anything other than the 4-layer model (Server / View / Store / Data Access)
- ❌ Never include the WebSocket events block in a case study that does not require real-time communication
- ❌ Never include the Component props API block in an Application case study
- ❌ Never use `[[Networking & APIs]]` — the correct wikilink is `[[Networking and APIs]]`
- ❌ Never fabricate content not present in the provided source material — if something is unclear, note it as `[TODO: verify from source]`

---

## 12. REGENERATION ORDER

If regenerating the entire vault from scratch, create files in this exact order:

```
1.  00 - MOC/FE SD - MOC.md
2.  01 - Guidebook/01 - FE SD - Introduction.md
3.  01 - Guidebook/FE vs BE System Design.md
4.  01 - Guidebook/02 - FE SD - Types of Questions.md
5.  01 - Guidebook/03 - RADIO Framework.md
6.  01 - Guidebook/04 - FE SD - Evaluation Axes.md
7.  01 - Guidebook/05 - FE SD - Common Mistakes.md
8.  01 - Guidebook/06 - FE SD - Cheatsheet.md            ← STUB
9.  02 - Core Concepts/Rendering Strategies.md
10. 02 - Core Concepts/State Management.md
11. 02 - Core Concepts/Caching Strategies.md
12. 02 - Core Concepts/Performance Optimization.md
13. 02 - Core Concepts/Networking and APIs.md
14. 02 - Core Concepts/Accessibility (A11y).md
15. 02 - Core Concepts/Component Architecture.md         ← STUB
16. 02 - Core Concepts/Internationalization (i18n).md    ← STUB
17. 03 - Case Studies/_Case Study Template.md
18. 03 - Case Studies/Case Study - Facebook News Feed.md
19. 03 - Case Studies/Case Study - Autocomplete.md
20. 03 - Case Studies/Case Study - Google Docs.md        ← STUB
21. 03 - Case Studies/Case Study - Netflix Media Player.md        ← STUB
22. 03 - Case Studies/Case Study - Instagram Media Upload.md      ← STUB
23. 03 - Case Studies/Case Study - Messenger Real-time Chat.md    ← STUB
24. 03 - Case Studies/Case Study - Airbnb SEO.md                  ← STUB
25. 03 - Case Studies/Case Study - Amazon E-commerce Performance.md ← STUB
26. 03 - Case Studies/Case Study - Lexical Rich Text Editor.md    ← STUB
27. 03 - Case Studies/Case Study - Dropdown Menu Component.md     ← STUB
28. 03 - Case Studies/Case Study - Image Carousel Component.md    ← STUB
29. 03 - Case Studies/Case Study - Modal Dialog Component.md      ← STUB
```

Use Section 8 templates for structure. Use Section 6 for wikilinks. Use Section 5 for tags. Use Section 7 for formatting.

---

*Version 2.0 — Complete rewrite. Stricter templates, explicit rules for every note type, mandatory sections enforced, wikilink naming corrected, graph topology documented.*