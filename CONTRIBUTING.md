# Contributing to SaaS Templates

Thank you for your interest in contributing! This project thrives on community contributions. Whether you're adding a new template, fixing a bug, improving documentation, or suggesting features — your help is appreciated.

---

## 📋 Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [How to Contribute](#how-to-contribute)
3. [Adding a New Template](#adding-a-new-template)
4. [Improving Existing Templates](#improving-existing-templates)
5. [Documentation Contributions](#documentation-contributions)
6. [Pull Request Process](#pull-request-process)
7. [Code Style & Standards](#code-style--standards)
8. [Testing Guidelines](#testing-guidelines)
9. [Getting Help](#getting-help)

---

## 🤝 Code of Conduct

By participating in this project, you agree to abide by our [Code of Conduct](CODE_OF_CONDUCT.md). Please be respectful, inclusive, and constructive in all interactions.

---

## 🛠️ How to Contribute

### 1. Fork & Clone

```bash
# Fork on GitHub, then clone your fork
git clone https://github.com/YOUR-USERNAME/Saas-templates.git
cd Saas-templates

# Add upstream remote
git remote add upstream https://github.com/owenndeule/Saas-templates.git
```

### 2. Create a Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/issue-description
# or
git checkout -b docs/update-readme
```

### 3. Make Changes

Follow the guidelines below for your contribution type.

### 4. Commit & Push

```bash
git add .
git commit -m "feat: add amazing new template"
git push origin feature/your-feature-name
```

### 5. Open a Pull Request

Use the PR template and fill in all required sections.

---

## 🎨 Adding a New Template

This is the most impactful way to contribute. Here's what a new template needs:

### Template Structure

Each template lives in its own directory under `templates/`:

```
templates/
└── your-template-name/
    ├── index.html          # Required: Semantic, accessible HTML
    ├── style.css           # Required: CSS with custom properties
    ├── script.js           # Optional: Vanilla JS only
    ├── config.json         # Required: Default configuration (working example)
    ├── assets/             # Optional: Local images, fonts, files
    ├── README.md           # Required: Template documentation
    ├── LICENSE             # Required: MIT license file
    ├── robots.txt          # Optional: SEO directives
    └── sitemap.xml         # Optional: Site map template
```

### Config Examples Location

Example configurations are stored in the central `configs/` folder at the repository root, namespaced by template name:

```
configs/
└── your-template-name/
    ├── config.json                  # Generic template
    ├── config-example1.json
    ├── config-example2.json
    └── config-example3.json
```

When releasing, config examples are added directly to `configs/your-template-name/`.

### Naming Conventions

| Item | Convention | Example |
|------|------------|---------|
| Template directory | kebab-case | `saas-dashboard`, `agency-landing` |
| Config examples | `config-{name}.json` | `config-restaurant.json` |
| CSS classes | BEM-ish | `.hero__title`, `.menu-card--featured` |
| JS functions | camelCase | `initializeMenu()`, `renderItems()` |

### Required Features

Every template **must** include:

1. **Zero dependencies** — No npm, no build tools, no frameworks
2. **Configuration-driven** — Content via `config.json`, not hardcoded HTML
3. **Responsive** — Mobile-first, works 320px–1920px+
4. **Accessible** — Semantic HTML, ARIA labels, keyboard navigation, WCAG AA contrast
5. **SEO-ready** — Meta tags, Open Graph, JSON-LD schema
6. **Deployable anywhere** — Static files only

### Template Documentation (README.md)

Each template needs a README with:

```markdown
# Template Name

Brief description of purpose and target audience.

## Features
- Feature 1
- Feature 2

## Quick Start
```bash
cd templates/your-template-name
cp ../../configs/your-template-name/config-example1.json config.json
python -m http.server 8000
```

## Configuration
Explain config.json structure with table.

## Customization
Colors, fonts, images, integrations.

## Business Types (if applicable)
Table of supported types and features.

## License
MIT — see LICENSE file.
```

### Config Examples

Provide **at least 3** distinct config examples showing different use cases. Each should:
- Be a complete, valid JSON file
- Use realistic content (not "Lorem ipsum")
- Include all required fields
- Demonstrate different business types or layouts

### Screenshots

Include screenshots in `screenshots/your-template-name/`:
- `hero.png` — Hero/landing section
- `features.png` — Key feature section (menu, services, gallery)
- `mobile.png` — Mobile view (optional but recommended)

**Dimensions:** 1280px width, auto height. Use the template's actual rendering.

When releasing, screenshots go directly to `screenshots/your-template-name/`.

---

## 🔧 Improving Existing Templates

### Bug Fixes

1. Check existing issues first
2. Create a minimal reproduction
3. Fix with minimal, focused changes
4. Test across browsers (Chrome, Firefox, Safari)
5. Test mobile responsiveness
6. Verify accessibility isn't regressed

### Feature Enhancements

1. Open an issue to discuss first
2. Ensure it aligns with zero-dependency philosophy
3. Maintain backward compatibility with existing configs
4. Update documentation and config examples if needed

### Accessibility Improvements

High priority areas:
- Color contrast ratios
- Keyboard navigation
- Screen reader support
- Focus management in modals
- Alt text handling
- Reduced motion support

### Performance Optimizations

- Minimize layout shifts
- Optimize image loading (lazy, proper sizing)
- Reduce JavaScript execution time
- Leverage browser caching headers

---

## 📝 Documentation Contributions

Documentation lives in:
- `README.md` — Root project documentation
- `templates/*/README.md` — Template-specific docs
- `docs/` — Deep-dive guides

### Guidelines

- Write for developers of varying experience levels
- Use clear headings, tables, code blocks
- Include working examples
- Link between related documents
- Keep it accurate — test your instructions

---

## 🔄 Pull Request Process

### Before Submitting

- [ ] Code follows project conventions
- [ ] No console errors or warnings
- [ ] Works in Chrome, Firefox, Safari (latest)
- [ ] Mobile responsive (test 375px, 768px, 1024px+)
- [ ] Keyboard navigable
- [ ] No accessibility regressions (run axe-core if possible)
- [ ] Config examples updated if schema changed
- [ ] Documentation updated
- [ ] Screenshots updated if UI changed

### PR Title Format

```
feat(scope): brief description
fix(scope): brief description
docs(scope): brief description
refactor(scope): brief description
test(scope): brief description
chore(scope): brief description
```

Examples:
- `feat(supa-template): add dark mode support`
- `fix(script.js): prevent lightbox swipe on vertical scroll`
- `docs(readme): add deployment guide for Cloudflare Pages`

### Review Process

1. Automated checks run (if CI configured)
2. Maintainer reviews code, tests locally
3. Feedback addressed via new commits
4. Approved → merged (squash or merge commit)
5. Contributor credited in release notes

---

## 🎯 Code Style & Standards

### HTML

```html
<!-- Semantic elements -->
<header>, <nav>, <main>, <section>, <article>, <aside>, <footer>

<!-- ARIA when needed -->
<button aria-label="Close modal" aria-expanded="false">

<!-- Descriptive IDs -->
<section id="pricing" aria-labelledby="pricing-heading">

<!-- Alt text from config -->
<img src="{{image}}" alt="{{name}}">
```

### CSS

```css
/* Custom properties for theming */
:root {
  --primary-color: #2D5016;
  --spacing-md: 2rem;
}

/* BEM-ish naming */
.menu-card { }
.menu-card__image { }
.menu-card--featured { }

/* Mobile-first */
.component { }
@media (min-width: 768px) { .component { } }
@media (min-width: 1024px) { .component { } }

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: none !important; }
}
```

### JavaScript

```javascript
// ES6 modules not used (single file for zero-deploy)
// Use IIFE or plain functions
function initializeMenu(config) { }

// Descriptive names
const currentActiveCategory = '';
const renderMenuItems = (items) => { };

// Feature detection
if ('IntersectionObserver' in window) { }

// Error handling
try {
  const config = await response.json();
} catch (error) {
  console.error('Config load failed:', error);
  showFallbackUI();
}
```

### JSON Config

```json
{
  "fieldName": "camelCase for keys",
  "arrays_use_plural": ["item1", "item2"],
  "objects_use_singular": { "key": "value" },
  "booleans_use_is_or_has": true,
  "comments_not_allowed": "JSON doesn't support comments"
}
```

---

## ✅ Testing Guidelines

### Manual Testing Checklist

For every change, verify:

- [ ] **Config loads** — All example configs render without errors
- [ ] **Responsive** — Test 320px, 375px, 768px, 1024px, 1440px, 1920px
- [ ] **Keyboard** — Tab through entire page, all interactive elements reachable
- [ ] **Screen reader** — Test with NVDA (Windows) or VoiceOver (Mac)
- [ ] **Touch** — Swipe gestures, tap targets (44px minimum)
- [ ] **Forms** — Submit, validation, WhatsApp links open correctly
- [ ] **Lightbox** — Open, navigate, close (keyboard, click, swipe, ESC)
- [ ] **Modals** — Open, close (button, overlay, ESC, back button)
- [ ] **Images** — Lazy loading, fallback on error
- [ ] **Console** — No errors, warnings acceptable only for known issues

### Automated Testing (Future)

When CI is set up:
- HTML validation (html-validate)
- CSS validation (stylelint)
- JavaScript linting (eslint)
- Accessibility (axe-core)
- Visual regression (playwright + pixelmatch)

---

## 🆘 Getting Help

- **Questions:** Open a [Discussion](https://github.com/owenndeule/Saas-templates/discussions)
- **Bugs:** File an [Issue](https://github.com/owenndeule/Saas-templates/issues/new?template=bug_report.md)
- **Feature requests:** File an [Issue](https://github.com/owenndeule/Saas-templates/issues/new?template=feature_request.md)
- **New template proposal:** File an [Issue](https://github.com/owenndeule/Saas-templates/issues/new?template=new_template.md)

---

## 🏷️ Labels

We use these labels to categorize issues and PRs:

| Label | Purpose |
|-------|---------|
| `template:supa-template` | Specific to SupaTemplate |
| `template:new` | New template proposal |
| `good first issue` | Beginner-friendly |
| `help wanted` | Community help needed |
| `accessibility` | A11y related |
| `performance` | Performance related |
| `documentation` | Docs only |
| `breaking-change` | Config/API breaking change |

---

## 🙏 Recognition

Contributors are recognized in:
- Release notes
- README.md contributors section
- GitHub contributor graph

Thank you for making this project better! 🎉