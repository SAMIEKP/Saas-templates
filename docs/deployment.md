# Deployment Guide

This guide covers deploying SupaTemplate to various hosting platforms.

## Prerequisites

- Template folder: `templates/supa-template/`
- Valid `config.json` in the template root
- All image URLs accessible
- Local testing completed

## Static Hosting Platforms

### Netlify (Recommended)

**Drag & Drop (Quickest):**
1. Zip the `supa-template` folder
2. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
3. Drag the zip file
4. Done! Get a `.netlify.app` URL instantly

**Git Integration (Auto-deploy):**
1. Push repo to GitHub/GitLab/Bitbucket
2. Connect repository in Netlify dashboard
3. Build settings:
   - Build command: (leave empty)
   - Publish directory: `templates/supa-template`
4. Deploy! Auto-deploys on every push

**Custom Domain:**
1. Domain settings → Add custom domain
2. Configure DNS (Netlify nameservers or CNAME)
3. SSL auto-provisioned

### Vercel

**CLI:**
```bash
cd templates/supa-template
npx vercel
# Follow prompts
```

**Git Integration:**
1. Import repository in Vercel dashboard
2. Framework preset: Other
3. Build command: (empty)
4. Output directory: `.`
5. Deploy

**Vercel.json (optional):**
```json
{
  "buildCommand": "",
  "outputDirectory": ".",
  "devCommand": "python -m http.server 8000",
  "installCommand": ""
}
```

### GitHub Pages

**From `/docs` folder:**
1. Copy `templates/supa-template/` to `/docs` in repo root
2. Settings → Pages → Source: Deploy from branch
3. Branch: `main`, Folder: `/docs`
4. Access at `https://username.github.io/repo-name/`

**GitHub Actions (Recommended):**
```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with:
          path: templates/supa-template
      - uses: actions/deploy-pages@v4
```

### Cloudflare Pages

1. Connect repository in Cloudflare Pages dashboard
2. Build settings:
   - Build command: (empty)
   - Build output directory: `templates/supa-template`
3. Deploy!
4. Custom domain: Add in Custom Domains tab

**Cloudflare-specific:**
- Automatic image optimization (Polish)
- Edge caching
- Free SSL/WAF

### Firebase Hosting

```bash
# Install CLI
npm install -g firebase-tools

# Login
firebase login

# Initialize
cd templates/supa-template
firebase init hosting
# Public directory: .
# Single-page app: No
# Overwrite index.html: No

# Deploy
firebase deploy
```

**firebase.json:**
```json
{
  "hosting": {
    "public": ".",
    "ignore": ["firebase.json", "**/.*", "**/node_modules/**"],
    "headers": [
      {
        "source": "**/*.@(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2)",
        "headers": [
          { "key": "Cache-Control", "value": "max-age=31536000" }
        ]
      }
    ]
  }
}
```

### AWS S3 + CloudFront

1. Create S3 bucket (static website hosting enabled)
2. Upload `supa-template/` contents
3. Create CloudFront distribution
4. Origin: S3 website endpoint
5. Default root object: `index.html`
6. Custom error pages: 404 → `index.html` (for SPA-like routing)

### Render (Static Sites)

1. New → Static Site
2. Connect repository
3. Build command: (empty)
4. Publish directory: `templates/supa-template`
5. Deploy!

### Surge.sh

```bash
cd templates/supa-template
npx surge
# First run: create account
# Domain: your-project.surge.sh
```

## Multi-Tenant / SaaS Deployment

### Option 1: Subdirectory per Client

```
/client-a/     → copy of supa-template with config-a.json
/client-b/     → copy of supa-template with config-b.json
```

**Nginx config:**
```nginx
location /client-a/ {
    alias /var/www/client-a/;
    try_files $uri $uri/ /client-a/index.html;
}

location /client-b/ {
    alias /var/www/client-b/;
    try_files $uri $uri/ /client-b/index.html;
}
```

### Option 2: Subdomain per Client

**DNS:** `client-a.yourdomain.com` → your server

**Nginx config:**
```nginx
server {
    listen 80;
    server_name *.yourdomain.com;
    
    root /var/www/supa-template;
    
    # Extract subdomain
    set $client "";
    if ($host ~* ^([^.]+)\.yourdomain\.com$) {
        set $client $1;
    }
    
    # Serve client-specific config
    location /config.json {
        try_files /configs/$client.json /config.json =404;
    }
    
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

### Option 3: Backend API

Replace in `script.js`:
```javascript
// Instead of:
const response = await fetch('./config.json');

// Use:
const clientId = new URLSearchParams(window.location.search).get('client') || 'default';
const response = await fetch(`/api/config/${clientId}`);
```

**API Response:**
```json
{
  "businessName": "Client A",
  "businessType": "restaurant",
  ...
}
```

### Option 4: Edge Functions (Cloudflare Workers)

```javascript
// worker.js
export default {
  async fetch(request, env) {
    const url = new URL(request.url);
    const client = url.searchParams.get('client') || 'default';
    
    // Fetch from KV or D1
    const config = await env.CONFIGS.get(client, { type: 'json' });
    
    if (!config) {
      return new Response('Config not found', { status: 404 });
    }
    
    // Inject config into HTML
    const html = await env.ASSETS.fetch(request);
    let htmlText = await html.text();
    
    // Replace placeholder or inject script
    htmlText = htmlText.replace(
      'const response = await fetch(\'./config.json\');',
      `const config = ${JSON.stringify(config)};`
    );
    
    return new Response(htmlText, {
      headers: { 'Content-Type': 'text/html' }
    });
  }
}
```

## CI/CD Pipeline

### GitHub Actions Example

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Validate JSON configs
        run: |
          for f in configs/supa-template/*.json; do
            echo "Validating $f"
            python -m json.tool "$f" > /dev/null
          done
      
      - name: Check HTML validity
        run: |
          npx html-validate templates/supa-template/index.html
      
      - name: Check CSS
        run: |
          npx stylelint templates/supa-template/style.css
      
      - name: Lint JavaScript
        run: |
          npx eslint templates/supa-template/script.js

  deploy-preview:
    needs: validate
    if: github.event_name == 'pull_request'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Netlify Preview
        uses: nwtgck/actions-netlify@v2
        with:
          publish-dir: './templates/supa-template'
          production-branch: main
          github-token: ${{ secrets.GITHUB_TOKEN }}
          deploy-message: "Preview for PR #${{ github.event.pull_request.number }}"
        env:
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}

  deploy-production:
    needs: validate
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Netlify Production
        uses: nwtgck/actions-netlify@v2
        with:
          publish-dir: './templates/supa-template'
          production-branch: main
          github-token: ${{ secrets.GITHUB_TOKEN }}
          deploy-message: "Production deploy ${{ github.sha }}"
        env:
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}
```

## Performance Optimization

### Headers

**Netlify (`_headers`):**
```
/*
  X-Frame-Options: DENY
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
  Permissions-Policy: camera=(), microphone=(), geolocation=()

/*.js
  Cache-Control: public, max-age=31536000, immutable

/*.css
  Cache-Control: public, max-age=31536000, immutable

/*.woff2
  Cache-Control: public, max-age=31536000, immutable

/*.jpg /*.png /*.webp
  Cache-Control: public, max-age=31536000, immutable
```

**Vercel (`vercel.json`):**
```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Frame-Options", "value": "DENY" },
        { "key": "X-Content-Type-Options", "value": "nosniff" }
      ]
    },
    {
      "source": "/(.*)\\.(js|css|woff2|jpg|png|webp)",
      "headers": [
        { "key": "Cache-Control", "value": "public, max-age=31536000, immutable" }
      ]
    }
  ]
}
```

### Compression

Enable gzip/brotli on your platform (usually automatic).

### Image Optimization

- Use WebP/AVIF with fallbacks
- Responsive images with `srcset`
- Lazy loading (already implemented)
- CDN: Cloudinary, imgix, Cloudflare Images

## Domain & SSL

### Custom Domain

1. Add domain in hosting dashboard
2. Configure DNS:
   - **Apex domain:** A record → provider IP / CNAME → provider hostname
   - **Subdomain:** CNAME → provider hostname
3. SSL auto-provisioned (Let's Encrypt or provider CA)

### www Redirect

**Netlify:** Automatic
**Vercel:** Automatic
**Cloudflare:** Page Rule: `www.example.com/*` → `https://example.com/$1` (301)

## Monitoring

### Uptime
- UptimeRobot (free)
- Pingdom
- Better Stack

### Analytics
- Google Analytics 4 (via config)
- Plausible (privacy-friendly)
- Fathom

### Error Tracking
- Sentry (add to script.js)
- LogRocket

## Troubleshooting

### Config Not Loading
- Check browser console for CORS errors
- Verify `config.json` is in same directory as `index.html`
- Ensure local server for development

### Images Not Showing
- Check image URLs in browser
- Verify CORS headers on image host
- Use direct image links (not gallery pages)

### Styles Broken
- Check CSS custom properties support
- Verify no syntax errors in CSS
- Check browser dev tools for failed loads

### WhatsApp Links Not Working
- Verify `whatsappNumber` format (digits only)
- Test `https://wa.me/15551234567` directly
- Check for ad blockers

### Form Submissions
- WhatsApp: Opens new tab (expected)
- Contact form: Console logs only (needs backend)

## Checklist Before Launch

- [ ] `config.json` validated
- [ ] All example configs tested
- [ ] Responsive on mobile/tablet/desktop
- [ ] Accessibility audit passed
- [ ] Performance budget met (< 3s load)
- [ ] SEO meta tags present
- [ ] Open Graph tags present
- [ ] JSON-LD schema valid
- [ ] Favicon works
- [ ] Custom domain configured
- [ ] SSL certificate active
- [ ] Analytics tracking
- [ ] Error tracking configured
- [ ] Backup/deploy process documented