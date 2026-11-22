# SaaS Templates

![License](https://img.shields.io/badge/License-MIT-green.svg)
![HTML](https://img.shields.io/badge/HTML-5-orange)
![CSS](https://img.shields.io/badge/CSS-3-blue)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

A collection of modern, lightweight, and responsive **HTML, CSS, and JavaScript templates** for local businesses and simple SaaS landing pages.

These templates are completely static, making them easy to customize, deploy, and extend into larger projects. Whether you're building a landing page for a restaurant, salon, startup, dealership, or service business, this repository provides a clean starting point.

---

## 🎯 Vision & Goals

This project aims to be the go-to resource for developers and small business owners who need production-ready, customizable website templates without the complexity of frameworks, build tools, or dependencies.

**Our goals:**
- Provide **zero-dependency** templates that work everywhere
- Enable **configuration over code** — customize via JSON, not HTML
- Support **multiple business types** from a single codebase
- Maintain **accessibility** and **responsive design** as first-class concerns
- Foster a **community** of contributors adding new templates and improvements

---

## 📦 Available Templates

### 1. SupaTemplate — Multi-Business Landing Page
**Location:** `templates/supa-template/`

A single, data-driven template that adapts to 10+ business types through configuration alone.

| Feature | Details |
|---------|---------|
| **Business Types** | Restaurant, Car Dealership, Salon, Spa, Fitness, Car Wash, Pet Care, Home Services, Professional Services, Other |
| **Configuration** | Single `config.json` — no HTML editing needed |
| **Sections** | Hero, New Arrivals, Menu/Services (with tabs), Gallery, Testimonials, Booking Modal, Contact, Footer |
| **Booking** | WhatsApp-first flow with optional modal for appointments |
| **SEO** | Dynamic meta tags, Open Graph, JSON-LD schema, Google Analytics |
| **Images** | Lightbox with swipe/keyboard navigation, multi-image gallery cards |
| **Responsive** | Mobile-first, hamburger menu, touch-friendly |
| **Local Assets** | `assets/` folder for self-hosted images, fonts, files |

**Use cases:** Any local business needing a professional web presence quickly.

---

## 📸 Screenshots

*Screenshots are generated from the actual template using the provided config examples. Run any config locally to see the live result.*

### To Generate Screenshots

1. Start the template with a config example:
   ```bash
   cd templates/supa-template
   cp ../../configs/supa-template/config-restaurant.json config.json
   python -m http.server 8000
   ```

2. Open http://localhost:8000 in browser

3. Use browser dev tools to set viewport:
   - Desktop: 1280px width
   - Mobile: 375px width

4. Take screenshots and save to `screenshots/supa-template/`

See `screenshots/README.md` for detailed naming conventions and automation options.
---

## 📁 Repository Structure

```
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── new_template.md
│   └── PULL_REQUEST_TEMPLATE.md
│
├── configs/
│   └── supa-template/
│       ├── config.json                  # Generic template
│       ├── config-restaurant.json
│       ├── config-car-dealership.json
│       ├── config-salon.json
│       ├── config-spa.json
│       ├── config-fitness.json
│       └── config-real-estate.json
│
├── templates/
│   └── supa-template/
│       ├── index.html           # Main HTML (semantic, accessible)
│       ├── style.css            # CSS with custom properties
│       ├── script.js            # Dynamic rendering engine
│       ├── config.json          # Working example (copy from configs/)
│       ├── assets/              # Local images, fonts, files
│       ├── robots.txt           # Search engine directives
│       ├── sitemap.xml          # Site map template
│       ├── README.md            # Template-specific docs
│       └── LICENSE              # Template license (MIT)
│
├── screenshots/
│   └── supa-template/
│       ├── hero.png
│       ├── features.png
│       ├── contact.png
│       ├── gallery.png
│       ├── testimonials.png
│       ├── footer.png
│       └── mobile.png
│
├── docs/
│   ├── configuration-guide.md   # Deep dive into config.json
│   ├── customization.md         # Advanced customization
│   ├── deployment.md            # Deployment guides
│   └── accessibility.md         # Accessibility checklist
│
├── CONTRIBUTING.md              # Contribution guidelines
├── LICENSE                      # Project license (MIT)
├── README.md                    # This file
└── .gitignore
```
---

## 🚀 Getting Started

### Prerequisites
- A modern web browser
- A local web server (required for `fetch('config.json')` due to CORS)

### Quick Start

**Option A: Command Line (Technical Users)**
```bash
# 1. Clone the repository
git clone https://github.com/owenndeule/Saas-templates.git
cd Saas-templates

# 2. Choose a template
cd templates/supa-template

# 3. Pick a config example (or edit config.json directly)
cp ../../configs/supa-template/config-restaurant.json config.json

# 4. Start a local server
# Python 3
python -m http.server 8000

# Node.js (npx)
npx serve

# PHP
php -S localhost:8000

# 5. Open in browser
# http://localhost:8000
```

**Option B: No Command Line (Non-Technical Users)**
1. **Download** the repository as ZIP from GitHub and extract it
2. **Open** the folder: `templates/supa-template/`
3. **Choose a config**: Go to `configs/supa-template/` and copy one of the config files (e.g., `config-restaurant.json`)
4. **Paste** it into `templates/supa-template/` and **rename** it to `config.json` (replace the existing one)
5. **Start a local server** (required for config to load):
   - **Windows**: Double-click `start-server.bat` (create it with: `python -m http.server 8000`)
   - **Mac/Linux**: Open Terminal in the folder and run `python -m http.server 8000`
   - **VS Code**: Install "Live Server" extension → Right-click `index.html` → "Open with Live Server"
6. **Open** http://localhost:8000 in your browser

### Why a Local Server?
The template loads `config.json` via `fetch()`. Browsers block `fetch()` from `file://` URLs due to CORS policy. A local server serves files over `http://` which allows the fetch to succeed.

---

## 🔧 How the Config System Works

The template uses a **single `config.json` file** in the template root. On page load, JavaScript fetches this file and dynamically renders the entire site.

### Config File Location

```
configs/
└── supa-template/
    ├── config.json                  # Generic template
    ├── config-restaurant.json      — Italian restaurant
    ├── config-car-dealership.json  — Vehicle dealership
    ├── config-salon.json           — Hair & beauty salon
    ├── config-spa.json             — Wellness spa
    ├── config-fitness.json         — Gym & fitness center
    └── config-real-estate.json     — Property listings
```

### Choosing a Configuration

You choose which config to use by **copying the desired example to `config.json`** in the template folder (`templates/supa-template/`).

**Command Line:**
```bash
cd templates/supa-template

# Use a restaurant config
cp ../../configs/supa-template/config-restaurant.json config.json

# Or use a dealership config
cp ../../configs/supa-template/config-car-dealership.json config.json

# Or create your own by editing
cp ../../configs/supa-template/config-restaurant.json config.json
# Then edit config.json with your business details
```

**Without Command Line (File Explorer/Finder):**
1. Open `configs/supa-template/` in your file manager
2. Copy the config you want (e.g., `config-restaurant.json`)
3. Paste it into `templates/supa-template/`
4. Rename the pasted file to `config.json` (replace the existing one)
5. Reload your browser — changes apply instantly

**To Customize:** Open `config.json` in any text editor (Notepad, TextEdit, VS Code) and edit the values:
- `businessName` — Your business name
- `businessType` — One of: `restaurant`, `car dealership`, `salon`, `spa`, `fitness`, `car wash`, `pet care`, `home services`, `professional services`, `other`
- `tagline` — Your tagline
- `primaryColor` — Hex color (e.g., `#2D5016`)
- `whatsappNumber` — Digits only (e.g., `15551234567`)
- `phoneNumber`, `email`, `address` — Your contact info
- `menuData` — Your products/services/prices
- And more — see [Configuration Guide](docs/configuration-guide.md)

### Advanced: Direct Config Fetch (No Copy Needed)

Instead of copying config files, you can **edit the fetch path directly in `templates/supa-template/script.js`** (line 25) to point to any config:

**Default:**
```javascript
const response = await fetch('./config.json');
```

**Point directly to any config in `configs/supa-template/`:**
```javascript
const response = await fetch('../../configs/supa-template/config-restaurant.json');
const response = await fetch('../../configs/supa-template/config-car-dealership.json');
const response = await fetch('../../configs/supa-template/config-salon.json');
const response = await fetch('../../configs/supa-template/config-spa.json');
const response = await fetch('../../configs/supa-template/config-fitness.json');
const response = await fetch('../../configs/supa-template/config-real-estate.json');
const response = await fetch('../../configs/supa-template/config.json');
```

**Benefits:**
- No file copying needed
- Switch configs by changing one line in `script.js`
- Useful for testing multiple configs quickly

**Note:** Requires a local server (CORS blocks `file://` fetches).

### How JavaScript Loads the Config

In `templates/supa-template/script.js`, the config is loaded on `DOMContentLoaded`:

```javascript
document.addEventListener('DOMContentLoaded', async function() {
    const response = await fetch('./config.json');
    const config = await response.json();
    globalConfig = config;
    
    applyConfig(config);
    initializeMenu(config);
    // ... rest of initialization
});
```

**Key points:**
- The template **always** loads `./config.json` from the same directory as `index.html`
- You choose which config to use by copying the desired example to `config.json`
- The `businessType` field in config.json controls all UI behavior (tabs, modals, nav labels, etc.)
- No code changes needed — just swap the JSON file

### Multi-Tenant / SaaS Deployment

For serving different configs per client:

```
yourdomain.com/client-a/     → serves config-a.json
yourdomain.com/client-b/     → serves config-b.json
```

Options:
1. **Subdirectory per client** — Copy template folder, swap `config.json`
2. **Backend API** — Replace `fetch('./config.json')` with `fetch('/api/config?client=xxx')`
3. **Edge function** — Rewrite at CDN level (Cloudflare Workers, Netlify Edge)

---

## ⚙️ Configuration Guide

All customization happens in `config.json`. No HTML/CSS/JS editing required for content changes.

### Core Configuration

```json
{
  "businessName": "Your Business",
  "businessType": "restaurant",
  "tagline": "Your tagline here",
  "primaryColor": "#2D5016",
  "whatsappNumber": "15551234567",
  "currencySymbol": "$",
  "analyticsId": "G-XXXXXXXXXX"
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `businessName` | Yes | Displayed in header, footer, title |
| `businessType` | Yes | Controls UI: `restaurant`, `car dealership`, `salon`, `spa`, `fitness`, `car wash`, `pet care`, `home services`, `professional services`, `other` |
| `tagline` | Yes | Subtitle under business name |
| `primaryColor` | Yes | Hex color — applied to buttons, accents, links |
| `whatsappNumber` | Yes | Country code + number, no `+` (e.g., `15551234567`) |
| `currencySymbol` | No | Prefix for prices (e.g., `$`, `€`, `MWK `) |
| `analyticsId` | No | Google Analytics 4 Measurement ID |

### Content Sections

```json
{
  "testimonials": [
    { "name": "John D.", "comment": "Amazing service!", "stars": 5 }
  ],
  "openingHours": {
    "Monday": "9:00 AM - 6:00 PM",
    "Sunday": "Closed"
  },
  "phoneNumber": "+1 (555) 123-4567",
  "email": "contact@example.com",
  "address": "123 Main St, City, State 12345",
  "mapUrl": "https://www.google.com/maps/embed?...",
  "heroImage": "https://example.com/hero.jpg",
  "gallery": [
    { "name": "Interior", "images": ["https://example.com/img1.jpg"] }
  ]
}
```

### Menu/Services Data (`menuData`)

Structure varies by `businessType`:

**Tabbed categories** (restaurant, car dealership):
```json
"menuData": {
  "Appetizers": [
    { "id": 1, "name": "Bruschetta", "description": "...", "price": "12", "images": ["..."] }
  ],
  "Mains": [ ... ]
}
```

**Flat services** (salon, spa, fitness, other):
```json
"menuData": {
  "Hair Services": [ ... ],
  "Spa Treatments": [ ... ]
}
```

Each item supports:
- `id`, `name`, `description`, `price`, `images[]`
- `badge` — "New", "Popular", "Sale", etc.
- `year`, `mileage`, `fuelType`, `stock` (dealership)
- `duration`, `features[]`, `includes[]` (services/packages)

### Text Overrides (`textOverrides`)

Customize button labels, section titles per business type:

```json
"textOverrides": {
  "restaurant": {
    "heroCtaButtonText": "Book a Table",
    "menuSectionTitle": "Our Menu",
    "bookingTitle": "Reserve a Table",
    "bookingCtaButtonText": "Send Booking Request",
    "whatsappBookingMessage": "a table"
  },
  "car dealership": { ... },
  "other": { ... }  // fallback
}
```

### SEO & Social

```json
{
  "seoDescription": "Meta description for search engines",
  "ogTitle": "Open Graph title",
  "ogDescription": "Open Graph description",
  "ogImage": "https://example.com/og-image.jpg",
  "favicon": "https://example.com/favicon.ico",
  "appleTouchIcon": "https://example.com/apple-touch-icon.png",
  "footerAboutText": "About text in footer",
  "socialLinks": {
    "facebook": "https://facebook.com/yourbusiness",
    "instagram": "https://instagram.com/yourbusiness",
    "twitter": "https://twitter.com/yourbusiness",
    "linkedin": "https://linkedin.com/company/yourbusiness"
  }
}
```

---

## 🎨 Customization

### Colors & Theme
Edit CSS custom properties in `style.css`:

```css
:root {
  --primary-color: #2D5016;      /* From config.primaryColor */
  --accent-color: #2D5016;       /* Set dynamically via JS */
  --text-dark: #1a1a1a;
  --text-light: #666;
  --bg-light: #f9f9f9;
  --white: #fff;
  --spacing-xs: 0.5rem;
  --spacing-sm: 1rem;
  --spacing-md: 2rem;
  --spacing-lg: 4rem;
  --border-radius: 8px;
  --transition: 0.3s ease;
}
```

### Fonts
Replace Google Fonts link in `index.html`:

```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

Update font families in `style.css`:
```css
:root {
  --font-heading: 'Playfair Display', serif;
  --font-body: 'Poppins', sans-serif;
}
```

### Images
- Replace URLs in `config.json` with your own (CDN, Cloudinary, local `/assets/`)
- For local images, place in `assets/` and reference as `assets/image.jpg`

### Forms & Integrations
The template uses WhatsApp for bookings and a simple contact form. Integrate with:
- **EmailJS** — Client-side email sending
- **Formspree** — Form endpoint service
- **Firebase/Supabase** — Backend-as-a-service
- **Custom API** — Modify `handleContactSubmit()` and `handleBookingSubmit()` in `script.js`

---

## 🛠️ SupaTemplate Deep Dive

### How It Works

1. **HTML loads** with semantic placeholder content
2. **JS fetches** `config.json` on `DOMContentLoaded`
3. **`applyConfig()`** updates all DOM elements:
   - Text content, meta tags, colors, images
   - WhatsApp links, contact info, opening hours
   - SEO schema, Open Graph, favicons
4. **`initializeMenu()`** renders `menuData`:
   - Tabbed categories for restaurant/dealership
   - Flat sections for service businesses
5. **Event listeners** attached for modals, lightbox, forms

### Business Type Behavior

| Type | Tabs | Booking Modal | Party Size | Direct WhatsApp |
|------|------|---------------|------------|-----------------|
| restaurant | ✓ | ✓ | ✓ | |
| car dealership | ✓ | ✓ | | ✓ |
| salon / spa / fitness / health | | ✓ | | |
| car wash / pet care / home services | | ✓ | | |
| professional services | | ✓ | | |
| other | | | | ✓ |

### Accessibility Features
- Semantic HTML5 (`header`, `nav`, `main`, `section`, `footer`)
- ARIA labels on interactive elements
- Focus-visible styles for keyboard navigation
- Alt text on all images (from config)
- Color contrast ratios (WCAG AA)
- Reduced motion support
- Screen reader friendly modals/lightbox

---

## 🚀 Deployment

### Static Hosting (Recommended)

| Platform | Setup |
|----------|-------|
| **Netlify** | Drag & drop `templates/supa-template/` folder |
| **Vercel** | Import Git repo, output: `.` |
| **GitHub Pages** | Enable Pages from `/templates/supa-template` |
| **Cloudflare Pages** | Connect repo, build: none, output: `templates/supa-template` |
| **Firebase Hosting** | `firebase init hosting`, public: `templates/supa-template` |

**No build step required.** Just upload the template folder.

### Multi-Tenant / SaaS Deployment

Serve different `config.json` per customer:

```
yourdomain.com/client-a/     → serves config-a.json
yourdomain.com/client-b/     → serves config-b.json
```

Options:
1. **Subdirectory per client** — Copy template folder, swap `config.json`
2. **Backend API** — Replace `fetch('./config.json')` with `fetch('/api/config?client=xxx')`
3. **Edge function** — Rewrite at CDN level (Cloudflare Workers, Netlify Edge)

---

## 🗺️ Roadmap

### ✅ Completed (v1.0)
- [x] SupaTemplate — Multi-business landing page
- [x] 6 business config examples (restaurant, dealership, salon, spa, fitness, real estate)
- [x] JSON-driven configuration
- [x] WhatsApp booking flow
- [x] Dynamic gallery with lightbox
- [x] SEO schema & meta tags
- [x] Responsive, accessible design

### 🚧 In Progress
- [ ] SupaTemplate accessibility audit & fixes
- [ ] Template-specific README files
- [ ] Contributing guidelines & templates
- [ ] Automated screenshot generation

### 📋 Planned Templates
- [ ] **SaaS Dashboard** — Admin panel with charts, tables, user management
- [ ] **Agency Landing Page** — Portfolio, services, team, case studies
- [ ] **Portfolio** — Creative showcase with filtering
- [ ] **Hotel/Resort** — Rooms, booking, amenities, packages
- [ ] **Medical Clinic** — Doctors, services, appointments, patient portal
- [ ] **School/Education** — Courses, faculty, events, admissions
- [ ] **E-commerce Landing** — Product grid, cart, checkout integration
- [ ] **Construction** — Projects, services, testimonials, quote request
- [ ] **Church/Non-profit** — Events, donations, sermons, ministries
- [ ] **Event/Conference** — Schedule, speakers, tickets, sponsors

### 🔧 Future Improvements
- [ ] Dark mode support via CSS custom properties
- [ ] Internationalization (i18n) in config
- [ ] Component library extraction (reusable cards, modals, forms)
- [ ] Visual config editor (web-based JSON generator)
- [ ] Template preview site (GitHub Pages)
- [ ] Automated accessibility testing in CI
- [ ] Performance budgets & monitoring

---

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

**Quick start for contributors:**
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-template`
3. Add your template in `templates/your-template-name/`
4. Follow the template structure conventions
5. Submit a Pull Request

**Areas to contribute:**
- New templates
- Bug fixes
- Accessibility improvements
- Performance optimizations
- Documentation
- Config examples for existing templates
- Translations

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

```
MIT License

Copyright (c) 2024 Owen Ndeule

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

You are free to use, modify, distribute, sell, and include in commercial projects. Please include the original copyright notice when redistributing.

---

## 👤 Author

**Owen Ndeule**
- GitHub: [@owenndeule](https://github.com/owenndeule)

---

## ⭐ Support

If you find this project useful, please consider giving it a star on GitHub. It helps with visibility and motivates continued development.

[![Star History Chart](https://api.star-history.com/svg?repos=owenndeule/Saas-templates&type=Date)](https://star-history.com/#owenndeule/Saas-templates&Date)