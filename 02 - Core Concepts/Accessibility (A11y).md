# Accessibility (A11y)

#concept #to-revise Back to: [[FE SD - MOC]] Used in: [[03 - RADIO Framework]] → O step, [[Case Study - Autocomplete]]

---

## Why it matters in interviews

Accessibility is an **explicit evaluation axis** in FE system design. See [[04 - FE SD - Evaluation Axes]]. Not mentioning a11y for a component question is a red flag.

---

## The 4 POUR principles (WCAG)

|Principle|Meaning|
|---|---|
|**Perceivable**|Users can perceive all content (alt text, captions, contrast)|
|**Operable**|Users can operate all UI with keyboard/assistive tech|
|**Understandable**|Content and UI is clear and predictable|
|**Robust**|Works with current and future assistive technologies|

---

## Keyboard navigation checklist

For any interactive component:

- [ ] All interactive elements are focusable (`tabindex`)
- [ ] Focus order is logical (top-to-bottom, left-to-right)
- [ ] Focus is visible (`:focus-visible` styles)
- [ ] Keyboard shortcuts where applicable (Escape to close modal, Arrow keys in dropdown)
- [ ] No keyboard traps (except modals — focus SHOULD be trapped in modals)

---

## Common ARIA patterns

|Component|Key ARIA attributes|
|---|---|
|**Modal/Dialog**|`role="dialog"`, `aria-modal="true"`, `aria-labelledby`, focus trap|
|**Dropdown/Menu**|`role="menu"`, `role="menuitem"`, `aria-expanded`, `aria-haspopup`|
|**Autocomplete**|`role="combobox"`, `aria-autocomplete`, `aria-expanded`, `aria-owns`|
|**Tabs**|`role="tablist"`, `role="tab"`, `role="tabpanel"`, `aria-selected`|
|**Alert/Toast**|`role="alert"` or `aria-live="polite"`|
|**Image**|`alt="descriptive text"` (or `alt=""` if decorative)|

---

## Focus management

Especially important for:

- **Modals** — when opened, move focus into modal. When closed, return focus to trigger element
- **Toast notifications** — announce via `aria-live`
- **Route changes** (SPA) — announce new page to screen readers

---

## Quick wins to mention in interviews

1. Semantic HTML — use `<button>` not `<div onclick>`, `<nav>`, `<main>`, `<header>`
2. Skip links — allow keyboard users to skip navigation
3. Sufficient color contrast — 4.5:1 ratio for text
4. Don't rely on color alone to convey information
5. `prefers-reduced-motion` — disable animations for users who prefer it

---

## Used in these case studies

- [[Case Study - Dropdown Menu Component]] — keyboard nav, ARIA menu role
- [[Case Study - Modal Dialog Component]] — focus trap, ARIA dialog
- [[Case Study - Image Carousel Component]] — ARIA live region, keyboard arrows
- [[Case Study - News Feed (e.g. Facebook)]] — feed announcements, button labels