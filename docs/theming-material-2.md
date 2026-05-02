# Theming Angular Material 2 (Legacy M2 API)

> Source: https://material.angular.dev/guide/material-2-theming — https://github.com/angular/components/blob/main/guides/material-2.md
>
> **This is the legacy M2 API.** New projects should use the [M3 theming guide](./theming.md).
> For migration instructions see the section at the bottom of this file.

## Palettes

An M2 palette is a Sass map of hues (50, 100–900) with contrast colors:

```scss
$m2-indigo-palette: (
  50: #e8eaf6,
  100: #c5cae9,
  // ...
  contrast: (
    50: rgba(black, 0.87),
    // ...
  )
);
```

Angular Material ships predefined M2 palettes (2014 Material Design spec). Access them via
`mat.$m2-indigo-palette`, `mat.$m2-pink-palette`, etc.

Custom palettes: [material palette tool](https://m2.material.io/design/color/the-color-system.html#tools-for-picking-colors).

## Defining a Theme

```scss
@use '@angular/material' as mat;

$my-primary: mat.m2-define-palette(mat.$m2-indigo-palette, 500);
$my-accent:  mat.m2-define-palette(mat.$m2-pink-palette, A200, A100, A400);
$my-warn:    mat.m2-define-palette(mat.$m2-red-palette);  // optional, defaults to red

$my-theme: mat.m2-define-light-theme((
  color: (
    primary: $my-primary,
    accent:  $my-accent,
    warn:    $my-warn,
  ),
  typography: mat.m2-define-typography-config(),
  density: 0,
));
```

Use `m2-define-dark-theme` for a dark background/foreground.

## Applying the Theme

```scss
@include mat.core-theme($my-theme);        // must be included once
@include mat.button-theme($my-theme);
// ... other component theme mixins
```

Or apply all at once (generates more CSS):

```scss
@include mat.all-component-themes($my-theme);
```

Add the theme file to `angular.json` `styles` array.

## Theming Dimensions

Each component has dimension-specific mixins:

| Mixin | Purpose |
|---|---|
| `component-base($theme)` | Structural styles (border-radius, border-width) — include once |
| `component-color($theme)` | Color styles |
| `component-typography($theme)` | Font styles |
| `component-density($theme)` | Spacing/size styles |
| `component-theme($theme)` | All four combined |

## Prebuilt M2 Themes

| Theme | Mode | Palettes |
|---|---|---|
| `deeppurple-amber.css` | Light | deep-purple, amber, red |
| `indigo-pink.css` | Light | indigo, pink, red |
| `pink-bluegrey.css` | Dark | pink, blue-grey, red |
| `purple-green.css` | Dark | purple, green, red |

## Multiple Themes

```scss
// Multiple themes in one file (via CSS selectors)
@include mat.all-component-themes($dark-theme);

@media (prefers-color-scheme: light) {
  @include mat.core-color($light-theme);
  @include mat.button-color($light-theme);
}
```

## Density

```scss
$my-theme: mat.m2-define-dark-theme((density: -2, ...));

// Or per-component:
.dense-zone {
  @include mat.button-density(-1);
}
```

## Reading Theme Values

```scss
// Colors
$color: mat.get-theme-color($theme, primary, default);
$color: mat.get-theme-color($theme, foreground, text);
$type:  mat.get-theme-type($theme);  // 'light' or 'dark'

// Typography
body {
  font: mat.get-theme-typography($theme, body-1);
  letter-spacing: mat.get-theme-typography($theme, body-1, letter-spacing);
}

// Density
$scale: mat.get-theme-density($theme);  // 0, -1, -2, -3, -4, -5

// Check configured dimensions
$has-color: mat.theme-has($theme, color);
```

### M2 Typography Levels

| Name | Description |
|---|---|
| `headline-1` – `headline-4` | Large one-off headers |
| `headline-5` | `<h1>` |
| `headline-6` | `<h2>` |
| `subtitle-1` | `<h3>` |
| `subtitle-2` | `<h4>` |
| `body-1` | Base body text |
| `body-2` | Secondary body text |
| `caption` | Small / hint text |
| `button` | Buttons and anchors |

Define custom typography:

```scss
$my-typography: mat.m2-define-typography-config(
  $headline-1: mat.m2-define-typography-level(112px, 112px, 300, $letter-spacing: -0.05em),
  $font-family: 'Roboto, sans-serif',
);
```

### Typography CSS Classes (from `typography-hierarchy`)

| CSS Class | Level |
|---|---|
| `.mat-headline-1` – `.mat-headline-4` | headline-1 – headline-4 |
| `.mat-h1` / `.mat-headline-5` | headline-5 / `<h1>` |
| `.mat-h2` / `.mat-headline-6` | headline-6 / `<h2>` |
| `.mat-h3` / `.mat-subtitle-1` | subtitle-1 / `<h3>` |
| `.mat-h4` / `.mat-body-1` | body-1 / `<h4>` |
| `.mat-body` / `.mat-body-2` | body-2 / body text |
| `.mat-body-strong` / `.mat-subtitle-2` | subtitle-2 |
| `.mat-small` / `.mat-caption` | caption |

## Strong Focus Indicators

```scss
@include mat.strong-focus-indicators();
@include mat.all-component-themes($my-theme);
@include mat.strong-focus-indicators-theme($my-theme);
```

## Migrating M2 → M3

No automated migration exists. General steps:

1. **Support both versions** by checking theme version in your mixins:

```scss
@mixin my-comp-theme($theme) {
  @if (mat.get-theme-version($theme) == 1) {
    // M3 styles
  } @else {
    // M2 styles
  }
}
```

2. **Replace theme definition** — use `mat.theme()` mixin (see [theming.md](./theming.md))

3. **Wrap root `@include` in a selector** — M3 requires all theme includes inside a selector:
   ```scss
   html { @include mat.all-component-themes($theme); }
   ```

4. **Enable backwards-compat for color variants** if needed:
   ```scss
   @include mat.color-variants-backwards-compatibility($theme);
   ```

5. **Enable backwards-compat for typography hierarchy** if needed:
   ```scss
   @include mat.typography-hierarchy($theme, $back-compat: true);
   ```
