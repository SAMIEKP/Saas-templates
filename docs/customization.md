# Customization Guide

This guide covers advanced customization of SupaTemplate beyond the `config.json` file.

## CSS Custom Properties

All design tokens are defined as CSS custom properties in `style.css`. Override them in a separate CSS file or inline `<style>` block for easy theming.

### Color System

```css
:root {
  /* Primary brand color (set from config.primaryColor) */
  --accent-color: #2D5016;
  
  /* Semantic colors */
  --color-primary: var(--accent-color);
  --color-primary-hover: #1e3a0f;
  --color-primary-light: #e8f5e9;
  
  --color-text: #1a1a1a;
  --color-text-light: #666;
  --color-text-muted: #999;
  --color-text-inverse: #fff;
  
  --color-bg: #fff;
  --color-bg-alt: #f9f9f9;
  --color-bg-dark: #1a1a1a;
  
  --color-border: #e0e0e0;
  --color-border-focus: var(--accent-color);
  
  --color-success: #2e7d32;
  --color-warning: #f57f17;
  --color-error: #c62828;
  
  /* Status badge colors */
  --color-open: #2e7d32;
  --color-closed: #c62828;
}
```

### Typography

```css
:root {
  --font-heading: 'Playfair Display', Georgia, serif;
  --font-body: 'Poppins', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;
  
  --font-size-xs: 0.75rem;
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;
  --font-size-2xl: 1.5rem;
  --font-size-3xl: 2rem;
  --font-size-4xl: 2.5rem;
  
  --font-weight-normal: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 600;
  --font-weight-bold: 700;
  
  --line-height-tight: 1.1;
  --line-height-normal: 1.5;
  --line-height-relaxed: 1.75;
}
```

### Spacing

```css
:root {
  --space-xs: 0.25rem;
  --space-sm: 0.5rem;
  --space-md: 1rem;
  --space-lg: 1.5rem;
  --space-xl: 2rem;
  --space-2xl: 3rem;
  --space-3xl: 4rem;
  --space-4xl: 6rem;
}
```

### Borders & Shadows

```css
:root {
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-full: 9999px;
  
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.07);
  --shadow-lg: 0 10px 15px rgba(0,0,0,0.1);
  --shadow-xl: 0 20px 25px rgba(0,0,0,0.15);
  
  --shadow-focus: 0 0 0 3px var(--color-border-focus);
}
```

### Transitions

```css
:root {
  --transition-fast: 150ms ease;
  --transition-base: 250ms ease;
  --transition-slow: 350ms ease;
}
```

### Z-Index Scale

```css
:root {
  --z-dropdown: 100;
  --z-sticky: 200;
  --z-fixed: 300;
  --z-modal-backdrop: 400;
  --z-modal: 500;
  --z-popover: 600;
  --z-tooltip: 700;
}
```

## Dark Mode Support

Add dark mode by extending the custom properties:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-text: #f5f5f5;
    --color-text-light: #aaa;
    --color-text-muted: #888;
    --color-text-inverse: #1a1a1a;
    
    --color-bg: #121212;
    --color-bg-alt: #1e1e1e;
    --color-bg-dark: #f5f5f5;
    
    --color-border: #333;
    
    --color-primary-light: #1e3a0f;
  }
  
  .hero {
    background-color: var(--color-bg-dark);
  }
  
  .menu-card,
  .gallery-card,
  .testimonial-card,
  .modal-container {
    background: var(--color-bg-alt);
    border-color: var(--color-border);
  }
  
  .form-group input,
  .form-group textarea,
  .form-group select {
    background: var(--color-bg);
    border-color: var(--color-border);
    color: var(--color-text);
  }
}
```

## Adding Custom Sections

### 1. Add HTML Section

In `index.html`, add your section:

```html
<section id="features" class="features-section" aria-labelledby="featuresHeading">
    <div class="container">
        <h2 id="featuresHeading" class="section-title">Why Choose Us</h2>
        <div class="features-grid" id="featuresGrid"></div>
    </div>
</section>
```

### 2. Add Config Data

In `config.json`:

```json
{
  "featuresData": [
    {
      "id": 1,
      "icon": "shield",
      "title": "Quality Guaranteed",
      "description": "All items inspected and certified"
    },
    {
      "id": 2,
      "icon": "truck",
      "title": "Free Delivery",
      "description": "On orders over $100"
    }
  ]
}
```

### 3. Add Render Function

In `script.js`:

```javascript
function renderFeatures(config) {
    const grid = document.getElementById('featuresGrid');
    if (!grid || !config.featuresData) return;
    
    grid.innerHTML = config.featuresData.map(feature => `
        <div class="feature-card">
            <div class="feature-icon">
                <svg>...</svg>
            </div>
            <h3>${feature.title}</h3>
            <p>${feature.description}</p>
        </div>
    `).join('');
}
```

### 4. Call in DOMContentLoaded

```javascript
document.addEventListener('DOMContentLoaded', async function() {
    // ... existing code
    renderFeatures(config);
});
```

### 5. Add Styles

In `style.css`:

```css
.features-section {
    padding: var(--space-4xl) 0;
    background: var(--color-bg-alt);
}

.features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: var(--space-xl);
}

.feature-card {
    text-align: center;
    padding: var(--space-xl);
}

.feature-icon {
    width: 64px;
    height: 64px;
    margin: 0 auto var(--space-md);
    background: var(--color-primary-light);
    border-radius: var(--radius-full);
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--accent-color);
}
```

## Modifying Components

### Button Variants

```css
/* Base button */
.cta-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: var(--space-sm);
    padding: var(--space-md) var(--space-xl);
    font-family: var(--font-body);
    font-size: var(--font-size-base);
    font-weight: var(--font-weight-semibold);
    border: none;
    border-radius: var(--radius-md);
    cursor: pointer;
    transition: all var(--transition-base);
    text-decoration: none;
}

/* Primary */
.cta-button {
    background: var(--accent-color);
    color: var(--color-text-inverse);
}

.cta-button:hover {
    background: var(--color-primary-hover);
    transform: translateY(-2px);
    box-shadow: var(--shadow-md);
}

/* Secondary */
.cta-button--secondary {
    background: transparent;
    color: var(--accent-color);
    border: 2px solid var(--accent-color);
}

.cta-button--secondary:hover {
    background: var(--color-primary-light);
}

/* Outline */
.cta-button--outline {
    background: transparent;
    color: var(--color-text);
    border: 2px solid var(--color-border);
}

.cta-button--outline:hover {
    border-color: var(--accent-color);
    color: var(--accent-color);
}

/* Sizes */
.cta-button--sm {
    padding: var(--space-sm) var(--space-md);
    font-size: var(--font-size-sm);
}

.cta-button--lg {
    padding: var(--space-lg) var(--space-2xl);
    font-size: var(--font-size-lg);
}
```

### Card Variants

```css
/* Base card */
.card {
    background: var(--color-bg);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-sm);
    overflow: hidden;
    transition: all var(--transition-base);
}

.card:hover {
    box-shadow: var(--shadow-lg);
    transform: translateY(-4px);
}

/* Menu card */
.menu-card {
    display: flex;
    flex-direction: column;
}

.menu-card-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.menu-card-content {
    padding: var(--space-lg);
    display: flex;
    flex-direction: column;
    flex: 1;
}

.menu-card-title {
    font-family: var(--font-heading);
    font-size: var(--font-size-xl);
    margin-bottom: var(--space-sm);
}

.menu-card-description {
    color: var(--color-text-light);
    flex: 1;
    margin-bottom: var(--space-md);
}

.menu-card-price {
    font-size: var(--font-size-xl);
    font-weight: var(--font-weight-bold);
    color: var(--accent-color);
    margin-bottom: var(--space-md);
}

/* Badge */
.menu-card-badge {
    position: absolute;
    top: var(--space-md);
    left: var(--space-md);
    padding: var(--space-xs) var(--space-sm);
    font-size: var(--font-size-xs);
    font-weight: var(--font-weight-bold);
    border-radius: var(--radius-full);
    text-transform: uppercase;
    letter-spacing: 0.05em;
}

.badge-new-arrival { background: #e3f2fd; color: #1565c0; }
.badge-popular { background: #fff3e0; color: #e65100; }
.badge-sale { background: #fce4ec; color: #c62828; }
.badge-signature { background: #f3e5f5; color: #7b1fa2; }
```

## JavaScript Customization

### Adding Custom Event Handlers

```javascript
// In script.js, after applyConfig()
function initializeCustomFeatures(config) {
    // Custom scroll spy
    const sections = document.querySelectorAll('section[id]');
    const navLinks = document.querySelectorAll('.nav-link[href^="#"]');
    
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                const id = entry.target.id;
                navLinks.forEach(link => {
                    link.classList.toggle('active', link.getAttribute('href') === `#${id}`);
                });
            }
        });
    }, { threshold: 0.3, rootMargin: '-100px 0px -66%' });
    
    sections.forEach(section => observer.observe(section));
    
    // Custom: Track WhatsApp clicks
    document.querySelectorAll('.whatsapp-cta').forEach(btn => {
        btn.addEventListener('click', () => {
            if (typeof gtag !== 'undefined') {
                gtag('event', 'whatsapp_click', {
                    'button_text': btn.textContent.trim(),
                    'page_location': window.location.href
                });
            }
        });
    });
}
```

### Extending Business Types

To add a new business type:

1. **Add to `typesWithTabs`** in `initializeMenu()`
2. **Add to `typesWithModal`** in `applyConfig()` and `initializeBookingModal()`
3. **Add text overrides** in config examples
4. **Test** all UI behaviors

```javascript
// In applyConfig()
const typesWithTabs = ['restaurant', 'car dealership', 'real estate'];
const typesWithModal = ['restaurant', 'salon', 'spa', 'fitness', 'health', 'car wash', 'pet care', 'home services', 'professional services', 'real estate'];
```

## Image Optimization

### Recommended Specs

| Use Case | Width | Format | Quality |
|----------|-------|--------|---------|
| Hero | 1920px | WebP/JPEG | 80% |
| Menu/Service | 800px | WebP/JPEG | 75% |
| Gallery | 1200px | WebP/JPEG | 80% |
| Thumbnail | 400px | WebP | 70% |
| Favicon | 32x32 | ICO/PNG | - |
| Apple Touch | 180x180 | PNG | - |

### Using WebP with Fallback

```html
<picture>
    <source srcset="image.webp" type="image/webp">
    <img src="image.jpg" alt="Description" loading="lazy">
</picture>
```

Or use a CDN that auto-converts (Cloudinary, imgix, Cloudflare Images).

## Font Loading Optimization

```html
<!-- Preconnect to Google Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Preload critical fonts -->
<link rel="preload" as="font" type="font/woff2" crossorigin href="https://fonts.gstatic.com/s/poppins/v20/pxiEyp8kv8JHgFVrJJfecg.woff2">

<!-- Font display swap -->
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

## Performance Tips

1. **Minify CSS/JS** for production (use online tools or build step)
2. **Enable compression** (gzip/brotli) on your hosting
3. **Set cache headers** for static assets
4. **Use a CDN** for images and fonts
5. **Lazy load** non-critical images (already implemented)
6. **Defer non-critical JS** — move analytics to bottom
7. **Reduce HTTP requests** — combine CSS if multiple files

## Testing Checklist

After customization:

- [ ] All config examples still work
- [ ] Responsive at 320px, 375px, 768px, 1024px, 1440px, 1920px
- [ ] Keyboard navigation works everywhere
- [ ] Screen reader announces dynamic content
- [ ] Color contrast passes WCAG AA
- [ ] No console errors
- [ ] Forms submit correctly
- [ ] WhatsApp links open with correct message
- [ ] Lightbox navigation works (keyboard, swipe, arrows)
- [ ] Modals trap focus
- [ ] Reduced motion respected
- [ ] Print styles work (add `@media print` if needed)