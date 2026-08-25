# Memory: architecture (Static Site Tree & Hygiene Rules)

Defines file structure and component patterns for 100% static hosting.

---

## 📁 Standard Static Site Layout

```
project-root/
├── index.html                   # Primary entry point
├── about.html                   # Content pages
├── contact.html
├── css/
│   ├── style.css                # Master stylesheet / tokens
│   └── reset.css                # CSS reset
├── js/
│   ├── main.js                  # ES Module entry point
│   └── components/              # Web Components (custom elements)
│       ├── site-header.js
│       └── site-footer.js
├── data/                        # JSON / Markdown content stores
│   └── content.json
└── assets/                      # Optimized SVGs, icons, and WebP media
```

---

## 🧩 Web Component Pattern (Zero Build Partials)

```javascript
class SiteHeader extends HTMLElement {
  connectedCallback() {
    this.innerHTML = `
      <header class="site-header">
        <nav class="nav-container">
          <a href="./index.html" class="logo">Brand</a>
          <ul class="nav-links">
            <li><a href="./index.html">Home</a></li>
            <li><a href="./about.html">About</a></li>
            <li><a href="./contact.html">Contact</a></li>
          </ul>
        </nav>
      </header>
    `;
  }
}
customElements.define('site-header', SiteHeader);
```
