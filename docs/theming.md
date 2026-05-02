# Theming Angular Material (M3 — v19+)

> Source: https://material.angular.dev/guide/theming — https://github.com/angular/components/blob/main/guides/theming.md
>
> This covers the **current** M3 API (`mat.theme` mixin, v19+). For the legacy M2 API see [theming-material-2.md](./theming-material-2.md).

## Core Concept

`mat.theme()` outputs CSS variables (`--mat-sys-*`) that drive all component styles. Variables use
the `light-dark()` CSS function so light/dark mode is handled via `color-scheme`.

## Minimal Theme Setup

```scss
@use '@angular/material' as mat;

html {
  color-scheme: light dark;
  @include mat.theme((
    color: mat.$violet-palette,
    typography: Roboto,
    density: 0
  ));
}
```

Apply surface/text defaults across the app:

```scss
body {
  background: var(--mat-sys-surface);
  color: var(--mat-sys-on-surface);
}
```

## Color

### Single Palette (simplest)

```scss
@include mat.theme((color: mat.$violet-palette, ...));
```

Uses the palette for primary, secondary, and tertiary. Colors are defined with `light-dark()`.

### Color Map (separate tertiary + theme-type)

```scss
@include mat.theme((
  color: (
    primary: mat.$violet-palette,
    tertiary: mat.$orange-palette,
    theme-type: light,   // 'light' | 'dark' | 'color-scheme'
  ),
  ...
));
```

`theme-type: color-scheme` (default) uses `light-dark()`. Use `light` or `dark` to lock the mode
for browsers that don't support `light-dark()`.

### Prebuilt Color Palettes

```
$red-palette       $green-palette      $blue-palette
$yellow-palette    $cyan-palette       $magenta-palette
$orange-palette    $chartreuse-palette $spring-green-palette
$azure-palette     $violet-palette     $rose-palette
```

### Custom Palettes

```bash
ng generate @angular/material:theme-color
```

## Typography

### Single Font Family

```scss
@include mat.theme((typography: Roboto, ...));
```

### Typography Map

```scss
@include mat.theme((
  typography: (
    plain-family: Roboto,
    brand-family: 'Open Sans',
    bold-weight: 900,
    medium-weight: 500,
    regular-weight: 300,
  ),
  ...
));
```

### Loading Fonts (Google Fonts example)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
```

## Density

Accepts integers `0` to `-5`. Each step reduces sizes by 4px.

```scss
@include mat.theme((density: -2, ...));
```

Setting below `0` reduces accessibility. Does not affect task/popup components (e.g., datepicker).

## Prebuilt CSS Themes

Four M3 themes, four legacy M2 themes:

| Theme | System | Mode | Palettes |
|---|---|---|---|
| `azure-blue.css` | M3 | Light | azure, blue |
| `rose-red.css` | M3 | Light | rose, red |
| `cyan-orange.css` | M3 | Dark | cyan, orange |
| `magenta-violet.css` | M3 | Dark | magenta, violet |
| `deeppurple-amber.css` | M2 | Light | deep-purple, amber |
| `indigo-pink.css` | M2 | Light | indigo, pink |
| `pink-bluegrey.css` | M2 | Dark | pink, blue-grey |
| `purple-green.css` | M2 | Dark | purple, green |

```json
"styles": ["@angular/material/prebuilt-themes/azure-blue.css"]
```

## Light / Dark Mode

```scss
// Follow system preference
html { color-scheme: light dark; }

// Lock to light
html { color-scheme: light; }

// Switch via CSS class
html { color-scheme: light; }
body.dark-mode { color-scheme: dark; }
```

Angular Material does NOT automatically apply `prefers-color-scheme` — that's intentional so you
control the behavior.

## Multiple Themes (Context-Specific)

```scss
html {
  @include mat.theme((color: mat.$violet-palette, typography: Roboto, density: 0));
}

.danger-zone {
  @include mat.theme((color: mat.$cyan-palette));
}
```

## Using Theme Styles in Custom Components

Use CSS variables directly:

```scss
.my-component {
  background: var(--mat-sys-primary-container);
  color: var(--mat-sys-on-primary-container);
  border: 1px solid var(--mat-sys-outline-variant);
  font: var(--mat-sys-body-large);
}
```

Or utility classes (requires `mat.system-classes()`):

```html
<div class="mat-bg-primary-container mat-text-on-primary-container mat-border-variant mat-font-body-lg"></div>
```

## Customizing Tokens

### System Token Overrides

```scss
html {
  @include mat.theme((...));

  .custom-section {
    @include mat.theme-overrides((primary-container: #84ffff));
  }
}
```

Or inline in `mat.theme`:

```scss
@include mat.theme((...), $overrides: (primary-container: orange));
```

### Component Token Overrides

Each component exposes an `overrides` mixin:

```scss
html {
  @include mat.card-overrides((
    elevated-container-color: red,
    elevated-container-shape: 32px,
    title-text-size: 2rem,
  ));
}
```

Do **not** override component CSS classes directly — they are private implementation details.

## Strong Focus Indicators (Accessibility)

```scss
html {
  @include mat.theme((...));
  @include mat.strong-focus-indicators();
}
```

Customize:

```scss
@include mat.strong-focus-indicators((
  border-color: red,
  border-style: dotted,
  border-width: 4px,
  border-radius: 2px,
));
```

## Shadow DOM

Theme styles must be loaded within each shadow root containing Angular Material components (manual
CSS load or Constructable Stylesheets).
