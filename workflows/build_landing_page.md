# Workflow: Build Landing Page

## Objective
Generate a modern, brand-consistent single-page HTML landing page from a business config and brand assets.

## Required Inputs
| Input | Source | Notes |
|---|---|---|
| Business config | `config/<business>.json` | Name, services, contact, hours, colors, fonts |
| Logo | `brand_assets/<logo>.png` | Relative path from project root |
| Brand guidelines | `brand_assets/<guidelines>.png` | Read visually to extract colors, fonts, style |

## Steps

### 1. Read brand assets
Open the logo and guidelines images to extract:
- Primary and accent colors (hex codes)
- Font families
- Button style, overall aesthetic (dark/light)

### 2. Check for existing config
- Look in `config/` for a JSON file for this business
- If it exists, read it and proceed to step 4
- If not, create it using the schema below

### 3. Create/update business config
- Populate all fields with real values — no "TBD" placeholders
- Colors must be hex codes derived from brand assets
- List every service with name, description, price, and duration

### 4. Build the HTML
- For static HTML with no external API calls: write `index.html` directly
- For pages requiring data from APIs or external sources: build a Python tool in `tools/`
- Use CSS custom properties (`--var`) so brand colors are defined once and applied everywhere
- Embed fonts via Google Fonts `<link>` tag

### 5. Verify
- Open `index.html` in a browser
- Confirm logo path resolves (relative from project root)
- Confirm no placeholder text remains
- Confirm colors match brand guidelines

## Config Schema (`config/<business>.json`)
```json
{
  "business": { "name": "", "tagline": "", "description": "" },
  "brand": {
    "logo": "brand_assets/logo.png",
    "colors": {
      "background": "#hex", "background_mid": "#hex", "background_card": "#hex",
      "accent": "#hex", "accent_dim": "#hex",
      "gold": "#hex", "gold_light": "#hex",
      "text": "#hex"
    },
    "fonts": { "primary": "Roboto Mono", "secondary": "Montserrat" }
  },
  "stats": [{ "number": "5K+", "label": "Happy Clients" }],
  "services": [{
    "icon": "🦶", "name": "", "description": "",
    "price": "from $45", "duration": "60 min", "featured": false
  }],
  "testimonials": [{
    "initials": "SM", "name": "", "info": "", "rating": 5, "text": ""
  }],
  "contact": {
    "address": "", "phone": "", "email": "", "hours_summary": "",
    "hours": [{ "day": "Mon – Fri", "time": "9AM – 9PM" }]
  }
}
```

## Lessons Learned
- **Logo path**: Always relative from project root (e.g. `brand_assets/logo.png`)
- **Google Fonts**: Requires internet at runtime — embed `<link>` in `<head>`
- **Static HTML**: No build tool needed — write `index.html` directly. Python tools are reserved for API calls and data pipelines.
- **Color fallback**: If guidelines don't specify a role, use dark navy bg + cyan accent + white text
