# SaaS Templates

![License](https://img.shields.io/badge/License-MIT-green.svg)
![HTML](https://img.shields.io/badge/HTML-5-orange)
![CSS](https://img.shields.io/badge/CSS-3-blue)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow)

A collection of modern, lightweight, and responsive **HTML, CSS, and JavaScript templates** for local businesses and simple SaaS landing pages.

These templates are completely static, making them easy to customize, deploy, and extend into larger projects. Whether you're building a landing page for a restaurant, salon, startup, dealership, or service business, this repository provides a clean starting point.

---

## ✨ Features

* 📱 Responsive design
* ⚡ Pure HTML, CSS & JavaScript
* 🎨 Easy to customize
* 📄 SEO-ready
* 📂 Data-driven configuration
* 💬 WhatsApp booking flow
* 🖼️ Dynamic gallery & testimonials
* 🚀 Deploy anywhere (GitHub Pages, Netlify, Vercel, Render, etc.)
* 🔓 MIT Licensed

---

# Repository Structure

```
Saas-templates/
│
├── README.md
├── LICENSE
│
└── SupaTemplate/
    ├── index.html
    ├── style.css
    ├── script.js
    ├── config.json
    ├── robots.txt
    ├── sitemap.xml
    └── assets/
```

---

# Included Template

## SupaTemplate

A complete, production-ready landing page template designed for:

* Restaurants
* Cafés
* Salons
* Barbershops
* Car dealerships
* Gyms
* Local stores
* Repair services
* SaaS startups
* Small businesses

The template is powered by a simple `config.json` file, allowing non-developers to update content without touching the HTML.

---

# Quick Start

## 1. Clone the repository

```bash
git clone https://github.com/owenndeule/Saas-templates.git
```

```bash
cd Saas-templates
```

---

## 2. Run locally

### Option 1 — Open directly

Open:

```
SupaTemplate/index.html
```

in your browser.

> **Note:** Some features (like loading `config.json`) require a local web server.

---

### Option 2 — Python

```bash
python3 -m http.server 8000
```

Open:

```
http://localhost:8000/SupaTemplate/
```

---

### Option 3 — Node.js

```bash
npx http-server -c-1 . -p 8000
```

Then visit:

```
http://localhost:8000/SupaTemplate/
```

---

# Customization

## Business Information

Edit:

```
SupaTemplate/config.json
```

You can change:

* Business name
* Tagline
* Phone number
* Email
* Address
* Opening hours
* Hero image
* Gallery
* Testimonials
* Menu
* Social media links
* Booking settings

No HTML editing is required for most content changes.

---

## Branding

Open:

```
style.css
```

Update the CSS variables inside `:root`.

Example:

```css
:root {
  --primary-color: #4f46e5;
  --accent-color: #f97316;
}
```

You can completely rebrand the template in just a few minutes.

---

## Images

Replace image URLs inside:

```
config.json
```

or store images locally inside:

```
SupaTemplate/assets/
```

---

## Fonts

Google Fonts are loaded inside:

```
index.html
```

Replace them with any font you prefer.

---

## Forms

The template currently uses:

* WhatsApp booking
* Simple contact form

You can easily integrate services such as:

* EmailJS
* Formspree
* Firebase
* Supabase
* Your own backend API

The integration points are documented inside:

```
script.js
```

---

# Developer Notes

The project intentionally has:

* No framework
* No build tools
* No dependencies
* No package manager
* No bundler

Everything works with plain HTML, CSS, and JavaScript.

Because `config.json` is loaded using `fetch()`, serving the project over HTTP is recommended instead of opening the files directly.

---

# Deployment

This project can be deployed to any static hosting provider, including:

* GitHub Pages
* Netlify
* Vercel
* Cloudflare Pages
* Render (Static Sites)
* Firebase Hosting
* Surge.sh

No build process is required.

---

# Contributing

Contributions are welcome.

Ideas include:

* New templates
* Bug fixes
* Performance improvements
* Accessibility improvements
* Additional business categories
* Better animations
* New components

1. Fork the repository.
2. Create a feature branch.

```bash
git checkout -b feature/new-template
```

3. Commit your changes.

```bash
git commit -m "Add new restaurant template"
```

4. Push the branch.

```bash
git push origin feature/new-template
```

5. Open a Pull Request.

---

# Roadmap

Future templates planned:

* SaaS Dashboard
* Agency Landing Page
* Portfolio
* Hotel Website
* Medical Clinic
* School Website
* E-commerce Landing Page
* Construction Company
* Church Website
* Event Landing Page

---

# License

This project is licensed under the **MIT License**.

You are free to:

* Use
* Modify
* Distribute
* Sell
* Include in commercial projects

Please include the original copyright notice when redistributing.

See the **LICENSE** file for the full license text.

---

# Author

**Owen Ndeule**

* GitHub: https://github.com/owenndeule

If you find this project useful, consider giving the repository a ⭐ to support future template development.
