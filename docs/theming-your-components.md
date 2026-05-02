# Theming Your Own Components (M3)

> Source: https://material.angular.dev/guide/theming-your-components — https://github.com/angular/components/blob/main/guides/theming-your-components.md

Two approaches to apply theme styles to custom components:

1. **CSS variables** (`--mat-sys-*`) — use in component stylesheets
2. **Utility classes** (`mat-bg-*`, `mat-text-*`, etc.) — use directly in templates

Both automatically support light/dark mode via `color-scheme`.

Requires `mat.theme()` and optionally `mat.system-classes()` in your theme file.

---

## Color System Tokens

All tokens follow the `--mat-sys-` prefix.

### Primary
```css
--mat-sys-primary              --mat-sys-on-primary
--mat-sys-primary-container    --mat-sys-on-primary-container
--mat-sys-primary-fixed        --mat-sys-primary-fixed-dim
--mat-sys-on-primary-fixed     --mat-sys-on-primary-fixed-variant
--mat-sys-inverse-primary
```

### Secondary
```css
--mat-sys-secondary              --mat-sys-on-secondary
--mat-sys-secondary-container    --mat-sys-on-secondary-container
--mat-sys-secondary-fixed        --mat-sys-secondary-fixed-dim
--mat-sys-on-secondary-fixed     --mat-sys-on-secondary-fixed-variant
```

### Tertiary
```css
--mat-sys-tertiary              --mat-sys-on-tertiary
--mat-sys-tertiary-container    --mat-sys-on-tertiary-container
--mat-sys-tertiary-fixed        --mat-sys-tertiary-fixed-dim
--mat-sys-on-tertiary-fixed     --mat-sys-on-tertiary-fixed-variant
```

### Error
```css
--mat-sys-error              --mat-sys-on-error
--mat-sys-error-container    --mat-sys-on-error-container
```

### Surface
```css
--mat-sys-surface                        --mat-sys-on-surface
--mat-sys-on-surface-variant             --mat-sys-surface-variant
--mat-sys-surface-bright                 --mat-sys-surface-dim
--mat-sys-surface-container              --mat-sys-surface-container-low
--mat-sys-surface-container-lowest      --mat-sys-surface-container-high
--mat-sys-surface-container-highest     --mat-sys-surface-tint
--mat-sys-inverse-surface               --mat-sys-inverse-on-surface
```

### Miscellaneous
```css
--mat-sys-background    --mat-sys-on-background
--mat-sys-outline       --mat-sys-outline-variant
--mat-sys-scrim         --mat-sys-shadow
--mat-sys-neutral-variant20    --mat-sys-neutral10
```

---

## Background Utility Classes

| Class | CSS Variable |
|---|---|
| `.mat-bg-primary` | `--mat-sys-primary` |
| `.mat-bg-primary-container` | `--mat-sys-primary-container` |
| `.mat-bg-secondary` | `--mat-sys-secondary` |
| `.mat-bg-secondary-container` | `--mat-sys-secondary-container` |
| `.mat-bg-error` | `--mat-sys-error` |
| `.mat-bg-error-container` | `--mat-sys-error-container` |
| `.mat-bg-surface` | `--mat-sys-surface` |
| `.mat-bg-surface-variant` | `--mat-sys-surface-variant` |
| `.mat-bg-surface-container` | `--mat-sys-surface-container` |
| `.mat-bg-surface-container-low` | `--mat-sys-surface-container-low` |
| `.mat-bg-surface-container-lowest` | `--mat-sys-surface-container-lowest` |
| `.mat-bg-surface-container-high` | `--mat-sys-surface-container-high` |
| `.mat-bg-surface-container-highest` | `--mat-sys-surface-container-highest` |
| `.mat-bg-inverse-surface` | `--mat-sys-inverse-surface` |
| `.mat-bg-disabled` | `color-mix(in srgb, --mat-sys-on-surface 12%, transparent)` |

---

## Text Utility Classes

| Class | Token |
|---|---|
| `.mat-text-primary` | `--mat-sys-primary` |
| `.mat-text-secondary` | `--mat-sys-secondary` |
| `.mat-text-error` | `--mat-sys-error` |
| `.mat-text-disabled` | `color-mix(in srgb, --mat-sys-on-surface 38%, transparent)` |
| `.mat-text-on-surface-variant` | `--mat-sys-on-surface-variant` |
| `.mat-text-on-primary` | `--mat-sys-on-primary` |
| `.mat-text-on-primary-container` | `--mat-sys-on-primary-container` |
| `.mat-text-on-secondary` | `--mat-sys-on-secondary` |
| `.mat-text-on-secondary-container` | `--mat-sys-on-secondary-container` |
| `.mat-text-on-error` | `--mat-sys-on-error` |
| `.mat-text-on-error-container` | `--mat-sys-on-error-container` |
| `.mat-text-on-surface` | `--mat-sys-on-surface` |
| `.mat-text-inverse-on-surface` | `--mat-sys-inverse-on-surface` |

---

## Typography System Tokens

Five categories × three sizes (sm/md/lg):

| Category | Sizes |
|---|---|
| Body | `--mat-sys-body-small/medium/large` |
| Display | `--mat-sys-display-small/medium/large` |
| Headline | `--mat-sys-headline-small/medium/large` |
| Label | `--mat-sys-label-small/medium/large` |
| Title | `--mat-sys-title-small/medium/large` |

Each has sub-tokens: `-font`, `-line-height`, `-size`, `-tracking`, `-weight`.

### Typography Utility Classes

| Class | Token |
|---|---|
| `.mat-font-body-sm` | `--mat-sys-body-small` |
| `.mat-font-body-md` | `--mat-sys-body-medium` |
| `.mat-font-body-lg` | `--mat-sys-body-large` |
| `.mat-font-display-sm/md/lg` | display small/medium/large |
| `.mat-font-headline-sm/md/lg` | headline small/medium/large |
| `.mat-font-label-sm/md/lg` | label small/medium/large |
| `.mat-font-title-sm/md/lg` | title small/medium/large |

---

## Shape (Corner Radius) System Tokens

```css
--mat-sys-corner-none: 0
--mat-sys-corner-extra-small: 4px
--mat-sys-corner-extra-small-top: 4px 4px 0 0
--mat-sys-corner-small: 8px
--mat-sys-corner-medium: 12px
--mat-sys-corner-large: 16px
--mat-sys-corner-large-top: 16px 16px 0 0
--mat-sys-corner-large-start: 16px 0 0 16px
--mat-sys-corner-large-end: 0 16px 16px 0
--mat-sys-corner-extra-large: 28px
--mat-sys-corner-extra-large-top: 28px 28px 0 0
--mat-sys-corner-full: 9999px
```

### Corner Utility Classes

| Class | Radius |
|---|---|
| `.mat-corner-xs` | `--mat-sys-corner-extra-small` (4px) |
| `.mat-corner-sm` | `--mat-sys-corner-small` (8px) |
| `.mat-corner-md` | `--mat-sys-corner-medium` (12px) |
| `.mat-corner-lg` | `--mat-sys-corner-large` (16px) |
| `.mat-corner-xl` | `--mat-sys-corner-extra-large` (28px) |
| `.mat-corner-full` | `--mat-sys-corner-full` (9999px) |

---

## Elevation

### Outline Tokens
```css
--mat-sys-outline          /* standard border */
--mat-sys-outline-variant  /* subtle border */
```

### Border Utility Classes
| Class | Effect |
|---|---|
| `.mat-border` | `1px solid --mat-sys-outline` |
| `.mat-border-subtle` | `1px solid --mat-sys-outline-variant` |

### Shadow (Box-Shadow) Tokens
```css
--mat-sys-level0  /* no shadow */
--mat-sys-level1  /* slight elevation — elevated card, slider handle */
--mat-sys-level2  /* raised — menu, select panel */
--mat-sys-level3  /* floating — FAB */
--mat-sys-level4  /* hover/focus interaction */
--mat-sys-level5  /* max elevation */
```

### Shadow Utility Classes
| Class | Token |
|---|---|
| `.mat-shadow-1` | `--mat-sys-level1` |
| `.mat-shadow-2` | `--mat-sys-level2` |
| `.mat-shadow-3` | `--mat-sys-level3` |
| `.mat-shadow-4` | `--mat-sys-level4` |
| `.mat-shadow-5` | `--mat-sys-level5` |

---

## M2 Compatibility

If your theme uses the legacy M2 `theme-config` approach:

```scss
html {
  @include mat.core-theme($theme);
  @include mat.button-theme($theme);
  @include mat.m2-theme($theme);      // generates --mat-sys-* from M2 theme
  @include mat.system-classes();       // enables utility classes
}
```

This lets you use CSS variables and utility classes without migrating to `mat.theme()` yet.
