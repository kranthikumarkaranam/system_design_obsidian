#source/greatfrontend #guide 

Source: [Types of Front End System Design Questions](https://www.greatfrontend.com/front-end-system-design-playbook/types-of-questions)
Back to: [[FE SD - MOC]] 

---

## Two main categories

There are **two** categories of FE system design questions:

1. **Applications** (~10 question types)
2. **UI Components** (~21 question types)

---

## Category 1 — Applications

Designing applications for FE system design feels similar to BE/FS system design but with key differences:

- Less talking about **distributed infrastructure** at a high level
- More focus on **page rendering, navigation, and interaction**
- More emphasis on **communication protocols within the client**
- More time on **real-time communication** and how it affects design

> 💡 Application performance directly affects the business. E.g. SEO for e-commerce has direct impact on sales, so it's often a priority interview topic.

### Important areas — Application Design

|Application|Companies|Important features|Important topics|
|---|---|---|---|
|**News feed**|Facebook, Twitter|Feed list, Feed items, Feed composer|Pagination types, [[Performance Optimization]]|
|**Messaging/Chat**|Messenger, Slack, Discord|Real-time messaging, Threads|Real-time comm, [[Networking & APIs]]|
|**E-commerce**|Amazon, eBay|Product listing, Product detail, Cart & checkout|[[Performance Optimization]]|
|**Photo sharing**|Instagram, Flickr, Google Photos|Photos listing, Photos editing|Media implementation|
|**Travel booking**|Airbnb, Booking.com|Search UI, Search results, Booking|SEO, [[Performance Optimization]]|
|**Video streaming**|Netflix, YouTube|Video player, Playlists|Streaming, [[Networking & APIs]]|
|**Pinterest**|Pinterest|Masonry layout|Media optimizations|
|**Collaborative apps**|Google Docs/Sheets/Slides, Figma|Real-time editing|Real-time comm, Conflict resolution, State syncing|
|**Email client**|Outlook, Apple Mail|Mailbox sorting, Email on email|App state, Offline mode|
|**Drawing**|Figma, Excalidraw|Canvas, Smart select, State management|Canvas rendering, Implementation|
|**Maps**|Google Maps, Apple Maps|Map rendering, Map controls|Map rendering, [[Performance Optimization]]|
|**File storage**|Google Drive, Dropbox|File uploading, File previewing|Uploading (chunked)|
|**Video conferencing**|Zoom, Google Meet|Video streaming, Meeting features|Video streaming, P2P|
|**Ridesharing**|Uber, Lyft|Trip booking, Driver location|App state|
|**Music streaming**|Spotify, Apple Music|Audio streaming, Music player, Downloads|Media streaming, App state|
|**Games**|Tetris, Snake|Game data, Same data|Same as frontend|

---

## Category 2 — UI Components

It is very common to use component libraries to build apps. Some popular ones: React, Material UI, Bootstrap, Ant Design.

UI components can be small (text, button, badge) or much more complex with significant behavior, visual, and accessibility requirements.

> 💡 Knowing how to build components from scratch makes you a better developer — even if you'd use a library in production.

### What to design for a UI component

You will usually be expected to:

1. Describe the **component hierarchy** (subcomponents)
2. Describe the **shape of the component state**
3. Describe the **entry points** — how the component accepts data

For example, an image carousel would need: current image state, pagination buttons, thumbnail list, and an entry point to receive image URLs.

### Component design: 4 focus areas

|Area|What to cover|
|---|---|
|**External API**|Props, events, callbacks — what does the consumer of this component interact with?|
|**Subcomponents**|Break down the component into smaller pieces|
|**Performance**|Virtualization, lazy loading images, memoization|
|**[[Accessibility (A11y)]]**|Keyboard nav, ARIA roles, focus management, screen readers|

### Examples of UI components in FE SD interviews

- Design an **autocomplete / typeahead component**
- Design a **dropdown component** → [[Case Study - Dropdown Menu Component]]
- Design an **image carousel** → [[Case Study - Image Carousel Component]]
- Design a **modal / dialog** → [[Case Study - Modal Dialog Component]]
- Design a **slider**
- Design a **data table with sorting and pagination**
- Design a **multiselect component**
- Design a **notification / toast component**

### Customising theming

You will often be asked to design a way for users of the component to **customise appearance**. Consider:

- CSS custom properties (variables)
- Theme tokens / design tokens
- Render props / slot patterns
  
> Refer to [Front End Interview Guidebook's UI Components API Design Principles Section](https://www.greatfrontend.com/front-end-interview-guidebook/user-interface-components-api-design-principles) for an overview and comparison of the different approaches.


---

## Applying RADIO to each type

| RADIO step | Application question              | UI Component question               |
| ---------- | --------------------------------- | ----------------------------------- |
| R          | Functional features + perf/scale  | Interactions, a11y, mobile/desktop? |
| A          | Full client architecture          | Component hierarchy diagram         |
| D          | Server state + client state shape | Component state shape only          |
| I          | REST/GraphQL/WebSocket API design | Props, events, hooks API            |
| O          | Perf, caching, SEO, i18n, a11y    | A11y, theming, edge cases           |

See: [[03 - RADIO Framework]]