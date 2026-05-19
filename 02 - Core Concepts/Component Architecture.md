# Component Architecture

#concept #to-revise Back to: [[FE SD - MOC]] Used in: [[03 - RADIO Framework]] → Architecture step

---

## What is Component Architecture?

Component architecture is how you decompose a UI system into discrete, well-scoped pieces with clear responsibilities and defined interfaces between them. In FE system design, good architecture means the interviewer can understand your system at a glance and you can extend it without rewriting the whole thing.

The central question: **who owns what state, and how do components talk to each other?**

---

## The MVC / Controller Pattern

The most reliable pattern for complex UI components in FE system design is **Model-View-Controller (MVC)**, applied to the front end:

|Layer|Role|Example (Autocomplete)|
|---|---|---|
|View|Renders UI; no logic|Input UI, Results UI (popup)|
|Controller|"Brain" — owns state, routes data, coordinates components|`AutocompleteController`|
|Model / Cache|Holds data; no UI|In-memory result cache|

**Why a central controller?** Race conditions, stale state, and loading indicators all need a single source of truth. If Input UI and Results UI both hold state, they can disagree. A controller that all components talk to removes this.

```
            ┌──────────────────────────────────────┐
            │        Component Boundary             │
            │                                      │
  User ───► │  View ──► Controller ──► View        │
            │              │                       │
            │           Cache ◄──► Server          │
            │                                      │
            └──────────────────────────────────────┘
```

---

## State Ownership Rules

A well-architected component separates state into two buckets:

|State type|Lives in|Examples|
|---|---|---|
|Transient UI state|Controller|`isOpen`, `isLoading`, `activeIndex`, `input`|
|Persistent data|Cache / Store|Query results, fetched entities, timestamps|

> 💡 If state is purely visual and ephemeral (changes on every keystroke, cleared on navigation) → controller. If state represents fetched data that could be reused across interactions → cache/store.

---

## Rendering Customisation — Three Approaches

When building a generic/reusable component, you need to let consumers customise rendering. Three options in increasing flexibility:

|Approach|How|Flexibility|Effort|
|---|---|---|---|
|Theming object|`themeOptions: { fontSize: '12px', color: 'red' }`|Low|Low|
|Class names|`classNames: { container: 'my-class' }`|Medium|Medium|
|Render function|`renderItem: (result) => <MyCustomRow />`|High|High|

**Render function (inversion of control)** is the most powerful: the component calls your function with data; you control the entire output. Use this as your answer for "how would you make the rendering customisable?"

```typescript
// Inversion of control example
type Props = {
  renderItem?: (result: Result) => React.ReactNode
}

// Inside component:
results.map(result =>
  props.renderItem ? props.renderItem(result) : <DefaultRow result={result} />
)
```

---

## Component Hierarchy Design

When decomposing a UI into components, ask:

1. **Responsibility** — does each component do exactly one thing?
2. **Data flow** — is data flowing in one direction (top-down from controller)?
3. **Coupling** — can you replace a View without touching the Controller?
4. **Entry points** — where does the component attach to the host page? (portal for popups)

For popup components (Autocomplete, Dropdown, Modal, Tooltip): render the popup via a **portal** so it escapes `overflow: hidden` containers and stacking context issues.

---

## Used in These Case Studies

- [[Case Study - Autocomplete]] — MVC controller as single source of truth; cache as model layer; `renderItem` inversion of control
- [[Case Study - Dropdown Menu Component]] — similar controller pattern; trigger vs popup separation
- [[Case Study - Modal Dialog Component]] — controller manages open/close state; portal rendering