# Configuration Guide

This guide provides a comprehensive reference for the `config.json` file used by SupaTemplate.

## Overview

The `config.json` file is the single source of truth for all content, styling, and behavior of your website. The template reads this file on load and dynamically renders everything — no HTML editing required.

## Complete Schema

```json
{
  "businessName": "string",
  "businessType": "string",
  "tagline": "string",
  "primaryColor": "string (hex)",
  "whatsappNumber": "string (digits only)",
  "currencySymbol": "string",
  "analyticsId": "string",
  "testimonials": "array",
  "openingHours": "object",
  "phoneNumber": "string",
  "email": "string",
  "address": "string (HTML allowed)",
  "mapUrl": "string (Google Maps embed URL)",
  "heroImage": "string (URL)",
  "gallery": "array",
  "menuData": "object",
  "textOverrides": "object",
  "socialLinks": "object",
  "seoDescription": "string",
  "ogTitle": "string",
  "ogDescription": "string",
  "ogImage": "string (URL)",
  "favicon": "string (URL)",
  "appleTouchIcon": "string (URL)",
  "footerAboutText": "string",
  "keywords": "string (optional, fallback)"
}
```

## Field Reference

### Core Identity

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `businessName` | Yes | string | Displayed in header, footer, page title, schema |
| `businessType` | Yes | string | Controls UI behavior. One of: `restaurant`, `car dealership`, `salon`, `spa`, `fitness`, `car wash`, `pet care`, `home services`, `professional services`, `other` |
| `tagline` | Yes | string | Subtitle under business name |
| `primaryColor` | Yes | hex string | Theme color for buttons, links, accents (e.g., `#2D5016`) |
| `whatsappNumber` | Yes | string | Country code + number, no `+` or spaces (e.g., `15551234567`) |
| `currencySymbol` | No | string | Prefix for prices (e.g., `$`, `€`, `MWK `) |
| `analyticsId` | No | string | Google Analytics 4 Measurement ID (G-XXXXXXXXXX) |

### Content Sections

#### Testimonials
```json
"testimonials": [
  {
    "name": "John D.",
    "comment": "Amazing service!",
    "stars": 5
  }
]
```
- `name` — Customer name
- `comment` — Review text
- `stars` — Integer 1-5

#### Opening Hours
```json
"openingHours": {
  "Monday": "9:00 AM - 6:00 PM",
  "Tuesday": "9:00 AM - 6:00 PM",
  "Sunday": "Closed"
}
```
- Keys: Day names (Monday–Sunday)
- Values: Time range string or "Closed"
- Used for display and open/closed status badge

#### Contact Info
```json
"phoneNumber": "+1 (555) 123-4567",
"email": "contact@example.com",
"address": "123 Main St<br>City, State 12345"
```
- `address` supports HTML line breaks (`<br>`)

#### Map URL
```json
"mapUrl": "https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3023.123!2d-73.987!3d40.748!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x89c259a9b3117469%3A0xd134e199a405a163!2sTimes%20Square!5e0!3m2!1sen!2sus!4v1234567890"
```
- Get from Google Maps → Share → Embed a map

#### Hero Image
```json
"heroImage": "https://example.com/hero.jpg"
```
- Full-width background for hero section
- Recommended: 1920px wide, optimized for web

#### Gallery
```json
"gallery": [
  {
    "name": "Interior",
    "description": "Cozy dining area",
    "images": [
      "https://example.com/img1.jpg",
      "https://example.com/img2.jpg"
    ]
  },
  "https://example.com/simple-image.jpg"
]
```
- Each item can be:
  - **Object** with `name`, `images[]` — shows name, supports multi-image carousel
  - **String URL** — simple image, no caption

#### Menu/Services Data (`menuData`)

Structure depends on `businessType`:

**Tabbed Categories** (restaurant, car dealership):
```json
"menuData": {
  "Starters": [
    {
      "id": 1,
      "name": "Bruschetta",
      "description": "Grilled bread with tomatoes",
      "price": "12",
      "images": ["https://example.com/bruschetta.jpg"],
      "badge": "Popular"
    }
  ],
  "Mains": [ ... ]
}
```

**Flat Services** (salon, spa, fitness, other):
```json
"menuData": {
  "Hair Services": [
    {
      "id": 1,
      "name": "Haircut",
      "description": "Precision cut with consultation",
      "price": "65",
      "images": ["https://example.com/haircut.jpg"],
      "badge": "Popular"
    }
  ],
  "Spa Treatments": [ ... ]
}
```

Each item supports:
| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `id` | Yes | number | Unique identifier |
| `name` | Yes | string | Display name |
| `description` | Yes | string | Details |
| `price` | Yes | string | Price (currency symbol added from config) |
| `images` | Yes | array[string] | At least one image URL |
| `badge` | No | string | "New", "Popular", "Sale", etc. |
| `year` | No | string | For vehicles |
| `mileage` | No | string | For vehicles |
| `fuelType` | No | string | For vehicles |
| `stock` | No | number | For inventory |
| `duration` | No | string | For services (e.g., "60 min") |
| `features` | No | array[string] | For memberships/packages |
| `includes` | No | array[string] | For packages |

#### Text Overrides (`textOverrides`)

Customize button labels, section titles per business type:

```json
"textOverrides": {
  "restaurant": {
    "heroCtaButtonText": "Book a Table",
    "menuSectionTitle": "Our Menu",
    "menuSectionSubtitle": "Authentic quality in every detail.",
    "bookingTitle": "Reserve a Table",
    "bookingCtaButtonText": "Send Booking Request",
    "contactBlockTitle": "Events & Private Dining",
    "contactBlockDescription": "Looking to host an event? We offer custom menus for private parties.",
    "whatsappBookingMessage": "a table",
    "hoursNote": "Last seating 30 minutes before closing",
    "keywords": "restaurant, italian, fine dining, pasta, wine"
  },
  "car dealership": { ... },
  "other": { ... }  // Fallback for unspecified types
}
```

Available overrides:
| Key | Used In |
|-----|---------|
| `heroCtaButtonText` | Hero CTA button |
| `menuSectionTitle` | Menu section heading |
| `menuSectionSubtitle` | Menu section subtitle |
| `bookingTitle` | Booking modal title |
| `bookingCtaButtonText` | Booking form submit button |
| `contactBlockTitle` | Contact section block title |
| `contactBlockDescription` | Contact section block description |
| `whatsappBookingMessage` | WhatsApp booking message text |
| `hoursNote` | Opening hours note |
| `keywords` | Meta keywords |

#### Social Links
```json
"socialLinks": {
  "facebook": "https://facebook.com/yourbusiness",
  "instagram": "https://instagram.com/yourbusiness",
  "twitter": "https://twitter.com/yourbusiness",
  "linkedin": "https://linkedin.com/company/yourbusiness"
}
```
- Empty strings are skipped
- Icons rendered automatically

#### SEO & Open Graph
```json
"seoDescription": "Meta description for search engines (150-160 chars)",
"ogTitle": "Open Graph title (for social sharing)",
"ogDescription": "Open Graph description",
"ogImage": "https://example.com/og-image.jpg",
"favicon": "https://example.com/favicon.ico",
"appleTouchIcon": "https://example.com/apple-touch-icon.png"
```

#### Footer
```json
"footerAboutText": "About text displayed in footer"
```

## Business Type Reference

### Restaurant
- Tabs: ✓ (categories from menuData keys)
- Booking Modal: ✓
- Party Size Field: ✓
- Hero CTA: Opens modal
- Nav: "Menu", "Book"

### Car Dealership
- Tabs: ✓ (categories from menuData keys)
- Booking Modal: ✓
- Party Size Field: ✗
- Hero CTA: Links to #menu
- Nav: "Inventory", "Test Drive"

### Salon / Spa / Fitness / Health
- Tabs: ✗ (flat sections)
- Booking Modal: ✓
- Party Size Field: ✗
- Hero CTA: Opens modal
- Nav: "Services", "Book"

### Car Wash / Pet Care / Home Services
- Tabs: ✗
- Booking Modal: ✓
- Party Size Field: ✗
- Hero CTA: Opens modal
- Nav: "Services", "Book"

### Professional Services
- Tabs: ✗
- Booking Modal: ✓
- Party Size Field: ✗
- Hero CTA: Opens modal
- Nav: "Services", "Contact"

### Other
- Tabs: ✗
- Booking Modal: ✗
- Party Size Field: ✗
- Hero CTA: Direct WhatsApp
- Nav: "Menu", "Contact"

## Validation Checklist

Before deploying, verify:

- [ ] All required fields present
- [ ] `businessType` matches a supported type
- [ ] `whatsappNumber` is digits only (no +, spaces, dashes)
- [ ] `primaryColor` is valid hex (#RRGGBB)
- [ ] All image URLs accessible (test in browser)
- [ ] `mapUrl` is valid Google Maps embed URL
- [ ] `openingHours` has all 7 days
- [ ] `menuData` structure matches `businessType`
- [ ] `textOverrides` includes `other` fallback
- [ ] No trailing commas in JSON
- [ ] Valid JSON (test with `cat config.json | python -m json.tool`)

## Common Issues

### Config Not Loading
- **Cause:** Opening `index.html` directly via `file://`
- **Fix:** Use a local server (`python -m http.server 8000`)

### CORS Error
- **Cause:** Fetching from different origin
- **Fix:** Serve config.json from same domain, or configure CORS headers

### Images Not Showing
- **Cause:** Invalid URLs or CORS on image host
- **Fix:** Use direct image URLs, host on same domain, or use Cloudinary/imgix

### Booking Modal Not Opening
- **Cause:** `businessType` not in modal list
- **Fix:** Check `typesWithModal` array in `script.js`

### Styles Not Applying
- **Cause:** CSS custom properties not supported
- **Fix:** Use modern browser; polyfill not provided

## Example: Minimal Config

```json
{
  "businessName": "My Business",
  "businessType": "other",
  "tagline": "We do great things",
  "primaryColor": "#2563eb",
  "whatsappNumber": "15551234567",
  "currencySymbol": "$",
  "phoneNumber": "+1 (555) 123-4567",
  "email": "hello@mybusiness.com",
  "address": "123 Main St, City, State 12345",
  "heroImage": "https://example.com/hero.jpg",
  "seoDescription": "My Business - We do great things",
  "ogTitle": "My Business",
  "ogDescription": "We do great things",
  "ogImage": "https://example.com/og.jpg",
  "footerAboutText": "My Business has been serving customers since 2020.",
  "socialLinks": {},
  "testimonials": [],
  "openingHours": {
    "Monday": "9:00 AM - 5:00 PM",
    "Tuesday": "9:00 AM - 5:00 PM",
    "Wednesday": "9:00 AM - 5:00 PM",
    "Thursday": "9:00 AM - 5:00 PM",
    "Friday": "9:00 AM - 5:00 PM",
    "Saturday": "Closed",
    "Sunday": "Closed"
  },
  "gallery": [],
  "menuData": {
    "Services": [
      {
        "id": 1,
        "name": "Service 1",
        "description": "Description of service 1",
        "price": "100",
        "images": ["https://example.com/service1.jpg"]
      }
    ]
  },
  "textOverrides": {
    "other": {
      "heroCtaButtonText": "Contact Us",
      "menuSectionTitle": "Our Services",
      "bookingTitle": "Get in Touch",
      "whatsappBookingMessage": "an inquiry"
    }
  }
}
```