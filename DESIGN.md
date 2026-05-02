---
version: alpha
name: Angular Material (M3)
description: >
  Material Design 3 implementation for Angular. Based on @angular/material v19+.
  Token names match --mat-sys-{name} CSS variables directly.
  All hex values are light-mode defaults using the violet palette.
  Dark-mode values are managed automatically via the CSS light-dark() function
  and the color-scheme property — do not hardcode dark-mode colors separately.

colors:
  # Primary role — key actions, active states, filled buttons
  primary: "#7d00fa"
  on-primary: "#ffffff"
  primary-container: "#ecdcff"
  on-primary-container: "#5f00c0"
  primary-fixed: "#ecdcff"
  primary-fixed-dim: "#d5baff"
  on-primary-fixed: "#270057"
  on-primary-fixed-variant: "#5f00c0"
  inverse-primary: "#d5baff"

  # Secondary role — supporting controls, filter chips, tonal buttons
  secondary: "#645b70"
  on-secondary: "#ffffff"
  secondary-container: "#eadef7"
  on-secondary-container: "#4b4357"
  secondary-fixed: "#eadef7"
  secondary-fixed-dim: "#cec2db"
  on-secondary-fixed: "#1f182a"
  on-secondary-fixed-variant: "#4b4357"

  # Error role — invalid state, destructive actions only
  error: "#b3261e"
  on-error: "#ffffff"
  error-container: "#f9dedc"
  on-error-container: "#8c1d18"

  # Surface role — backgrounds and containers
  background: "#fef8fc"
  on-background: "#1d1b1e"
  surface: "#fef8fc"
  on-surface: "#1d1b1e"
  on-surface-variant: "#49454e"
  surface-variant: "#e8e0eb"
  surface-bright: "#fef8fc"
  surface-dim: "#ded8dd"
  surface-container-lowest: "#ffffff"
  surface-container-low: "#f8f2f6"
  surface-container: "#f2ecf1"
  surface-container-high: "#ede6eb"
  surface-container-highest: "#e6e1e6"
  surface-tint: "#7d00fa"
  inverse-surface: "#323033"
  inverse-on-surface: "#f5eff4"

  # Outline role — borders and dividers
  outline: "#7b757f"
  outline-variant: "#cbc4cf"

  # Utility
  scrim: "#000000"
  shadow: "#000000"

elevation:
  # Shadow levels — six elevation levels (0-5) with progressively stronger shadows
  # Applied as box-shadow; CSS variable names: --mat-sys-level{N}
  level0: "none"
  level1: "0px 2px 6px rgba(0,0,0,0.12)"
  level2: "0px 4px 8px rgba(0,0,0,0.16)"
  level3: "0px 8px 12px rgba(0,0,0,0.20)"
  level4: "0px 12px 16px rgba(0,0,0,0.24)"
  level5: "0px 16px 24px rgba(0,0,0,0.28)"

typography:
  # Display — hero text, one-off large headings (brand font)
  # Token names match --mat-sys-{name}: display-large → var(--mat-sys-display-large)
  display-large:
    fontFamily: Roboto
    fontSize: 57px
    fontWeight: 400
    lineHeight: 64px
    letterSpacing: -0.25px
  display-medium:
    fontFamily: Roboto
    fontSize: 45px
    fontWeight: 400
    lineHeight: 52px
    letterSpacing: 0px
  display-small:
    fontFamily: Roboto
    fontSize: 36px
    fontWeight: 400
    lineHeight: 44px
    letterSpacing: 0px

  # Headline — section titles, page headers (brand font)
  headline-large:
    fontFamily: Roboto
    fontSize: 32px
    fontWeight: 400
    lineHeight: 40px
    letterSpacing: 0px
  headline-medium:
    fontFamily: Roboto
    fontSize: 28px
    fontWeight: 400
    lineHeight: 36px
    letterSpacing: 0px
  headline-small:
    fontFamily: Roboto
    fontSize: 24px
    fontWeight: 400
    lineHeight: 32px
    letterSpacing: 0px

  # Title — card titles, dialog headers, toolbar labels
  title-large:
    fontFamily: Roboto
    fontSize: 22px
    fontWeight: 400
    lineHeight: 28px
    letterSpacing: 0px
  title-medium:
    fontFamily: Roboto
    fontSize: 16px
    fontWeight: 500
    lineHeight: 24px
    letterSpacing: 0.15px
  title-small:
    fontFamily: Roboto
    fontSize: 14px
    fontWeight: 500
    lineHeight: 20px
    letterSpacing: 0.1px

  # Body — reading content, list items, form text (plain font)
  body-large:
    fontFamily: Roboto
    fontSize: 16px
    fontWeight: 400
    lineHeight: 24px
    letterSpacing: 0.5px
  body-medium:
    fontFamily: Roboto
    fontSize: 14px
    fontWeight: 400
    lineHeight: 20px
    letterSpacing: 0.25px
  body-small:
    fontFamily: Roboto
    fontSize: 12px
    fontWeight: 400
    lineHeight: 16px
    letterSpacing: 0.4px

  # Label — buttons, chips, captions, metadata (plain font)
  label-large:
    fontFamily: Roboto
    fontSize: 14px
    fontWeight: 500
    lineHeight: 20px
    letterSpacing: 0.1px
  label-medium:
    fontFamily: Roboto
    fontSize: 12px
    fontWeight: 500
    lineHeight: 16px
    letterSpacing: 0.5px
  label-small:
    fontFamily: Roboto
    fontSize: 11px
    fontWeight: 500
    lineHeight: 16px
    letterSpacing: 0.5px

rounded:
  none: 0px
  xs: 4px      # extra-small — snackbars, tooltips
  sm: 8px      # small — chips, text fields (outlined)
  md: 12px     # medium — cards
  lg: 16px     # large — FAB, datepicker
  xl: 28px     # extra-large — dialogs, side sheets
  full: 9999px # full — buttons, badges, navigation indicators

spacing:
  base: 8px
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  xxl: 48px
  # CSS variables: spacing.xs → --mat-sys-spacing-xs (4px), etc.
  # All values are multiples of the 8px base grid (except xs=4px micro-adjustment)

components:
  # Buttons — five variants in descending emphasis order
  button-filled:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-lg}"
    rounded: "{rounded.full}"
    padding: "10px 24px"
    height: 40px
  button-filled-hover:
    backgroundColor: "{colors.primary}"
  button-tonal:
    backgroundColor: "{colors.secondary-container}"
    textColor: "{colors.on-secondary-container}"
    typography: "{typography.label-lg}"
    rounded: "{rounded.full}"
    padding: "10px 24px"
    height: 40px
  button-elevated:
    backgroundColor: "{colors.surface-container-low}"
    textColor: "{colors.primary}"
    typography: "{typography.label-lg}"
    rounded: "{rounded.full}"
    shadow: "{elevation.level1}"
    padding: "10px 24px"
    height: 40px
  button-outlined:
    backgroundColor: "transparent"
    textColor: "{colors.primary}"
    typography: "{typography.label-lg}"
    rounded: "{rounded.full}"
    padding: "10px 24px"
    height: 40px
  button-text:
    backgroundColor: "transparent"
    textColor: "{colors.primary}"
    typography: "{typography.label-lg}"
    rounded: "{rounded.full}"
    padding: "10px 12px"
    height: 40px

  # Cards — three surface variants
  card-elevated:
    backgroundColor: "{colors.surface-container-low}"
    rounded: "{rounded.md}"
    shadow: "{elevation.level1}"
    padding: "{spacing.lg}"
  card-filled:
    backgroundColor: "{colors.surface-container-highest}"
    rounded: "{rounded.md}"
    padding: "{spacing.lg}"
  card-outlined:
    backgroundColor: "{colors.surface}"
    rounded: "{rounded.md}"
    padding: "{spacing.lg}"

  # Form fields — two appearances
  form-field-filled:
    backgroundColor: "{colors.surface-container-high}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-lg}"
    rounded: "4px 4px 0 0"
  form-field-outlined:
    backgroundColor: "transparent"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-lg}"
    rounded: "{rounded.xs}"

  # Chips — 32px height, small radius
  chip-assist:
    backgroundColor: "transparent"
    textColor: "{colors.on-surface}"
    typography: "{typography.label-lg}"
    rounded: "{rounded.sm}"
    height: 32px
  chip-filter:
    backgroundColor: "{colors.surface-container-low}"
    textColor: "{colors.on-surface-variant}"
    typography: "{typography.label-lg}"
    rounded: "{rounded.sm}"
    height: 32px
  chip-filter-selected:
    backgroundColor: "{colors.secondary-container}"
    textColor: "{colors.on-secondary-container}"
    rounded: "{rounded.sm}"
    height: 32px

  # FAB — floating action button
  fab:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.on-primary-container}"
    rounded: "{rounded.lg}"
    shadow: "{elevation.level3}"
    size: 56px
  fab-small:
    backgroundColor: "{colors.primary-container}"
    textColor: "{colors.on-primary-container}"
    rounded: "{rounded.md}"
    shadow: "{elevation.level3}"
    size: 40px

  # Navigation
  nav-indicator-active:
    backgroundColor: "{colors.secondary-container}"
    textColor: "{colors.on-secondary-container}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
  nav-indicator-inactive:
    backgroundColor: "transparent"
    textColor: "{colors.on-surface-variant}"
    typography: "{typography.label-md}"

  # Feedback components
  dialog:
    backgroundColor: "{colors.surface-container-high}"
    rounded: "{rounded.xl}"
    shadow: "{elevation.level3}"
    padding: "{spacing.xl}"
  snackbar:
    backgroundColor: "{colors.inverse-surface}"
    textColor: "{colors.inverse-on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.xs}"
  tooltip:
    backgroundColor: "{colors.inverse-surface}"
    textColor: "{colors.inverse-on-surface}"
    typography: "{typography.body-sm}"
    rounded: "{rounded.xs}"
  badge:
    backgroundColor: "{colors.error}"
    textColor: "{colors.on-error}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
---

# Angular Material Design System

## Overview

Angular Material implements Google's **Material Design 3 (M3)** specification for Angular
applications. M3 is personal, adaptive, and expressive — built around dynamic color roles,
accessible contrast ratios, and component-level design tokens emitted as CSS variables.

The system targets professional Angular web applications across enterprise and consumer contexts.
It is version-gated: this document covers **@angular/material v19+** and the `mat.theme()` mixin
API. The legacy Material Design 2 API (`mat.define-light-theme`) uses different Sass functions and
is documented separately in `docs/theming-material-2.md`.

**Core principle:** use the `--mat-sys-*` CSS variable system to express all design decisions.
Never hardcode colors, font sizes, or shadows in custom components. Always reference tokens so the
application theme can change without touching component code.

**Light and dark mode** are handled automatically via the CSS `light-dark()` function. Set
`color-scheme: light dark` on `html` to follow system preference. The YAML tokens above are
light-mode reference values. Do not maintain separate dark-mode stylesheets.

Install and configure:

```bash
ng add @angular/material
```

Minimal theme file (`styles.scss`):

```scss
@use '@angular/material' as mat;

html {
  color-scheme: light dark;
  @include mat.theme((
    color: mat.$violet-palette,
    typography: Roboto,
    density: 0,
  ));
  @include mat.system-classes();
}

body {
  background: var(--mat-sys-surface);
  color: var(--mat-sys-on-surface);
}
```

## Colors

M3 uses a **role-based color system**, not a palette-based one. A color role communicates
semantic intent — primary action, error state, surface hierarchy — independently of which
palette is chosen. Swapping palettes (e.g., violet → azure) updates all roles automatically.

Every token in the YAML `colors` section maps directly to a CSS variable:
`colors.primary` → `var(--mat-sys-primary)`. Use CSS variables in custom components, not the
YAML hex values, so themes remain changeable at runtime.

### Color Roles

**Primary** — the most prominent color. Use for filled buttons, selected states, active tab
indicators, checkboxes, and sliders. Do not use primary for decorative purposes.

**Secondary** — supporting color. Use for tonal buttons, selected navigation indicators, filter
chips. Less prominent than primary; provides visual variety without competing for attention.

**Tertiary** — accent color auto-derived from the primary palette. Use sparingly for elements
that need visual distinction from both primary and secondary. Not available in YAML tokens as it
is generated at runtime; reference `var(--mat-sys-tertiary)` directly.

**Error** — invalid state only. Form field error underlines and messages, destructive action
buttons, badges on error states. Never use error color for warnings or neutral notifications.

**Surface** — backgrounds and containers. Six container tiers (`lowest` → `highest`) convey
elevation hierarchy through tonal shift rather than shadow. Higher container tones appear more
elevated.

| Token | Use case |
|---|---|
| `surface-container-lowest` | Page background alternative |
| `surface-container-low` | Elevated cards, side navigation |
| `surface-container` | Menus, dropdowns |
| `surface-container-high` | Filled form fields, filled cards |
| `surface-container-highest` | App bars when scrolled |

**Outline** — borders and dividers. Use `outline` for interactive element boundaries (outlined
buttons, form field borders). Use `outline-variant` for decorative separators (dividers, card
borders on outlined cards).

**Inverse surface** — use for components that must visually pop against the normal surface, such
as snackbars and tooltips.

### Light and Dark Mode

Angular Material does **not** automatically apply `prefers-color-scheme`. You control the
`color-scheme` property:

```scss
html { color-scheme: light dark; }  /* follows system preference */
html { color-scheme: light; }       /* always light */
body.dark-mode { color-scheme: dark; } /* toggled via class */
```

## Typography

M3 defines **five type categories**, each with three sizes. Two font families are configured:
`plain-family` for body and label text; `brand-family` for display and headline text.

| Category | Sizes | Purpose |
|---|---|---|
| Display | lg / md / sm | Hero text, marketing headings — brand font |
| Headline | lg / md / sm | Section titles, page-level headers — brand font |
| Title | lg / md / sm | Card titles, dialog headers, toolbar labels |
| Body | lg / md / sm | Reading content, list items, form inputs |
| Label | lg / md / sm | Buttons, chips, captions, input labels |

Use `var(--mat-sys-{level})` in custom component stylesheets:

```scss
.my-card-title {
  font: var(--mat-sys-title-large);
}
.my-caption {
  font: var(--mat-sys-body-small);
  letter-spacing: var(--mat-sys-body-small-tracking);
}
```

Configure typography via `mat.theme()`:

```scss
@include mat.theme((
  typography: (
    plain-family: Roboto,
    brand-family: 'Your Brand Font',
    bold-weight: 700,
    medium-weight: 500,
    regular-weight: 400,
  ),
));
```

Load fonts before using them (Google Fonts example):

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap"
      rel="stylesheet">
```

Utility classes (requires `mat.system-classes()`):

| Class | Level |
|---|---|
| `.mat-font-body-sm/md/lg` | body-small / medium / large |
| `.mat-font-label-sm/md/lg` | label-small / medium / large |
| `.mat-font-title-sm/md/lg` | title-small / medium / large |
| `.mat-font-headline-sm/md/lg` | headline-small / medium / large |
| `.mat-font-display-sm/md/lg` | display-small / medium / large |

## Layout

Angular Material does not impose a grid system. Use your own grid; Material components adapt to
whatever layout they are placed in.

### Spacing Token Reference

All spacing follows an **8px base grid**, except `xs` (4px micro-adjustment). Use CSS variables in code; reference this table when designing:

| Token | Pixel Value | CSS Variable | Typical Use Cases |
|-------|-------------|--------------|-------------------|
| **xs** | 4px | `--mat-sys-spacing-xs` | Icon-to-label gaps, micro-spacing within components |
| **sm** | 8px | `--mat-sys-spacing-sm` | Small component padding, adjacent element gaps |
| **md** | 16px | `--mat-sys-spacing-md` | Section padding, moderate gaps between groups |
| **lg** | 24px | `--mat-sys-spacing-lg` | Major section gaps, card padding |
| **xl** | 32px | `--mat-sys-spacing-xl` | Large section gaps, hero section padding |
| **xxl** | 48px | `--mat-sys-spacing-xxl` | Extra-large gaps, full-width sections |

**Usage in CSS:**
```scss
.my-component {
  padding: var(--mat-sys-spacing-lg);  // 24px
  gap: var(--mat-sys-spacing-md);      // 16px between flex children
  margin-bottom: var(--mat-sys-spacing-lg);  // ❌ DON'T — let parent control margins
}
```

**Grid Philosophy:** The 8px grid creates mathematical rhythm. Never use 5px, 7px, 13px. When you need fine-tuning, use `xs` (4px) for micro-adjustments, not arbitrary values.

**Spacing** follows an **8px base grid**. All layout measurements should be multiples of 8px.
Use 4px (`spacing.xs`) only for micro-adjustments within a component (icon-to-label gap, input
padding). Expose the 8px grid via the token: `var(--mat-sys-spacing)` is not emitted by default;
use the YAML `spacing.*` values as your reference scale.

**Density** controls component internal size (height, padding), not layout. Configured via
`mat.theme()`:

```scss
@include mat.theme((density: 0));   /* default — recommended for most apps */
@include mat.theme((density: -1));  /* slightly compact */
@include mat.theme((density: -2));  /* compact — dashboards, data-dense UIs */
```

Density range: `0` (default) to `-5` (most compact). Each step reduces affected sizes by 4px.
Never go below `-2` for standard user-facing interfaces — lower values impair touch targets and
accessibility. Density does not affect task/popup contexts (datepicker, dialog, tooltip, menu).

## Elevation & Depth

M3 communicates depth through **tonal elevation** as the primary signal and **shadows** as a
secondary signal. Tonal elevation uses `surface-tint` mixed into surface containers — higher
containers appear slightly more chromatic, implying they sit above the page surface.

### Elevation Levels and Shadow Values

All shadows in Material Design 3 follow a consistent progression. Use these exact box-shadow values:

| Level | Box-Shadow | Blur | Offset | Use Case |
|-------|-----------|------|--------|----------|
| **0** | none | — | — | Flush surfaces, no separation (background, main surface) |
| **1** | `0px 2px 6px rgba(0,0,0,0.12)` | 6px | 2px down | Slight elevation (empty state, subtle cards) |
| **2** | `0px 4px 8px rgba(0,0,0,0.16)` | 8px | 4px down | Raised components (cards, chips, FAB at rest) |
| **3** | `0px 8px 12px rgba(0,0,0,0.20)` | 12px | 8px down | Floating components (menus, select panels, FAB at rest) |
| **4** | `0px 12px 16px rgba(0,0,0,0.24)` | 16px | 12px down | Hovered/focus state (FAB on hover, elevated dialog) |
| **5** | `0px 16px 24px rgba(0,0,0,0.28)` | 24px | 16px down | Maximum emphasis (modal feedback, critical interactions) |

**Component Elevation Mapping:**

| Component | Default Shadow | Hover Shadow | Notes |
|-----------|---|---|---|
| **Card** (elevated) | level1 | level2 | Raised default, slight emphasis on hover |
| **Card** (outlined) | level0 | level0 | No shadow; relies on outline border |
| **Button** (filled) | level0 | level1 | Flat default, slight lift on hover |
| **Button** (elevated) | level1 | level2 | Pre-elevated; stronger on hover |
| **Menu/Select** | level3 | level3 | Floating by default; no hover change |
| **Dialog** | level4 | level4 | High elevation; fixed |
| **FAB** (standard) | level3 | level4 | Floating; lifts on hover |
| **Snackbar** | level3 | level3 | Floating; no interaction |
| **Chip** (elevated) | level1 | level1 | Optional shadow |
| **Bottom sheet** | level3 | level3 | Floating overlay |

**CSS Usage:**
```scss
.mat-card-elevated {
  box-shadow: var(--mat-sys-level1);  // Default
  
  &:hover {
    box-shadow: var(--mat-sys-level2);  // On hover
  }
}

.mat-fab {
  box-shadow: var(--mat-sys-level3);
  
  &:hover,
  &:focus {
    box-shadow: var(--mat-sys-level4);
  }
}
```

Shadow levels supplement tonal elevation for components that physically float above the layout:

| Level | Token | Use case |
|---|---|---|
| 0 | `--mat-sys-level0` | Flat surfaces — filled cards, table rows |
| 1 | `--mat-sys-level1` | Slightly elevated — elevated cards, slider handle |
| 2 | `--mat-sys-level2` | Raised — menus, select panels, autocomplete |
| 3 | `--mat-sys-level3` | Floating — FAB at rest |
| 4 | `--mat-sys-level4` | Hovered/focused FAB |
| 5 | `--mat-sys-level5` | Maximum — reserved for interaction feedback only |

Apply in custom components via `box-shadow`:

```scss
.my-floating-panel {
  box-shadow: var(--mat-sys-level2);
}
```

Shadow utility classes (requires `mat.system-classes()`): `.mat-shadow-1` through `.mat-shadow-5`.

Prefer tonal surface tokens over shadows for cards and containers. Use shadows only when a
component must visually detach from all underlying surfaces (menus, FABs, dialogs).

## Shapes

### Corner Radius Token Reference

Material Design 3 defines **7 standard corner sizes**. Each communicates visual hierarchy and component personality:

| Size | Pixel Value | CSS Variable | Components | Visual Meaning |
|------|------------|---|---|---|
| **None** | 0 | `--mat-sys-corner-none` | Dividers, full-width bottom sheets | No rounding — structural, spanning |
| **Extra-small** | 4px | `--mat-sys-corner-extra-small` | Snackbars, tooltips, small indicators | Minimal rounding — tight, dense |
| **Small** | 8px | `--mat-sys-corner-small` | Chips, outlined text fields, small buttons | Compact rounding — interactive, grouped |
| **Medium** | 12px | `--mat-sys-corner-medium` | Cards, elevated buttons, medium containers | Standard rounding — balanced, friendly |
| **Large** | 16px | `--mat-sys-corner-large` | FABs (standard), menus, large containers | Prominent rounding — emphasis, floating |
| **Extra-large** | 28px | `--mat-sys-corner-extra-large` | Dialogs, bottom sheets, modals | Maximum rounding — full-screen, immersive |
| **Full** | 9999px | `--mat-sys-corner-full` | FABs (small), badges, pill shapes | Fully rounded — badges, toggles |

**Usage in CSS:**
```scss
.mat-card {
  border-radius: var(--mat-sys-corner-medium);  // 12px
}

.mat-dialog {
  border-radius: var(--mat-sys-corner-extra-large);  // 28px
}

.mat-fab {
  border-radius: var(--mat-sys-corner-large);  // 16px (standard)
}

.mat-badge {
  border-radius: var(--mat-sys-corner-full);  // 9999px (fully rounded)
}
```

**Rule:** Never use arbitrary border-radius values. Always pick from the 7 standard sizes above.

M3 corner radius communicates component personality and hierarchy. Angular Material maps shape
to seven tiers. Directional variants exist for components that are only rounded on some sides:
`--mat-sys-corner-large-top`, `--mat-sys-corner-large-start`, `--mat-sys-corner-large-end`.

**Never mix rounded and sharp corners within a single component.** Do not override a component's
corner radius with a tier that contradicts its category (e.g., do not apply `corner-none` to a
button, or `corner-full` to a card).

## Components

### Buttons

Five variants in descending emphasis order. Use the highest emphasis variant that the action
warrants. **Never place two filled buttons side by side** — that signals equal importance and
confuses hierarchy.

| Variant | Selector | Emphasis | Background | Text |
|---|---|---|---|---|
| Filled | `<button mat-flat-button>` | Highest | primary | on-primary |
| Tonal | `<button mat-button color="secondary">` | High | secondary-container | on-secondary-container |
| Elevated | `<button mat-raised-button>` | Medium | surface-container-low | primary |
| Outlined | `<button mat-stroked-button>` | Low | transparent | primary |
| Text | `<button mat-button>` | Lowest | transparent | primary |

All buttons: `border-radius: full`, `height: 40px`, `label-large` typography, `10px 24px`
padding (text variant: `10px 12px`). Icon buttons: `40px × 40px`, `border-radius: full`.

### Button States (All Variants)

Every button variant responds to user interaction. This table shows color and styling changes per state:

| Variant | Default BG | Hover BG | Focus BG | Pressed BG | Disabled BG | Disabled Text |
|---------|-----------|----------|----------|-----------|------------|---|
| **Filled** | primary | primary (darker) | primary | primary (darker) | surface-container-high | on-surface-variant (30% opacity) |
| **Tonal** | secondary-container | secondary-container (darker) | secondary-container | secondary-container (darker) | surface-container-high | on-surface-variant (30% opacity) |
| **Elevated** | surface-container-low | surface-container-low (darker) | surface-container-low | surface-container-low (darker) | surface-container-high | on-surface-variant (30% opacity) |
| **Outlined** | transparent | surface-container-low | transparent | surface-container-low | transparent | on-surface-variant (30% opacity) |
| **Text** | transparent | surface-container-low | transparent | surface-container-low | transparent | on-surface-variant (30% opacity) |

**State Details:**

| State | Visual Indicator | Implementation |
|-------|---|---|
| **Default** | Resting state | No additional styling |
| **Hover** | Background color shift (darker) | `:hover` → 8% darker shade of background color |
| **Focus** | Outline + color shift | `:focus-visible` → 2px primary color outline + darker background |
| **Pressed** | Stronger color shift + shadow | `:active` → 12% darker shade + level1 shadow |
| **Disabled** | Muted colors, no interaction | `:disabled` → surface-container-high background, 30% opacity text |

**CSS Example:**
```scss
button[mat-flat-button] {
  background-color: var(--mat-sys-primary);
  color: var(--mat-sys-on-primary);
  
  &:hover {
    background-color: var(--mat-sys-primary-hover);  // Darker shade
  }
  
  &:focus-visible {
    outline: 2px solid var(--mat-sys-primary);
    outline-offset: 2px;
  }
  
  &:active {
    background-color: var(--mat-sys-primary-pressed);  // Even darker
    box-shadow: var(--mat-sys-level1);
  }
  
  &:disabled {
    background-color: var(--mat-sys-surface-container-high);
    color: var(--mat-sys-on-surface-variant);
    opacity: 0.38;
  }
}
```

### Form Fields

Two appearances controlled by `appearance` input:

**Filled** (`appearance="fill"`) — `surface-container-high` background, rounded top corners
(4px), flat bottom with active indicator line. Default. Use in most forms.

**Outlined** (`appearance="outline"`) — transparent background, full border, `extra-small` (4px)
corner radius. Use when the form sits on a surface that has the same color as the filled field.

Both appearances support: floating label, prefix/suffix icons, hint text, error messages.
The `<mat-form-field>` wrapper provides these; the inner control (`matInput`, `mat-select`, etc.)
does not render them independently.

### Cards

Three variants via the `appearance` input on `<mat-card>`:

| Variant | Background | Shadow |
|---|---|---|
| Elevated (default) | `surface-container-low` | level1 |
| Filled | `surface-container-highest` | none |
| Outlined | `surface` | none + `outline-variant` border |

All cards: `corner-medium` (12px) radius. Use cards to group related content. Do not use cards
as list items — use `<mat-list>` instead.

### Chips

Four types, all `32px` height, `corner-small` (8px) radius, `label-large` typography:

| Type | Selector | Use case |
|---|---|---|
| Assist | `<mat-chip>` | Suggest actions related to content |
| Filter | `<mat-chip-listbox>` | Filter content; toggles selected/unselected state |
| Input | `<mat-chip-grid>` | Represent discrete items entered by the user |
| Suggestion | `<mat-chip-set>` | Dynamically generated suggestions |

Selected filter chips: `secondary-container` background.

### Navigation

Choose the navigation pattern based on destination count and screen size:

| Pattern | Component | Destinations | Placement |
|---|---|---|---|
| Top app bar | `<mat-toolbar>` | — | Always visible header |
| Navigation bar | `<mat-tab-nav-bar>` | 3–5 | Bottom of screen (mobile) |
| Navigation rail | Custom with CDK | 3–7 | Left side (tablet) |
| Navigation drawer | `<mat-sidenav>` | 5+ | Left side (desktop) |

Active navigation indicator: `secondary-container` background, `corner-full` radius.
Inactive label: `on-surface-variant`.

### Dialogs

Use `MatDialog.open()` to launch. Background: `surface-container-high`, `corner-extra-large`
(28px) radius. Structure: icon (optional) → headline → supporting text → actions.

Actions: text buttons only inside dialogs. Never use filled or elevated buttons in a dialog —
the dialog surface itself provides the necessary elevation emphasis.

### Feedback Components

**Snackbar** — `inverse-surface` background, `inverse-on-surface` text, `corner-extra-small`
radius. Single line of `body-medium` text. One optional action button (`inverse-primary` text
color). Auto-dismiss after 4–10 seconds.

**Tooltip** — `inverse-surface` background, `body-small` text, `corner-extra-small` radius.
Appears on hover/focus after 500ms. Maximum 1 line of text.

**Badge** — `error` background (for counts/alerts) or `primary` (for status). `corner-full`
radius. `label-small` typography. Position: top-right of the host element.

### FAB (Floating Action Button)

Two sizes: standard (56px) and small (40px). Background: `primary-container`.
Text/icon: `on-primary-container`. Shadow: level3 at rest, level4 on hover.
Corner radius: `corner-large` (16px) for standard, `corner-medium` (12px) for small.

Use FAB only for the single most important action on a screen. Never show more than one FAB
per screen.

## Do's and Don'ts

### Theming

- **Do** configure all theming via `mat.theme()` — never modify generated CSS class internals
- **Do** place every `@include mat.theme(...)` inside a CSS selector: `html { @include mat.theme(...); }`
- **Do** call `mat.system-classes()` inside the same selector to enable utility classes
- **Do** use `mat.theme-overrides()` or `mat.{component}-overrides()` for targeted token changes
- **Do** use `--mat-sys-*` CSS variables in custom component stylesheets to inherit the theme
- **Don't** override `--mat-sys-*` variables directly in plain CSS — use the Sass override APIs
- **Don't** reference `@angular/material` CSS class internals (`.mat-mdc-*`) — they are private

### Component Code

- **Do** use the `host` object in `@Component`/`@Directive` config for host bindings:
  ```ts
  @Component({ host: { '[class.active]': 'isActive' } })
  ```
- **Don't** use `@HostBinding` or `@HostListener` — they cause type-preservation issues in SSR
- **Do** use `@Input({transform: booleanAttribute})` for boolean inputs:
  ```ts
  @Input({transform: booleanAttribute}) disabled: boolean = false;
  ```
- **Don't** use `coerceBooleanProperty()` — it is legacy CDK; `booleanAttribute` is the Angular
  built-in equivalent
- **Do** expose native inputs via `ng-content`, not wrapped in template `<input>` elements
- **Don't** use class inheritance for shared component behaviors — use TypeScript mixins

### Custom Form Field Controls

- **Do** implement the full `MatFormFieldControl<T>` interface when building custom form controls
- **Do** use a `Subject<void>` for `stateChanges` and emit on every property change that
  affects form field appearance
- **Do** use `ngDoCheck` with an `updateErrorState()` method — a simple getter misses parent
  form submission triggers
- **Do** accept `aria-describedby` as an `@Input` and merge it in `setDescribedByIds()`

### CSS and SCSS

- **Do** prioritize lowest CSS specificity — flat selectors, no nesting for organization
- **Do** use class selectors: `.mat-mdc-slider` — not tag selectors: `mdc-slider`
- **Do** support Windows high-contrast mode: `@include cdk-high-contrast(active, off) { ... }`
- **Don't** set `margin` on a component's host element — leave that to the consumer
- **Don't** use `display: flex` on a component's outermost element
- **Don't** use SCSS nesting purely for code organization — it increases specificity unnecessarily

### Accessibility

- **Do** set `color-scheme: light dark` to ensure the browser UI (scrollbars, inputs) matches
- **Do** use `BidiModule` and `Directionality` for RTL-aware custom components
- **Do** include `role="group"` and `aria-labelledby` on multi-input custom controls
- **Do** call `mat.strong-focus-indicators()` when WCAG AA focus visibility is required
- **Don't** set density below `-2` — smaller touch targets fail WCAG success criterion 2.5.5

### Icons

- **Do** use `MatIconRegistry` to register custom SVG icons with `DomSanitizer`
- **Do** use `mat-icon` with `fontSet` for non-Material icon libraries
- **Don't** inline SVG directly in templates — register and reference via `mat-icon`

## Agent Prompt Guide

### Quick Color Reference
| Role | Hex | CSS Variable |
|------|-----|--------------|
| Primary | `#7d00fa` | `--mat-sys-primary` |
| On Primary | `#ffffff` | `--mat-sys-on-primary` |
| Surface | `#fef8fc` | `--mat-sys-surface` |
| On Surface | `#1d1b1e` | `--mat-sys-on-surface` |
| Secondary Container | `#eadef7` | `--mat-sys-secondary-container` |
| Outline | `#7b757f` | `--mat-sys-outline` |

### Example Component Prompts

**Elevated Button:**
"Angular Material elevated button (`mat-raised-button`). Background: var(--mat-sys-surface-container-low), text: var(--mat-sys-primary), shadow: var(--mat-sys-level1), radius: var(--mat-sys-corner-full)."

**Standard Card:**
"Angular Material card (`mat-card`). Background: var(--mat-sys-surface-container-low), shadow: var(--mat-sys-level1), radius: var(--mat-sys-corner-medium) (12px). Padding: var(--mat-sys-spacing-lg) (24px)."

**Outlined Form Field:**
"Angular Material form field (`mat-form-field`) with `appearance=\"outline\"`. Border: var(--mat-sys-outline), radius: var(--mat-sys-corner-extra-small) (4px). Typography: var(--mat-sys-body-large)."

### Iteration Tips
1. **Never hardcode hex values** in component CSS. Always use `var(--mat-sys-*)` tokens.
2. **Use light-dark()** for color properties that must adapt to theme: `color: light-dark(var(--mat-sys-primary), var(--mat-sys-inverse-primary))`.
3. **8px Grid:** All spacing and padding should use `var(--mat-sys-spacing-*)` variables.
4. **Corner Radius:** Only use the 7 standard levels: `none`, `extra-small`, `small`, `medium`, `large`, `extra-large`, `full`.
5. **Tonal Elevation:** Prefer `surface-container` tiers over box-shadows for grouping content.
