# Saas-templates

A set of minimal, static HTML/CSS/JS starter templates for local small businesses and simple SaaS-style landing pages. The repo includes a complete, ready-to-use template (SupaTemplate) that you can drop into any static host, edit in-place, or use as a starting point for a more advanced project.

This project is free to use and open — feel free to copy, adapt, and redistribute. By default this README declares the project available under the MIT License (see the LICENSE section below). Use at your own risk; no warranty is provided.

---

## What you get

- SupaTemplate/ — a complete static site template (HTML, CSS, JS, config.json, robots/sitemap). It targets small local businesses (restaurants, salons, shops, car dealerships, etc.).
  - index.html — the page markup and content placeholders
  - style.css — theme variables and styles (rebrand by changing CSS variables)
  - script.js — client-side logic: loads config.json, renders menu/gallery/testimonials, booking flow (WhatsApp-first), lightbox, and simple form handling
  - config.json — data-driven site configuration (business name, contact, menu/gallery data)
  - robots.txt, sitemap.xml — SEO basics

## Quick start — open the template locally

1. Clone the repository:

   git clone https://github.com/owenndeule/Saas-templates.git

2. Serve the files from the SupaTemplate folder. The simplest options:

   - Open SupaTemplate/index.html directly in your browser (works for basic testing)

   - Start a temporary local server from the repo root (recommended so fetch() calls for config.json work):

     # Python 3 (from the repo root)
     python3 -m http.server 8000

     # or using Node (http-server)
     npx http-server -c-1 . -p 8000

   Then open http://localhost:8000/SupaTemplate/ in your browser.

## How to customize

The template is intentionally data-driven. Most changes happen in SupaTemplate/config.json and a few spots in the HTML/CSS.

- Business details and content
  - Edit SupaTemplate/config.json to change businessName, tagline, phoneNumber, email, address, gallery, menuData, testimonials, social links, heroImage, etc.
  - script.js reads config.json at load-time and injects content into index.html.

- Images
  - Replace hero and gallery image URLs in config.json (or point them to local files inside the SupaTemplate directory).
  - Replace any placeholder images or the logo in index.html if you prefer an inline asset.

- Colors & fonts
  - Edit the CSS variables in SupaTemplate/style.css (:root) to rebrand colors quickly — --primary-color and --accent-color are the main ones.
  - Fonts are loaded via the Google Fonts link in index.html; swap them there if needed.

- Forms and integrations
  - The reservation and contact forms are client-side and currently trigger a WhatsApp flow or a simple alert. Integrate with your backend or a service like EmailJS/Formspree inside script.js (see comments near handleBookingSubmit and handleContactSubmit).

- Behavior
  - The hero CTA and many "Book" buttons will either open a booking modal or send users to WhatsApp depending on the businessType in config.json.
  - To change that logic, edit the conditional lists near initializeBookingModal and applyConfig in script.js.

## Notes for developers

- The app is static (no build step required). JavaScript loads SupaTemplate/config.json with fetch; serving files over HTTP is recommended so CORS/fetch works reliably.
- The templates are intentionally unopinionated — you can convert the static site into a Next.js/React/Vue app, or plug it into a backend for dynamic data.
- Accessibility: basic landmarks and aria attributes are present, but please audit before production usage.

## Contributing

If you improve the template (bug fixes, new business types, extra templates), feel free to open a PR or copy the repo and share your version. Keep the notices if you redistribute derivatives.

## License (permissive)

This repository is provided under the MIT License — feel free to use, copy, modify, and redistribute this code in personal or commercial projects. No warranty is provided.

```
MIT License

Copyright (c) 2026 OwennDeule

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

If you'd like, I can add a LICENSE file to the repository with the full MIT text and commit it for you.