# SupaTemplate — Multi-Business Landing Page

A single, data-driven template that adapts to 10+ business types through configuration alone. No code changes needed — just edit `config.json`.

## Features

| Feature | Details |
|---------|---------|
| **Business Types** | Restaurant, Car Dealership, Salon, Spa, Fitness, Car Wash, Pet Care, Home Services, Professional Services, Other |
| **Configuration** | Single `config.json` — no HTML editing needed |
| **Sections** | Hero, New Arrivals, Menu/Services (with tabs), Gallery, Testimonials, Booking Modal, Contact, Footer |
| **Booking** | WhatsApp-first flow with optional modal for appointments |
| **SEO** | Dynamic meta tags, Open Graph, JSON-LD schema, Google Analytics |
| **Images** | Lightbox with swipe/keyboard navigation, multi-image gallery cards |
| **Responsive** | Mobile-first, hamburger menu, touch-friendly |
| **Accessible** | Semantic HTML, ARIA labels, keyboard navigation, WCAG AA contrast, focus management |
| **Zero Dependencies** | Vanilla HTML/CSS/JS — no build tools, no frameworks |

## Quick Start

**Option A: Command Line**
```bash
# 1. Navigate to template
cd templates/supa-template

# 2. Choose a config example (or edit config.json directly)
cp ../../configs/supa-template/config-restaurant.json config.json

# 3. Start a local server (required for config.json fetch)
python -m http.server 8000
# or: npx serve
# or: php -S localhost:8000

# 4. Open http://localhost:8000
```

**Option B: No Command Line (File Manager)**
1. Open this folder (`supa-template/`) in your file manager
2. Go up two levels to `configs/supa-template/` folder
3. Copy the config you want (e.g., `config-restaurant.json`)
4. Paste it here in `supa-template/` and **rename to `config.json`** (replace existing)
5. Start a local server:
   - **VS Code**: Install "Live Server" extension → Right-click `index.html` → "Open with Live Server"
   - **Windows**: Create `start.bat` with `python -m http.server 8000` and double-click
   - **Mac/Linux**: Open Terminal here → run `python -m http.server 8000`
6. Open http://localhost:8000

## How the Config System Works

The template uses a single `config.json` file in the template root. On page load, the JavaScript fetches this file and dynamically renders the entire site.

### Choosing a Configuration

All example configurations are stored in the central `configs/supa-template/` folder at the repository root:

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

**To use an example config:**

**Command Line:**
```bash
# Copy any example to config.json in the template folder
cp ../../configs/supa-template/config-restaurant.json config.json

# Or create your own by copying and editing
cp ../../configs/supa-template/config-restaurant.json config.json
# Then edit config.json with your business details
```

**Without Command Line (File Manager):**
1. Open `configs/supa-template/` folder (two levels up from here)
2. Copy the config you want (e.g., `config-restaurant.json`)
3. Paste it here in `supa-template/` and **rename to `config.json`** (replace existing)
4. Reload browser — changes apply instantly

**To Customize:** Open `config.json` in any text editor and edit:
- `businessName`, `businessType`, `tagline`
- `primaryColor`, `whatsappNumber`, `currencySymbol`
- `phoneNumber`, `email`, `address`
- `menuData` — your products/services/prices
- See [Configuration Guide](../docs/configuration-guide.md) for all fields

### Advanced: Direct Config Fetch (No Copy Needed)

Instead of copying config files, you can **edit the fetch path directly in `script.js`** to point to any config:

**In `script.js` line 25, change:**
```javascript
const response = await fetch('./config.json');
```

**To any of these:**
```javascript
// Load directly from configs/supa-template/ folder (relative to template)
const response = await fetch('../../configs/supa-template/config-restaurant.json');
const response = await fetch('../../configs/supa-template/config-car-dealership.json');
const response = await fetch('../../configs/supa-template/config-salon.json');
const response = await fetch('../../configs/supa-template/config-spa.json');
const response = await fetch('../../configs/supa-template/config-fitness.json');
const response = await fetch('../../configs/supa-template/config-real-estate.json');
const response = await fetch('../../configs/supa-template/config.json');  // Generic template
```

**Benefits:**
- No file copying needed
- Switch configs by changing one line
- Useful for testing multiple configs quickly
- Works with any config in the `configs/supa-template/` folder

**Note:** This requires a local server (CORS blocks `file://` fetches).

### How JavaScript Loads the Config

In `script.js`, the config is loaded on `DOMContentLoaded`:

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

### Creating Your Own Config

1. Copy an existing example:
   ```bash
   cp ../../configs/supa-template/config-restaurant.json config.json
   ```

2. Edit `config.json` with your business details:
   - `businessName`, `businessType`, `tagline`
   - `primaryColor`, `whatsappNumber`, `currencySymbol`
   - `menuData` — your products/services
   - `gallery`, `testimonials`, `openingHours`
   - Contact info, SEO, social links

3. Reload the page — changes apply instantly

## Configuration

All customization happens in `config.json`. See [Configuration Guide](../docs/configuration-guide.md) for full details.

### Core Fields

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

### Content Sections

- `testimonials` — Array of customer reviews
- `openingHours` — Object with days as keys
- `phoneNumber`, `email`, `address` — Contact info
- `mapUrl` — Google Maps embed URL
- `heroImage` — Hero background image
- `gallery` — Array of gallery items with images
- `menuData` — Products/services by category
- `textOverrides` — Business-type specific text (CTA buttons, titles)
- `socialLinks` — Social media URLs
- `seoDescription`, `ogTitle`, `ogDescription`, `ogImage` — SEO/Open Graph
- `favicon`, `appleTouchIcon` — Favicon URLs
- `footerAboutText` — Footer description

### Business Type Behavior

| Type | Tabs | Booking Modal | Party Size | Direct WhatsApp |
|------|------|---------------|------------|-----------------|
| restaurant | ✓ | ✓ | ✓ | |
| car dealership | ✓ | ✓ | | ✓ |
| salon / spa / fitness / health | | ✓ | | |
| car wash / pet care / home services | | ✓ | | |
| professional services | | ✓ | | |
| other | | | | ✓ |

## Example Configs

All example configurations are in the central `configs/supa-template/` folder at the repository root:

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

To use an example:
```bash
cp ../../configs/supa-template/config-restaurant.json config.json
```

## Customization

### Colors & Theme

Edit CSS custom properties in `style.css`:

```css
:root {
  --primary-color: #2D5016;
  --accent-color: #2D5016;  /* Set dynamically from config */
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

## Deployment

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

## File Structure

```
supa-template/
├── index.html          # Semantic, accessible HTML
├── style.css           # CSS with custom properties
├── script.js           # Dynamic rendering engine
├── config.json         # Your business config (edit this!)
├── assets/             # Local images, fonts, files
├── robots.txt          # Search engine directives
├── sitemap.xml         # Site map template
├── LICENSE             # MIT License
└── README.md           # This file
```

**Example configs:** `../../configs/supa-template/`

## How It Works

1. **HTML loads** with semantic placeholder content
2. **JS fetches** `config.json` on `DOMContentLoaded`
3. **`applyConfig()`** updates all DOM elements:
   - Text content, meta tags, colors, images
   - WhatsApp links, contact info, opening hours
   - SEO schema, Open Graph, favicons
   - Navigation labels based on business type
4. **`initializeMenu()`** renders `menuData`:
   - Tabbed categories for restaurant/dealership
   - Flat sections for service businesses
5. **Event listeners** attached for modals, lightbox, forms

## Accessibility Features

- Semantic HTML5 (`header`, `nav`, `main`, `section`, `footer`)
- ARIA labels on interactive elements
- Focus-visible styles for keyboard navigation
- Alt text on all images (from config)
- Color contrast ratios (WCAG AA)
- Reduced motion support
- Screen reader friendly modals/lightbox
- Focus trapping in modals
- Keyboard navigation for all interactive elements

## Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## License

MIT — see [LICENSE](LICENSE) file. Use freely for any project.