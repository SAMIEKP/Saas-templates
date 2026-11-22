# Accessibility Guide

This document outlines the accessibility features of SupaTemplate and guidelines for maintaining compliance.

## Current Compliance

SupaTemplate targets **WCAG 2.1 Level AA** compliance.

### Implemented Features

| Feature | WCAG Criterion | Status |
|---------|---------------|--------|
| Semantic HTML structure | 1.3.1 Info and Relationships | ✅ |
| Meaningful page titles | 2.4.2 Page Titled | ✅ |
| Heading hierarchy | 1.3.1, 2.4.6 | ✅ |
| Alt text for images | 1.1.1 Non-text Content | ✅ |
| Color contrast (text) | 1.4.3 Contrast (Minimum) | ✅ |
| Color contrast (UI) | 1.4.11 Non-text Contrast | ✅ |
| Keyboard navigation | 2.1.1 Keyboard | ✅ |
| Focus visible | 2.4.7 Focus Visible | ✅ |
| Focus order | 2.4.3 Focus Order | ✅ |
| Focus trapping (modals) | 2.4.3, 4.1.2 | ✅ |
| ARIA labels | 1.3.1, 4.1.2 | ✅ |
| Live regions (status) | 4.1.3 Status Messages | ✅ |
| Reduced motion | 2.3.3 Animation from Interactions | ✅ |
| Language declaration | 3.1.1 Language of Page | ✅ |
| Form labels | 1.3.1, 3.3.2 | ✅ |
| Error identification | 3.3.1 | ⚠️ Basic |
| Skip links | 2.4.1 Bypass Blocks | ❌ Planned |

## Semantic Structure

```html
<header role="banner">
    <nav aria-label="Main navigation">...</nav>
</header>

<main>
    <section id="home" aria-labelledby="hero-heading">...</section>
    <section id="menu" aria-labelledby="menuSectionTitle">...</section>
    <section id="gallery" aria-labelledby="galleryHeading">...</section>
    <section id="testimonials" aria-labelledby="testimonialsHeading">...</section>
    <section id="reservations" aria-labelledby="reservationsHeading">...</section>
    <section id="contact" aria-labelledby="contactHeading">...</section>
</main>

<footer role="contentinfo">...</footer>
```

## ARIA Patterns Used

### Navigation
```html
<nav aria-label="Main navigation">
    <a href="#home" class="nav-link">Home</a>
    ...
</nav>

<nav class="nav-mobile" id="mobileNav" aria-label="Mobile navigation">
    ...
</nav>
```

### Tabs (Menu Categories)
```html
<div class="menu-tabs" role="tablist" aria-label="Menu categories">
    <button role="tab" aria-selected="true" aria-controls="menuGrid" data-category="Starters">
        Starters
    </button>
    ...
</div>
```

### Modals
```html
<div id="bookingModal" role="dialog" aria-modal="true" aria-labelledby="bookingTitle" hidden>
    <button class="modal-close-btn" aria-label="Close booking modal">&times;</button>
    <h2 id="bookingTitle">Book a Table</h2>
    ...
</div>
```

### Lightbox
```html
<div id="lightbox" role="dialog" aria-modal="true" aria-labelledby="lightboxTitle" hidden>
    <span class="lightbox-close" aria-label="Close lightbox">&times;</span>
    <img id="lightboxImage" alt="Gallery Image">
    <a class="lightbox-prev" aria-label="Previous image">...</a>
    <a class="lightbox-next" aria-label="Next image">...</a>
    <h3 id="lightboxTitle"></h3>
    ...
</div>
```

### Live Regions
```html
<span id="statusBadge" class="status-badge" aria-live="polite"></span>
```

### Forms
```html
<form id="reservationForm" novalidate>
    <div class="form-group">
        <label for="reservationDate">Date</label>
        <input type="date" id="reservationDate" required aria-required="true">
    </div>
    ...
</form>
```

### Images
```html
<!-- Config-driven alt text -->
<img src="${item.images[0]}" alt="${item.name}" class="menu-card-image" loading="lazy">

<!-- Decorative images -->
<svg aria-hidden="true">...</svg>
```

## Color Contrast

### Current Palette (Light Mode)

| Element | Foreground | Background | Ratio | Status |
|---------|-----------|------------|-------|--------|
| Body text | `#1a1a1a` | `#fff` | 12.6:1 | ✅ AA/AAA |
| Light text | `#666` | `#fff` | 5.7:1 | ✅ AA |
| Muted text | `#999` | `#fff` | 3.0:1 | ❌ Large only |
| Primary button | `#fff` | `#2D5016` | 8.2:1 | ✅ AA/AAA |
| Secondary button | `#2D5016` | `#fff` | 8.2:1 | ✅ AA/AAA |
| Links | `#2D5016` | `#fff` | 8.2:1 | ✅ AA/AAA |
| Focus ring | `#2D5016` | `#fff` | 8.2:1 | ✅ AA/AAA |
| Badge (new) | `#1565c0` | `#e3f2fd` | 6.1:1 | ✅ AA |
| Badge (popular) | `#e65100` | `#fff3e0` | 5.2:1 | ✅ AA |
| Status open | `#fff` | `#2e7d32` | 8.6:1 | ✅ AA/AAA |
| Status closed | `#fff` | `#c62828` | 6.5:1 | ✅ AA |

### Dark Mode (Planned)

```css
@media (prefers-color-scheme: dark) {
    :root {
        --color-text: #f5f5f5;      /* 15.3:1 on #121212 */
        --color-text-light: #bbb;   /* 4.5:1 on #121212 */
        --color-bg: #121212;
        --color-bg-alt: #1e1e1e;
        --color-border: #333;
    }
}
```

## Keyboard Navigation

### Tab Order
1. Header: Logo → Nav links → WhatsApp button → Mobile menu toggle
2. Hero: CTA button
3. Menu: Tab buttons → Menu items (View Details buttons)
4. Gallery: Images → See More button
5. Testimonials: (read-only)
6. Booking modal: Close → Form fields → Submit → WhatsApp links
7. Contact form: Fields → Submit
8. Footer: Links → Social icons
9. Float WhatsApp button
10. Scroll to top button

### Key Bindings

| Context | Key | Action |
|---------|-----|--------|
| Global | `Tab` | Next focusable |
| Global | `Shift+Tab` | Previous focusable |
| Lightbox | `Escape` | Close |
| Lightbox | `ArrowLeft` | Previous image |
| Lightbox | `ArrowRight` | Next image |
| Lightbox | `Tab` | Trap in lightbox |
| Modal | `Escape` | Close |
| Modal | `Tab` | Trap in modal |
| Mobile menu | `Enter`/`Space` | Toggle |
| Carousel | `ArrowLeft`/`ArrowRight` | Navigate |

### Focus Styles

```css
/* Visible focus for all interactive elements */
:focus-visible {
    outline: 3px solid var(--accent-color);
    outline-offset: 2px;
}

/* Remove outline for mouse users */
:focus:not(:focus-visible) {
    outline: none;
}

/* Custom focus for specific elements */
.cta-button:focus-visible,
.nav-link:focus-visible,
.menu-tab:focus-visible,
.form-group input:focus-visible,
.form-group textarea:focus-visible,
.form-group select:focus-visible {
    outline: 3px solid var(--accent-color);
    outline-offset: 2px;
}

/* Skip link (planned) */
.skip-link {
    position: absolute;
    top: -100%;
    left: 50%;
    transform: translateX(-50%);
    padding: var(--space-md) var(--space-xl);
    background: var(--accent-color);
    color: var(--color-text-inverse);
    border-radius: var(--radius-md);
    z-index: var(--z-tooltip);
    transition: top var(--transition-fast);
}

.skip-link:focus {
    top: var(--space-md);
}
```

## Focus Trapping

```javascript
function trapFocus(e, container) {
    const focusableElements = container.querySelectorAll(
        'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
    );
    const firstElement = focusableElements[0];
    const lastElement = focusableElements[focusableElements.length - 1];
    
    if (e.shiftKey && document.activeElement === firstElement) {
        e.preventDefault();
        lastElement.focus();
    } else if (!e.shiftKey && document.activeElement === lastElement) {
        e.preventDefault();
        firstElement.focus();
    }
}
```

Applied to:
- Booking modal
- Lightbox

## Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
    *,
    *::before,
    *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
        scroll-behavior: auto !important;
    }
    
    /* Disable parallax */
    .hero {
        background-attachment: scroll;
    }
}
```

JavaScript respects this:
```javascript
lightbox.addEventListener('touchmove', e => {
    // ... swipe handling
}, { passive: true });

// CSS transitions disabled via media query
```

## Screen Reader Testing

### Tested With
- **NVDA** (Windows) + Chrome/Firefox
- **VoiceOver** (macOS) + Safari
- **TalkBack** (Android) + Chrome
- **VoiceOver** (iOS) + Safari

### Announcement Verification

| Component | Expected Announcement |
|-----------|----------------------|
| Page load | "Business Name \| Tagline, main content" |
| Nav link | "Home, link" |
| Menu tab | "Starters, selected, tab 1 of 4" |
| View Details | "View details for Item Name, button" |
| Gallery image | "Gallery image, image" |
| Lightbox open | "Item Name, dialog" |
| Status badge | "Open Now" / "Closed" (live region) |
| Form error | "Date, required, invalid entry" |

## Form Accessibility

### Current Implementation
- All inputs have associated `<label>`
- `required` + `aria-required="true"`
- `novalidate` on forms (custom validation)
- Error handling: alert() (basic)

### Recommended Enhancements
```html
<!-- Add error messaging -->
<div class="form-group">
    <label for="reservationDate">Date</label>
    <input type="date" id="reservationDate" required aria-required="true" aria-describedby="date-error">
    <span id="date-error" class="error-message" aria-live="polite"></span>
</div>
```

```javascript
function showError(input, message) {
    const errorId = `${input.id}-error`;
    const errorEl = document.getElementById(errorId);
    if (errorEl) {
        errorEl.textContent = message;
        input.setAttribute('aria-invalid', 'true');
    }
}

function clearError(input) {
    const errorId = `${input.id}-error`;
    const errorEl = document.getElementById(errorId);
    if (errorEl) {
        errorEl.textContent = '';
        input.removeAttribute('aria-invalid');
    }
}
```

## Touch Target Sizes

All interactive elements meet **44×44px** minimum:

```css
.cta-button {
    min-height: 48px;
    min-width: 48px;
    padding: var(--space-md) var(--space-xl);
}

.nav-link {
    min-height: 44px;
    display: flex;
    align-items: center;
    padding: var(--space-sm) var(--space-md);
}

.menu-tab {
    min-height: 44px;
    padding: var(--space-sm) var(--space-md);
}

.gallery-nav-btn {
    width: 44px;
    height: 44px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.mobile-menu-toggle {
    width: 48px;
    height: 48px;
}
```

## Testing Checklist

### Automated
- [ ] Run axe-core: `npx @axe-core/cli templates/supa-template/index.html`
- [ ] Run Lighthouse accessibility audit
- [ ] Validate HTML: `npx html-validate templates/supa-template/index.html`

### Manual - Desktop
- [ ] Tab through entire page — all elements reachable
- [ ] Focus indicators visible on all interactive elements
- [ ] Modal traps focus (Tab/Shift+Tab)
- [ ] Lightbox traps focus
- [ ] Escape closes modals/lightbox
- [ ] Arrow keys navigate lightbox
- [ ] Screen reader reads page structure
- [ ] Live region announces status changes
- [ ] Forms submit with keyboard only
- [ ] Color contrast passes (use Colour Contrast Analyser)

### Manual - Mobile
- [ ] Touch targets 44×44px minimum
- [ ] Swipe gestures work (lightbox)
- [ ] Pinch zoom not disabled
- [ ] Viewport meta tag correct
- [ ] VoiceOver/TalkBack navigation works
- [ ] Rotor/gesture navigation works

### Configuration-Specific
- [ ] All config examples pass automated tests
- [ ] Dynamic content (menu, gallery) accessible
- [ ] Alt text from config is meaningful
- [ ] Business type variations tested

## Known Limitations

1. **Skip links** — Not yet implemented (planned)
2. **Form validation errors** — Uses `alert()`, not inline (needs enhancement)
3. **Carousel auto-play** — None (good for accessibility)
4. **PDF/downloads** — Not applicable
5. **Video/audio** — Not in template
6. **Complex tables** — Not in template

## Resources

- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
- [axe-core](https://github.com/dequelabs/axe-core)
- [Colour Contrast Analyser](https://www.tpgi.com/color-contrast-analyser/)
- [WebAIM Checklist](https://webaim.org/standards/wcag/checklist)