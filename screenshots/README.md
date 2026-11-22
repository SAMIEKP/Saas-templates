# Screenshots

This folder contains preview screenshots for the SupaTemplate configurations.

## Structure

```
screenshots/
├── supa-template/
│   ├── hero.png           # Hero/landing section (1280px width)
│   ├── features.png       # Menu/Services section (1280px width)
│   ├── contact.png        # Contact section (1280px width)
│   ├── gallery.png        # Gallery section (1280px width)
│   ├── testimonials.png   # Testimonials section (1280px width)
│   ├── footer.png         # Footer section (1280px width)
│   └── mobile.png         # Mobile view (375px width) — *not yet captured*
```

## Current Screenshots (supa-template/)

| File | Description | Status |
|------|-------------|--------|
| `hero.png` | Hero/landing section | ✅ Captured |
| `features.png` | Menu/Services section | ✅ Captured |
| `contact.png` | Contact section | ✅ Captured |
| `gallery.png` | Gallery section | ✅ Captured |
| `testimonials.png` | Testimonials section | ✅ Captured |
| `footer.png` | Footer section | ✅ Captured |
| `mobile.png` | Mobile view (375px) | ❌ Missing |

## Generating Screenshots

**Command Line (Copy Config):**
```bash
cd templates/supa-template
cp ../../configs/supa-template/config-restaurant.json config.json
python -m http.server 8000
```

**Without Command Line (File Manager):**
1. Copy `configs/supa-template/config-restaurant.json` to `templates/supa-template/config.json` (replace existing)
2. Start a local server:
   - **VS Code**: Install "Live Server" → Right-click `index.html` → "Open with Live Server"
   - **Windows**: Create `start.bat` in `supa-template/` with `python -m http.server 8000` and double-click
   - **Mac/Linux**: Terminal in `supa-template/` → `python -m http.server 8000`
3. Open http://localhost:8000 in browser

**Advanced: Direct Fetch (No Copy):**
Edit `templates/supa-template/script.js` line 25:
```javascript
// Change from:
const response = await fetch('./config.json');
// To any config directly:
const response = await fetch('../../configs/supa-template/config-restaurant.json');
const response = await fetch('../../configs/supa-template/config-car-dealership.json');
const response = await fetch('../../configs/supa-template/config-salon.json');
const response = await fetch('../../configs/supa-template/config-spa.json');
const response = await fetch('../../configs/supa-template/config-fitness.json');
const response = await fetch('../../configs/supa-template/config-real-estate.json');
```
Then start server and reload — no file copying needed.

4. Use browser dev tools to set viewport:
   - Desktop: 1280px width
   - Mobile: 375px width

5. Take screenshots and save to `screenshots/supa-template/`

## Naming Convention

| File | Description | Dimensions |
|------|-------------|------------|
| `hero.png` | Hero/landing section | 1280px width, auto height |
| `features.png` | Key feature section (menu/services) | 1280px width, auto height |
| `contact.png` | Contact section | 1280px width, auto height |
| `gallery.png` | Gallery section | 1280px width, auto height |
| `testimonials.png` | Testimonials section | 1280px width, auto height |
| `footer.png` | Footer section | 1280px width, auto height |
| `mobile.png` | Mobile view | 375px width, auto height |

## Adding New Template Screenshots

Create a subfolder named after the template:
```
screenshots/
├── supa-template/
│   ├── hero.png
│   ├── features.png
│   ├── contact.png
│   ├── gallery.png
│   ├── testimonials.png
│   ├── footer.png
│   └── mobile.png
└── your-new-template/
    ├── hero.png
    ├── features.png
    └── mobile.png
```