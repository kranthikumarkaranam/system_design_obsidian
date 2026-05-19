# CLAUDE.md — FE System Design Obsidian Vault

## Agent Instruction File

> **Purpose of this file:** When a new agent or new Claude session reads this file, it must be able to:
> 
> 1. Understand the full project context
> 2. Recreate the exact folder and file structure
> 3. Know the precise anatomy of every note type
> 4. Know every linking rule, tag, and convention
> 5. Generate new notes from raw source material (screenshots, PDFs, articles) in exactly the right format

---

## 1. PROJECT CONTEXT

**Who:** A frontend engineer preparing for FE system design interviews at FAANG-level companies.

**What:** An Obsidian knowledge vault for FE System Design interview prep.

**Source material:** GreatFrontend (https://www.greatfrontend.com/front-end-system-design) — a structured FE SD study guide.

**Why Obsidian:** The graph view in Obsidian visualizes how concepts connect. Every `[[wikilink]]` between notes draws an edge in the graph. The goal is for the graph to become a visual map of the entire FE SD knowledge domain — where case studies cluster around core concept nodes, and everything routes back to the central MOC (Map of Content).

**Interview context:**

- FE system design interviews are open-ended
- Framework used: **RADIO** (Requirements, Architecture, Data model, Interface, Optimizations)
- Two question types: **Applications** (e.g. News Feed, Google Docs) and **UI Components** (e.g. Modal, Dropdown)
- Deep-dive topics that matter: Performance, Accessibility, Rendering, Caching, Networking, State
- Source of truth for all content: GreatFrontend guide + author Yangshun Tay (Sr. Meta Staff Engineer)

---

## 2. VAULT FOLDER STRUCTURE

```
📁 FE Interview Prep/               ← Root vault folder (open this in Obsidian)
  📁 00 - MOC/                      ← Central index — entry point to everything
  📁 01 - Guidebook/                ← All GreatFrontend guidebook notes, in sidebar order
  📁 02 - Core Concepts/            ← Technical concept notes (Rendering, Caching, A11y, etc.)
  📁 03 - Case Studies/             ← One note per case study (Facebook Feed, Google Docs, etc.)
  CLAUDE.md                         ← This file (keep at vault root)
```

### Guidebook sidebar order (GreatFrontend left-nav sequence — respect this order)

The `01 - Guidebook/` folder mirrors the exact order of the GreatFrontend guidebook sidebar:

```
1. Introduction
2. Types of questions
3. RADIO framework
4. Evaluation axes
5. Common mistakes
6. Cheatsheet
```

Obsidian sorts files alphabetically, so filenames are prefixed with the order number to enforce the correct sequence in the file explorer:

```
01 - FE SD - Introduction.md
02 - FE SD - Types of Questions.md
03 - RADIO Framework.md
04 - FE SD - Evaluation Axes.md
05 - FE SD - Common Mistakes.md
06 - FE SD - Cheatsheet.md
FE vs BE System Design.md          ← sub-note of Introduction, no prefix needed
```

### General naming rules

- Folders: `NN - Name` (two-digit prefix + space + dash + space + name)
- Guidebook files: `NN - FE SD - Topic Name.md` (order prefix + "FE SD -" prefix)
- Case studies: always `Case Study - [System Name].md`
- Case study template: `_Case Study Template.md` (underscore sorts it to top)
- Concept notes: named exactly as they appear in wikilinks — `Accessibility (A11y).md`, `Networking and APIs.md`

---

## 3. COMPLETE FILE REGISTRY

Every file that exists or must exist. `[EXISTS]` = created and filled. `[STUB]` = linked but content not yet written. When the user provides source material for a stub, generate its full content.

### 00 - MOC/

- [EXISTS] `FE SD - MOC.md` — central index hub

### 01 - Guidebook/

_(Files are prefixed with order numbers to match GreatFrontend sidebar sequence)_

|#|Filename|Status|Content|
|---|---|---|---|
|1|`01 - FE SD - Introduction.md`|[EXISTS]|What FE SD interviews are, why they're hard, senior-level importance, guide overview|
|2|`02 - FE SD - Types of Questions.md`|[EXISTS]|Applications table (16 types) + UI Components section|
|3|`03 - RADIO Framework.md`|[EXISTS]|Full RADIO breakdown — all 5 steps, time allocation, examples|
|4|`04 - FE SD - Evaluation Axes.md`|[EXISTS]|7 evaluation dimensions with what interviewers check|
|5|`05 - FE SD - Common Mistakes.md`|[EXISTS]|7 mistakes in What/Why/Fix format|
|6|`06 - FE SD - Cheatsheet.md`|[STUB]|Quick-reference cheatsheet for interview day|
|—|`FE vs BE System Design.md`|[EXISTS]|Comparison table, FE focus areas, classic FB News Feed example|

### 02 - Core Concepts/

- [EXISTS] `Rendering Strategies.md`
- [EXISTS] `State Management.md`
- [EXISTS] `Caching Strategies.md`
- [EXISTS] `Performance Optimization.md`
- [EXISTS] `Networking and APIs.md`
- [EXISTS] `Accessibility (A11y).md`
- [STUB] `Component Architecture.md`
- [STUB] `Internationalization (i18n).md`

### 03 - Case Studies/

- [EXISTS] `_Case Study Template.md` — blank RADIO template; duplicate for each new case study
- [EXISTS] `Case Study - Facebook News Feed.md`
- [EXISTS] `Case Study - Autocomplete.md`
- [STUB] `Case Study - Google Docs.md`
- [STUB] `Case Study - Netflix Media Player.md`
- [STUB] `Case Study - Instagram Media Upload.md`
- [STUB] `Case Study - Messenger Real-time Chat.md`
- [STUB] `Case Study - Airbnb SEO.md`
- [STUB] `Case Study - Amazon E-commerce Performance.md`
- [STUB] `Case Study - Lexical Rich Text Editor.md`
- [STUB] `Case Study - Dropdown Menu Component.md`
- [STUB] `Case Study - Image Carousel Component.md`
- [STUB] `Case Study - Modal Dialog Component.md`

---

## 4. TAG SYSTEM

Every note must have tags on line 2 (immediately after the H1 title, before any other content).

|Tag|Used on|Meaning|
|---|---|---|
|`#concept`|Core concept notes|A standalone technical concept|
|`#framework`|Framework notes|A process, mental model, or methodology|
|`#case-study`|Case study notes|A real system to design end-to-end|
|`#mistake`|Mistakes notes|Things to avoid in interviews|
|`#to-revise`|Any note worth reviewing|Mark for pre-interview review sessions|
|`#source/greatfrontend`|Notes from GreatFrontend|Tracks which notes came from this source|

**Tag placement example:**

```markdown
# Note Title

#concept #source/greatfrontend #to-revise
Back to: [[FE SD - MOC]]
```

Tags go on ONE line, space-separated. No blank line between H1 and tags.

---

## 5. WIKILINK CONVENTIONS

Wikilinks are the core mechanic. Every link `[[Note Name]]` creates an edge in the graph.

### Rules for linking:

1. **Always link back to MOC** — every note has `Back to: [[FE SD - MOC]]` near the top
2. **Link "Introduced in"** — if a concept was first seen in a specific article, add `Introduced in: [[Note Name]]`
3. **Link "Used in"** — concept notes list which case studies use them
4. **Cross-link concepts** — every concept note links to related concepts where natural
5. **Case studies link to ALL concepts they touch** — this is what makes the graph dense
6. **Link inline in prose** — when mentioning a concept in text, link it: `[[Performance Optimization]]`

### Exact wikilink names (must match filenames exactly, case-sensitive):

```
[[FE SD - MOC]]
[[01 - FE SD - Introduction]]
[[FE vs BE System Design]]
[[RADIO Framework]]
[[FE SD Question Types]]
[[FE SD Evaluation Axes]]
[[FE SD Common Mistakes]]
[[Rendering Strategies]]
[[State Management]]
[[Caching Strategies]]
[[Performance Optimization]]
[[Networking & APIs]]           ← NOTE: uses & not "and" in wikilinks
[[Accessibility (A11y)]]
[[Internationalization (i18n)]]
[[Component Architecture]]
[[Case Study - Facebook News Feed]]
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

⚠️ IMPORTANT: The file `Networking and APIs.md` uses "and" but the wikilink is `[[Networking & APIs]]` — Obsidian resolves these differently. The file should be renamed to `Networking & APIs.md` to match the wikilink. If regenerating, use `Networking & APIs.md` as the filename.

---

## 6. NOTE ANATOMY — EXACT TEMPLATES

### 6.1 MOC Note (00 - MOC/)

```markdown
# [Title] — Map of Content

> [One-line description of what this MOC covers]

## 🗺️ How this vault works
- [Usage tip 1]
- [Usage tip 2]

---

## 📌 Start Here
- [[Note]] — [one-line description]

---

## 📚 Core Topics
- [[Note]] — [one-line description]

---

## 🔧 Core Concepts
*(fill these in as you study each topic)*
- [[Concept Note]] — [one-line description]

---

## 🏗️ Case Studies
*(each case study links back to the concepts it uses)*
- [[Case Study - X]]

---

## 🏷️ Tags used in this vault
| Tag | Meaning |
|-----|---------|
| `#tag` | meaning |
```

### 6.2 Intro / Article Note (01 - Intro/)

```markdown
# [Article Title]

#source/greatfrontend #to-revise
Source: [URL]
Author: [Author name and role]

Back to: [[FE SD - MOC]]

---

## [Section heading from article]

[Content as bullet points or prose — paraphrase, never copy verbatim]

> 💡 [Key insight as a callout]

---

## [Another section]

[Content with inline wikilinks to concepts where natural]

See: [[Related Note]]
```

### Correct 4-layer client architecture (from article — do NOT use old 5-layer version)

|Layer|What it contains|
|---|---|
|**Server**|Black box — HTTP/GraphQL/WebSocket APIs|
|**View layer**|Components/pages — presentation + local state ONLY|
|**Store / Model layer**|Cross-cutting data — Redux Toolkit, Zustand, Jotai, MobX|
|**Data access layer**|Fetching, caching, errors — React Query, tRPC, Apollo Client|

⚠️ Do NOT use: "Controller/Logic layer", "Service/Network layer", "Cache layer" — these are NOT in the source.

### 6.3 Framework Note (02 - Framework/)

```markdown
# [Framework Name]

#framework #source/greatfrontend #to-revise
Back to: [[FE SD - MOC]]
Source: [Source description]

---

## What is [Framework]?

[Brief explanation — what problem it solves, when to use it]

```

[Acronym breakdown as code block if applicable]

```

> 💡 [Core insight as callout]

---

## [Each step/component as its own H2]

**Goal:** [What this step achieves]

[Content with bullet points, tables, and code examples]

---

## Summary table

| Column | Column |
|--------|--------|
| row | row |

---

## [Framework] applied to [Example] (quick reference)

| Step | Answer |
|------|--------|
| [Step] | [Answer] |

See: [[Related Case Study]]
```

### 6.4 Concept Note (06 - Core Concepts/)

````markdown
# [Concept Name]

#concept #to-revise
Back to: [[FE SD - MOC]]
Used in: [[RADIO Framework]] → [which step]

---

## [Core explanation section]

[Explanation with tables, comparisons, code snippets]

---

## [Technique / Pattern section]

[Content — be specific, include code examples for technical concepts]

```[language]
// Code example with comments
````

---

## [Decision guide / when to use]

[Decision tree or table showing when to apply this concept]

---

## Used in these case studies

[This section is critical — it connects concepts to case studies in the graph]

- [[Case Study - X]] — [why it's relevant]
- [[Case Study - Y]] — [why it's relevant]

````

### 6.5 Case Study Note (05 - Case Studies/)

```markdown
# Case Study - [System Name]

#case-study #to-revise
Back to: [[FE SD - MOC]]
Question type: [[FE SD Question Types]] → [Application / UI Component]

---

## Requirements (R)

### Functional
- [Feature 1]
- [Feature 2]

### Non-functional
- [Performance requirement]
- [Accessibility requirement]
- [Scale/device target]

### Out of scope (for this session)
- [What we're NOT designing]

---

## Architecture (A)

**Major components:**
- [Component 1] — [what it does]
- [Component 2] — [what it does]

**Data flow:**
[Description of how data moves through the system]

**Architecture diagram (text):**
````

[ASCII or text representation of component hierarchy]

````

---

## Data Model (D)

```typescript
// Server data (from API)
type [Entity] = {
  [field]: [type]   // comment
}

// Client UI state
type [State] = {
  [field]: [type]   // comment
}
````

**Server state:** [what comes from API] **Client state:** [what is UI-only]

---

## Interface / API (I)

**Server API:**

```
[HTTP METHOD] /api/[endpoint]?[params]
  → { [response shape] }
```

**WebSocket events (if real-time):**

```
Client → Server: { type: '[event]', payload: {...} }
Server → Client: { type: '[event]', payload: {...} }
```

**Component API (if UI component):**

```typescript
type [Component]Props = {
  [prop]: [type]   // [description]
}
```

---

## Optimizations (O)

### Performance

- [Specific optimization] — [why it matters here]
- Links: [[Performance Optimization]]

### Accessibility

- [Specific a11y consideration]
- Links: [[Accessibility (A11y)]]

### [Other relevant area]

- [Content]

---

## Concepts used in this case study

[CRITICAL: link every concept this system uses — this builds the graph]

- [[Rendering Strategies]] — [how it's used here]
- [[State Management]] — [how it's used here]
- [[Networking & APIs]] — [how it's used here]
- [[Performance Optimization]] — [how it's used here]
- [[Caching Strategies]] — [how it's used here]
- [[Accessibility (A11y)]] — [how it's used here]

````

### 6.6 Evaluation / Mistakes Notes (04 - Eval & Mistakes/)

For **Common Mistakes**, each mistake uses this sub-structure:
```markdown
## ❌ Mistake N — [Mistake name]

**What happens:** [Behavior description]

**Why it hurts:** [Impact on interview score]

**Fix:** [Concrete actionable correction] See [[Related Note]].
````

For **Evaluation Axes**, each axis uses:

```markdown
## N. [Axis Name]

- [What is evaluated — question 1]
- [What is evaluated — question 2]

Links: [[Related Note]] → [specific part]
```

---

## 7. FORMATTING RULES

These rules apply to ALL notes:

1. **H1 = note title** — exactly one H1 per note, at the very top
2. **H2 = major sections** — use for top-level sections
3. **H3 = subsections** — use within a section
4. **Horizontal rules `---`** separate major sections
5. **Callouts** use `> 💡 [text]` format (not Obsidian callout syntax)
6. **Tables** are used for comparisons, not for lists that could be prose
7. **Code blocks** for: TypeScript interfaces, API endpoints, HTTP headers, code patterns
    - Always specify language: ` ```typescript `, ` ```javascript `, ` ```http `, ` ```bash `
8. **Bold** `**text**` for emphasis on key terms, never for decoration
9. **Never use bullet points for everything** — use prose where ideas connect
10. **Emoji** only in MOC headers (📌 📚 🔧 🏗️ 🏷️) — not in other notes
11. **`> 💡`** callouts for: key insights, things to memorize, interview tips
12. **No nested bullet points deeper than 2 levels**

---

## 8. HOW TO GENERATE NOTES FROM SOURCE MATERIAL

When the user provides a new article, screenshot, or PDF from GreatFrontend:

### Step 1 — Identify what type of content it is

|Source content|Note type|Folder|Naming|
|---|---|---|---|
|Introduction / overview article|Intro note (6.2)|`01 - Guidebook/`|`01 - FE SD - Introduction.md`|
|Types of questions article|Question types note|`01 - Guidebook/`|`02 - FE SD - Types of Questions.md`|
|Framework explanation|Framework note (6.3)|`01 - Guidebook/`|`03 - RADIO Framework.md`|
|Evaluation / scoring criteria|Eval axes note|`01 - Guidebook/`|`04 - FE SD - Evaluation Axes.md`|
|Common mistakes|Mistakes note|`01 - Guidebook/`|`05 - FE SD - Common Mistakes.md`|
|Cheatsheet|Cheatsheet note|`01 - Guidebook/`|`06 - FE SD - Cheatsheet.md`|
|A specific system to design|Case study note (6.5)|`03 - Case Studies/`|`Case Study - [Name].md`|
|A technical concept|Concept note (6.4)|`02 - Core Concepts/`|`[Concept Name].md`|

### Step 2 — Extract these elements from the source

- **Main topic** → note title and H2 sections
- **Key facts, rules, patterns** → bullet points and tables
- **Code examples or APIs** → code blocks
- **Comparisons** (X vs Y) → tables
- **Decisions** (when to use X) → decision trees or if/then tables
- **Things to remember** (interview tips) → `> 💡` callouts
- **Related concepts mentioned** → wikilinks inline

### Step 3 — Apply the correct template (section 6)

### Step 4 — Add all wikilinks

- Backlink to MOC
- Backlink to source note (Introduced in / Source)
- Forward links to every concept mentioned
- For case studies: "Concepts used in this case study" section at the bottom

### Step 5 — Add tags (section 4)

### Step 6 — If this note is a case study, update existing concept notes

Add the case study to the "Used in these case studies" section of every concept it links to. This keeps the graph bidirectional.

---

## 9. GRAPH DESIGN INTENT

The Obsidian graph should visually show these relationships:

```
FE SD - MOC (center hub)
    │
    ├── RADIO Framework
    │       ├── Rendering Strategies
    │       ├── State Management
    │       ├── Networking & APIs
    │       ├── Performance Optimization
    │       ├── Caching Strategies
    │       └── Accessibility (A11y)
    │
    ├── FE SD Question Types
    │       ├── [links to all case studies]
    │       └── [links to concept notes]
    │
    ├── Case Studies (cluster)
    │       ├── Case Study - Facebook News Feed ──► Performance, State, Networking
    │       ├── Case Study - Google Docs ──────────► Networking (WS), State, A11y
    │       ├── Case Study - Messenger ────────────► Networking (WS), State
    │       ├── Case Study - Netflix ──────────────► Performance, Networking (streaming)
    │       ├── Case Study - Airbnb SEO ───────────► Rendering (SSR), Performance
    │       ├── Case Study - Amazon ───────────────► Performance, Caching, Rendering
    │       ├── Case Study - Instagram Upload ──────► Performance, Networking
    │       ├── Case Study - Dropdown ─────────────► A11y, Component Architecture
    │       ├── Case Study - Modal ────────────────► A11y, Component Architecture
    │       └── Case Study - Image Carousel ────────► A11y, Performance
    │
    └── Core Concepts (satellite cluster)
            ├── Rendering Strategies
            ├── State Management
            ├── Networking & APIs
            ├── Performance Optimization ── (most-linked node)
            ├── Caching Strategies
            ├── Accessibility (A11y)
            ├── Component Architecture
            └── Internationalization (i18n)
```

**Performance Optimization** should be the most-linked node — virtually every case study and the RADIO framework reference it.

---

## 10. EXISTING NOTE SUMMARIES (for context reconstruction)

### FE SD - MOC

Central hub. Lists all notes under: Start Here, Core Topics, Core Concepts, Case Studies, Tags. Every other note links back to this.

### 01 - FE SD - Introduction

Source: GreatFrontend intro article. Author: Yangshun Tay. Covers: what FE SD interviews are, why they're hard, why SD matters at senior level, the guide structure (Question Types → RADIO → Eval Axes → Common Mistakes → Case Studies), and the list of case studies in the guide.

### FE vs BE System Design

The exact comparison table from the GreatFrontend intro image. 7 rows: Requirements, Architecture (distributed vs client-side components), Capacity estimation (BE may need it, FE usually not), Data model (schema vs app state), Infrastructure (client vs server is black box), API types (gRPC/HTTP distributed vs component events + REST), Deep dives (SRAC for BE vs Performance/UX/A11y/i18n for FE). Includes the classic Facebook News Feed example showing how the same question differs.

### RADIO Framework

**Critical nuance:** RADIO is a checklist, NOT a rigid linear sequence. Backtrack freely. Don't force it on narrow questions. Write "RADIO" on the whiteboard to track coverage.

R: functional vs non-functional requirements (defined + distinguished). Preferred approach = take initiative to list requirements yourself, get alignment. Core questions: features to focus on, core vs good-to-have, devices, offline, perf, SEO, a11y. Write down agreed requirements.

A: 4 layers (NOT 5): **Server** (black box), **View layer** (presentation + local state only), **Store/Model layer** (cross-cutting data, Redux/Zustand/Jotai/MobX, unidirectional flow), **Data access layer** (React Query/tRPC/Apollo — fetching, caching, error management; only layer affected by offline storage). Not every layer needed for every product. Also covers: separation of concerns, where computation happens (client vs server trade-off), verbally describe each box after drawing, News Feed component responsibilities table. Tools: Excalidraw, diagrams.net.

D: Server-originated data vs Client-only data. Client-only further splits into: Data to be persisted (sent to server eventually) vs Ephemeral data (OK to lose on tab close). Present as a table: Source | Entity | Belongs to | Fields. Iterative process — add fields as requirements evolve. List fields under the component that owns them in the architecture diagram.

I: Every API has 3 parts: Name/functionality, Parameters, Return value. Three interface types: (1) Server↔Client — 6 protocols: HTTP/REST (default), WebSockets (bidirectional real-time), SSE (server→client only), Long polling (fallback, rarely used now), GraphQL (flexible queries, unlikely needed in interviews), WebRTC (P2P media, very specific). Full News Feed GET /feed JSON example with cursor pagination. (2) Client↔Client — 3 patterns: Props+callbacks (foundational), Store dispatch (central store, actions have name+payload), Pub/sub event listeners (decoupled, most prevalent in browser). (3) UI Component props — 5 categories: Data props, Event/Callback props, Configuration/Behavior props, Styling/Presentation props, Render/Slot props. Only spend time on component API if the question is specifically about a component.

O: 2 guiding principles: (1) Focus on unique/important areas for this product. (2) Showcase your strengths. Available areas: Performance, Networking, UX, A11y, SEO, i18n, Multi-device, Security. CRITICAL — what to AVOID: JS framework debates, CSS framework choices, generic perf advice (unless core to problem), logging/analytics/monitoring, DevOps/CI/CD details, build tooling. Exception: mention framework only when it changes architectural trade-offs (e.g. SSR/SSG strategy, CDN/edge). Summary table. RADIO applied to News Feed with full corrected architecture (Data access layer → Store → Feed UI).

### FE SD Question Types

Two categories: Applications (16 types in table: News Feed, Messaging, E-commerce, Photo sharing, Travel, Video streaming, Pinterest, Collaborative, Email, Drawing, Maps, File storage, Video conf, Ridesharing, Music streaming, Games — each with companies, important features, important topics). UI Components: what to design (hierarchy, state, entry points), 4 focus areas, list of ~8 component examples, customizing theming section, RADIO applied per type table.

### FE SD Evaluation Axes

7 axes: 1. Problem Clarification, 2. System Architecture, 3. Technical Depth, 4. Performance Awareness, 5. Accessibility & Inclusivity, 6. Internationalization, 7. Communication. Each has bullet points of what the interviewer is checking and wikilinks to relevant notes.

### FE SD Common Mistakes

7 mistakes in What/Why/Fix format: 1. Skipping requirements, 2. Treating FE SD like BE SD, 3. No performance discussion, 4. Forgetting accessibility, 5. No API design, 6. One-way communication, 7. No trade-offs.

### _Case Study Template

Blank RADIO-structured template. Sections: Requirements (Functional/Non-functional/Out of scope), Architecture (components + data flow), Data Model (TypeScript types + server vs client), Interface (Server API + Component API), Optimizations (Performance/A11y/Caching/Other), Concepts used (wikilinks).

### Rendering Strategies

CSR/SSR/SSG/ISR comparison table with pros/cons/best-for. Decision tree for which to choose. Hydration explanation and common pitfall (hydration mismatch). Links to Airbnb, Amazon, Facebook case studies.

### State Management

Two types: server state vs client UI state. More granular: URL state, Global UI, Server cache, Local component, Form state. State shape design with TypeScript example (FeedState). Key questions to ask about state. Links to 3 case studies.

### Caching Strategies

5 layers: CDN, HTTP cache, Service Worker, In-memory, localStorage/IndexedDB. Cache-Control headers with examples. Service Worker patterns (cache-first, network-first, stale-while-revalidate). React Query code example. Links to Amazon, Airbnb, Facebook case studies.

### Performance Optimization

Core Web Vitals table: LCP (<2.5s), INP (<200ms), CLS (<0.1) — note: INP replaced FID in March 2024. Loading techniques: code splitting, lazy loading, prefetch/preload, tree shaking, image optimization (WebP/AVIF, srcset). Runtime: list virtualization (react-virtual, react-window), memoization (React.memo, useMemo, useCallback), debounce vs throttle. Network performance. Rendering link. Links to 5 case studies.

### Networking and APIs

Protocol table: HTTP/REST, GraphQL, WebSockets, SSE, Long polling with when-to-use. REST API design rules (nouns not verbs, cursor-based pagination). WebSockets vs SSE comparison table. Optimistic updates pattern with code (dispatch → API call → rollback on error). Error handling patterns. Links to 4 case studies.

### Accessibility (A11y)

POUR principles table. Keyboard navigation checklist (7 items). ARIA patterns table for 6 components (Modal, Dropdown, Autocomplete, Tabs, Alert, Image). Focus management for modals and SPAs. Quick wins list (5 items). Links to 4 case studies.

---

## 11. WHEN USER PROVIDES NEW SOURCE MATERIAL

Do this in order:

1. Read all content from the source (image/PDF/URL)
2. Identify which note(s) to create or update
3. Check the File Registry (section 3) — is this a STUB being filled or a new note?
4. Apply the correct template from section 6
5. Add all wikilinks (section 5)
6. Add correct tags (section 4)
7. Follow formatting rules (section 7)
8. Output all files with their exact folder paths
9. If a case study was created, also update the "Used in" section of relevant concept notes

**Output format:** Create files at the correct paths. Always state the complete path, e.g.:

- Guidebook note: `01 - Guidebook/03 - RADIO Framework.md`
- Core concept: `02 - Core Concepts/Rendering Strategies.md`
- Case study: `03 - Case Studies/Case Study - Facebook News Feed.md`

---

## 12. WHAT TO NEVER DO

- ❌ Never create a flat note without wikilinks back to MOC
- ❌ Never use a concept name in text without linking it `[[Concept Name]]`
- ❌ Never create a case study without the "Concepts used in this case study" section at the bottom
- ❌ Never create a new concept that doesn't list "Used in these case studies"
- ❌ Never use tags in the middle of a note — tags go on line 2 only
- ❌ Never use Obsidian callout syntax (`> [!note]`) — use `> 💡` instead
- ❌ Never use the word "and" in wikilinks where `&` is correct: `[[Networking & APIs]]` not `[[Networking and APIs]]`
- ❌ Never write a case study without TypeScript types in the Data Model section
- ❌ Never write a case study without actual API endpoint examples in the Interface section
- ❌ Never add emoji outside of MOC headers

---

## 13. REGENERATION COMMAND

If an agent needs to regenerate this vault from scratch, create files in this exact order:

```
00 - MOC/
  FE SD - MOC.md

01 - Guidebook/
  01 - FE SD - Introduction.md
  02 - FE SD - Types of Questions.md
  03 - RADIO Framework.md
  04 - FE SD - Evaluation Axes.md
  05 - FE SD - Common Mistakes.md
  06 - FE SD - Cheatsheet.md          ← STUB
  FE vs BE System Design.md

02 - Core Concepts/
  Rendering Strategies.md
  State Management.md
  Caching Strategies.md
  Performance Optimization.md
  Networking and APIs.md
  Accessibility (A11y).md
  Component Architecture.md           ← STUB
  Internationalization (i18n).md      ← STUB

03 - Case Studies/
  _Case Study Template.md
  Case Study - Facebook News Feed.md
  Case Study - Autocomplete.md
  [remaining stubs as listed in section 3]

CLAUDE.md                             ← vault root
```

Use section 10 (summaries) as content reference. Use section 6 (templates) for structure. Use section 5 for wikilinks. Use section 4 for tags.

---

_Last updated: Folder structure refactored — 7 folders → 4 folders. `01 - Intro`, `02 - Framework`, `03 - Question Types`, `04 - Eval & Mistakes` consolidated into `01 - Guidebook`. `05 - Case Studies` → `03 - Case Studies`. `06 - Core Concepts` → `02 - Core Concepts`. Guidebook files now carry order-number prefixes (01–06) to match GreatFrontend sidebar sequence._ _Total notes: 14 filled + FE SD Cheatsheet (stub) + 2 concept stubs + 9 case study stubs._