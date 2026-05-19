#source/greatfrontend #guide 

Introduced in: [[01 - FE SD - Introduction]]
Back to: [[FE SD - MOC]] 

---

## The core difference

In traditional BE system design, you architect a **distributed system** — servers, API gateways, load balancers, caches, databases, microservices, message queues.

In FE system design, the emphasis shifts to the **client** — what happens inside the browser/app, how components are structured, how state flows, and how the API surface between client and server is designed.

> 💡 In FE interviews, the server is often treated as a **black box** you can call. Your job is to design what's on the other side.

---

## Comparison Table

| Aspect                                       | Back End / Full Stack                                                                                                        | Front End                                                                                   |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Gather requirements**                      | Required                                                                                                                     | Required                                                                                    |
| **Architecture / High-level entities**       | Distributed cloud services: Load balancer, App server, Database, File storage, Caches, Message queues, CDN, Full-text search | Components within the **client**: View layer, Store (state), Networking layer               |
| **Back-of-the-envelope capacity estimation** | May be required                                                                                                              | Usually NOT required                                                                        |
| **Data model**                               | Database schema                                                                                                              | **Application state** (what lives in memory/store)                                          |
| **I (Infrastructure — less important)**      | Client (treat as black box)                                                                                                  | Server (treat as black box)                                                                 |
| **Type of APIs between components**          | Between distributed services: HTTP, gRPC, etc.                                                                               | Between server and client (HTTP, docs), Events / actions between **client-side components** |
| **Deep dives / focus areas**                 | Scalability, Reliability, Consistency, Availability                                                                          | **Performance**, User Experience, **Accessibility**, **Internationalization**               |

---

## What FE interviews DO focus on

- [[Rendering Strategies]] — SSR vs CSR vs SSG, when to use each
- [[Component Architecture]] — How to structure UI into reusable pieces
- [[State Management]] — Where state lives, how it flows
- [[Networking & APIs]] — What API shape does the component need?
- [[Performance Optimization]] — LCP, FID, CLS, lazy loading, code splitting
- [[Accessibility (A11y)]] — Keyboard nav, ARIA, screen readers
- [[Internationalization (i18n)]] — RTL support, locale-aware formatting
- [[Caching Strategies]] — HTTP cache headers, service workers, CDN

## What FE interviews mostly SKIP

- Server scaling (auto-scaling groups, horizontal scaling)
- Back-of-the-envelope: QPS, storage math, bandwidth calc
- Database replication, sharding
- Message queue internals

---

## Classic example: "Design the Facebook News Feed"

The same question has two very different answers:

**BE / Full stack answer:** Capacity estimation, fan-out writes vs reads, database sharding, CDN for images, Kafka for events, caching user feeds...

**FE answer:** How to fetch and render the feed (pagination vs infinite scroll), optimistic updates when liking, virtualized list for performance, skeleton loaders, accessibility of the feed items, offline support, image lazy loading...

See: [[Case Study - News Feed (e.g. Facebook)]]