# HTML Email Template System

A production-ready, modular HTML email template system built on top of the [Acorn Email Framework](https://github.com/ThemeMountain/acorn). Designed for rapid campaign development — every component is copy-paste ready, tested across major email clients, and built for repurposing across campaigns.

## Why This Exists

Building HTML emails from scratch for every campaign is slow. This system provides a **library of battle-tested, modular components** that can be assembled into any email layout in minutes. Need a promotional email with a hero image, 3-column feature section, testimonial, and CTA? Grab the components, drop them into the boilerplate, and customize.

## Architecture

```
email-template-system/
│
├── boilerplate/            # Starter HTML skeleton with all resets & responsive CSS
│   └── boilerplate.html
│
├── grid/                   # Column layout systems (golden ratio, 600px container)
│   ├── 1-column.html
│   ├── 2-columns.html
│   ├── 3-columns.html
│   ├── 4-columns.html
│   ├── 1-3-columns.html    # Sidebar left (138px / 414px)
│   └── 3-1-columns.html    # Sidebar right (414px / 138px)
│
├── components/             # Reusable email blocks — copy, paste, customize
│   ├── accordion/          # Interactive expand/collapse (CSS-only, mobile)
│   ├── alerts/             # Background color & outlined alert bars
│   ├── buttons/            # Filled, outlined, pill — bulletproof for Outlook
│   ├── coupons/            # Dashed, filled, image-left promo blocks
│   ├── divider/            # Horizontal rule with consistent spacing
│   ├── feature-columns/    # Side-by-side feature highlights
│   ├── labels/             # Inline filled & outlined label spans
│   ├── navigation/         # Basic horizontal nav + hamburger menu (mobile)
│   ├── pricing-tables/     # 2-col & 3-col, boxed & full-width variants
│   ├── spacer/             # Table, row, and universal spacer patterns
│   ├── stats/              # Stat counters — text, boxed, background image
│   ├── testimonials/       # Avatar, border, and icon quote styles
│   └── timeline/           # Vertical timeline for history/milestones
│
├── responsive/             # Advanced responsive & Outlook-specific patterns
│   ├── 1-col-centered-on-desktop.html
│   ├── bkg-image.html                  # CSS + VML background images
│   ├── fluid-retina-image.html         # 2x retina with fluid scaling
│   ├── mobile-reorder-2col.html        # Reverse stack order on mobile
│   ├── mobile-reorder-3col.html        # 3-column reorder on mobile
│   └── vml-body-bkg-image.html         # Full-body VML background (Outlook)
│
└── docs/                   # QA checklists, compatibility, personalization guide
    ├── qa-checklist.md
    ├── email-client-compatibility.md
    └── personalization-guide.md
```

## How To Use

### 1. Start with the boilerplate
Copy `boilerplate/boilerplate.html` — it includes all DOCTYPE declarations, MSO conditionals, viewport meta tags, the responsive CSS framework, and the 600px container wrapper.

### 2. Pick a grid layout
Choose a column structure from `grid/` and paste it inside the `<!-- ADD ROWS HERE -->` comment in the boilerplate. Stack multiple grids for complex layouts.

### 3. Drop in components
Browse `components/` for the blocks you need. Each file is a self-contained HTML snippet — paste it into a grid column and customize colors, copy, and images.

### 4. Customize & send
Update brand colors, copy, images, and links. The responsive CSS classes from the boilerplate handle mobile adaptation automatically.

## Grid System

Based on a **golden ratio typography grid** within a 600px container:

| Columns | Widths | Use Case |
|---------|--------|----------|
| 1 col | 552px (full) | Hero, full-width content |
| 2 col | 276px / 276px | Side-by-side features |
| 3 col | 184px / 184px / 184px | Product grids, pricing |
| 4 col | 138px / 138px / 138px / 138px | Icon rows, social links |
| 1-3 | 138px / 414px | Thumbnail + text |
| 3-1 | 414px / 138px | Text + thumbnail |

All columns stack to full-width on mobile (≤480px) with configurable reorder using `stack-sm-first` and `stack-sm-last` classes.

## Key Technical Features

- **Outlook/MSO compatibility** — VML background images, `mso-padding-alt`, conditional CSS, `OfficeDocumentSettings` for DPI
- **Bulletproof buttons** — `<th>` + `<a>` pattern with MSO padding fallbacks
- **Responsive breakpoints** — 632px (container fluid) and 480px (column stacking)
- **Retina support** — 2x images with `width` attribute for fluid scaling
- **Mobile column reorder** — `display: table-header-group` / `table-footer-group` for source-order-independent stacking
- **Interactive components** — CSS-only accordion and hamburger nav for supported clients
- **System font stack** — `-apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto` with web font fallback

## Responsive Utility Classes

| Class | Effect |
|-------|--------|
| `col-sm-1` through `col-sm-3` | Column width on mobile (25%–75%) |
| `stack-sm-first` / `stack-sm-last` | Reorder columns on mobile |
| `show-sm` / `hide-sm` | Toggle visibility on mobile |
| `text-sm-center` / `text-sm-left` / `text-sm-right` | Text alignment on mobile |
| `p-sm-0` through `p-sm-24` | Padding overrides on mobile |
| `align-sm-center` | Center block elements on mobile |

## Email Client Compatibility

Tested with [Email on Acid](https://www.emailonacid.com). See `docs/email-client-compatibility.md` for the full matrix.

**Primary support:** Gmail (web/mobile), Apple Mail, Outlook 2016–2021+, Outlook.com, Yahoo Mail, Samsung Mail, iOS Mail

## Documentation

- **[QA Checklist](docs/qa-checklist.md)** — Pre-send validation steps for rendering, links, accessibility, and personalization
- **[Email Client Compatibility](docs/email-client-compatibility.md)** — Client support matrix and known quirks
- **[Personalization Guide](docs/personalization-guide.md)** — Dynamic content, merge tags, conditional logic patterns

## Credits

Grid system and responsive framework based on [Acorn by ThemeMountain](https://github.com/ThemeMountain/acorn). Components built and tested for production campaign use.
