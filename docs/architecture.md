# styles — Architecture

## Overview

`@karelhagel/styles` is a **shared SCSS design system** published as a GitHub-hosted npm package. It provides a single SCSS file containing reusable utility classes and component-level CSS used consistently across all Angular frontends in the platform. It has no build step — raw SCSS is installed and compiled by each consuming project.

- **Package name:** `@karelhagel/styles`
- **Version:** 1.0.7 (as of last release)
- **Language:** SCSS
- **Distribution:** GitHub-hosted npm (installed via git URL)
- **License:** MIT

---

## Context Diagram

```
  ┌──────────────────────────────────────────────────────────┐
  │                  @karelhagel/styles                       │
  │                  (GitHub repository)                      │
  └──────┬───────────────────────────────────────────────────┘
         │  npm install via git URL
         │  "https://github.com/karelhagel/styles.git"
         │
         ├──► auth-frontend
         ├──► portfolio-frontend
         ├──► vehicle_maintenance-frontend
         └──► user_management-frontend
                      │
                      ▼
              Angular CLI compiles SCSS
              at build time → CSS bundle
```

---

## Repository Structure

```
/
├── styles.scss          # Single SCSS file — entire design system (734 lines)
├── package.json         # npm manifest (name, version, files: [styles.scss])
├── instructions.md      # Version bump and publish workflow
└── docs/                # Documentation (this file)
```

There is no build pipeline, no compiled output, and no configuration files.

---

## How It Is Consumed

### Installation

```json
// package.json of consuming project
"@karelhagel/styles": "https://github.com/karelhagel/styles.git"
```

Update an existing installation:
```bash
npm update @karelhagel/styles
```

### Import

In each project's `src/styles.scss`:
```scss
@use "@karelhagel/styles/styles" as *;

@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  /* Project-specific overrides */
}
```

The `as *` makes all exported classes available in the global namespace. Tailwind layers are used to manage specificity when both are used together.

---

## Component Catalogue

### Layout

| Class | Description |
|-------|-------------|
| `.root-container` | Max-width 1200px centred container |
| `.panel-border` | Card/panel with border and padding |
| `.panel-panel` | Responsive panel wrapper |

### Forms

| Class | Description |
|-------|-------------|
| `.form-group` | Flexbox field grouping |
| `.form-label` | Field label |
| `.form-input` | Input / textarea with focus state |
| `.select-container` / `.select-box` / `.select-title` | Dropdown wrapper system |
| `.select-form-grid` / `.select-form-row` | Multi-column form grids |

### Tables

| Class | Description |
|-------|-------------|
| `.main-table` | Base table (collapsed, truncating cells) |
| `.table-header-main` / `.table-header-details` | Column headers |
| `.table-group-header` / `.table-account-header` | Account column styling |
| `.table-value-cell` / `.table-sub-header` | Value columns |
| `.table-subtotal` / `.table-subtotal-cell` | Subtotal rows |
| `.table-grand-total` / `.table-grand-total-label` | Grand total rows |
| `.table-empty` | Empty state row |
| `.table-opening-header` / `.table-month-header` | P&L-specific headers |
| `.table-balances-table` | Balances-specific table |

### Modals

| Class | Description |
|-------|-------------|
| `.modal-overlay` | Full-screen backdrop with centering |
| `.modal-content` | Modal body (max-width: 500px) |
| `.modal-content-small` | Smaller variant |
| `.modal-header` / `.modal-title` / `.modal-close` | Header section |
| `.modal-body` / `.modal-footer` | Content sections |
| `.modal-button` | Base button |
| `.modal-button-primary` | Primary action (blue) |
| `.modal-button-secondary` | Secondary action (grey) |
| `.modal-button-danger` | Destructive action (red) |

### Charts

| Class | Description |
|-------|-------------|
| `.base-chart-wrap` | Chart container |
| `.base-chart-header` / `.base-chart-title` | Title area |
| `.base-chart-legend` / `.base-chart-legend-item` / `.base-chart-swatch` | Legend |
| `.base-chart-line` / `.base-chart-hit` | Line and hover target |
| `.base-chart-tooltip-bg` / `.base-chart-tooltip-text` | Tooltip |

### Bulk data entry (spreadsheet UI)

| Class | Description |
|-------|-------------|
| `.bulk-form-container` | 720px-wide container |
| `.bulk-currency-input-wrapper` | Right-aligned currency field |
| `.bulk-balance-input` | Numeric input for balance entry |
| `.bulk-formatted-display` | Read-only formatted display |
| `.bulk-readonly` | Read-only indicator |
| `.bulk-fixed-interest-indicator` | Fixed-interest account label |
| `.bulk-hidden` | `display: none` utility |

### Pagination

| Class | Description |
|-------|-------------|
| `.pagination` | Button group container |
| `.pagination button.active` | Current page highlight |
| `.pagination button:disabled` | Disabled state |

### Messaging

| Class | Description |
|-------|-------------|
| `.warning-message` / `.warning-text` | Warning (red text) |
| `.success-message` | Success (green) |
| `.error-message` | Error (red) |
| `.loading-message` | Loading state |

### Utilities

| Class | Description |
|-------|-------------|
| `.text-left` / `.text-center` / `.text-right` | Text alignment |
| `.bold` | `font-weight: bold` |
| `.action-link` | Link-style button (no background) |
| `.record-details` | Light grey info box |

---

## Design Tokens

There are **no SCSS variables or CSS custom properties** defined. All values are hardcoded in class definitions. Key values used:

| Token | Values |
|-------|--------|
| Primary blue | `#0b5fff`, `#4299e1`, `#3182ce` |
| Error/danger | `#d9534f`, `#e53e3e` |
| Success | `#5cb85c` |
| Neutral text | `#222`, `#333`, `#666` |
| Border colour | `#e2e8f0`, `#cbd5e0` |
| Font family | `Helvetica, Arial, sans-serif` |
| Font sizes | 12px – 24px |
| Modal shadow | `0 20px 60px rgba(0,0,0,0.3)` |

Customisation is handled by consuming projects via CSS overrides in `@layer base` or SCSS nesting.

---

## Versioning & Release

```bash
# Bump patch/minor/major version
npm version patch        # updates package.json + creates git tag

# Push with tag so GitHub sees the new release
git push --follow-tags

# Consuming projects update
npm update @karelhagel/styles
```

There is no CI/CD pipeline or Docker setup — the library is the SCSS source file itself.
