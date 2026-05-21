> 💡 Entity ranges prevent storing unsafe HTML, but rendering user content is still dangerous.

User-generated content can contain:

- text
- links
- mentions
- captions

All are potential attack vectors.

---

### 1. Output encode user text

Problem:

User submits:

```html
Hello <script>alert("Hacked")</script>
```

Safe:

```jsx
<div>{text}</div>
```

React escapes automatically:

```html
&lt;script&gt;
```

Browser shows text instead of executing it.

Danger:

```jsx
<div dangerouslySetInnerHTML={{__html:text}} />
```

This renders raw HTML and can execute scripts.

✅ Default rule:

- Use framework text interpolation
- Avoid `dangerouslySetInnerHTML`
- If HTML is required → sanitize with DOMPurify

---

### 2. Validate URL schemes

Problem:

Attacker submits:

```html
<a href="javascript:stealData()">
```

User clicks → JavaScript executes.

Safe allowlist:

```txt
http:
https:
mailto:
```

Reject:

```txt
javascript:
data:
vbscript:
```

Validate at render time too, not only submission time.

> Submission validation can be bypassed. Rendering checks are the final defense.

---

### 3. Secure external links

Opening:

```html
<a target="_blank">
```

creates:

```js
window.opener
```

Malicious tab can modify the original page.

Fix:

```html
<a
 target="_blank"
 rel="noopener noreferrer"
>
```

Prevents tab-nabbing attacks.

---

### 4. Content Security Policy (CSP)

CSP = browser security rules.

Example:

```txt
default-src 'self'
script-src 'self'
img-src cdn.myapp.com
```

Meaning:

- scripts only from our site
- images only from our CDN

Even if malicious code reaches the page, browser blocks disallowed resources.

CSP = last line of defense.

---

### Quick interview summary

```txt
Never store HTML
        ↓
Escape output
        ↓
Validate URLs
        ↓
Use noopener+noreferrer
        ↓
Add CSP
```