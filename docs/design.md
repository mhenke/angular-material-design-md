# Angular Material Design System (M3)

> This document establishes design constraints and patterns for AI code generation in Angular Material projects. It references [Material Design 3](https://m3.material.io/) and [Angular Material v19+](https://material.angular.dev/).

## Design Tokens

### Color System

Material Design 3 uses a **semantic color system** with dynamic color generation. All colors are defined via CSS variables in the `--mat-sys-*` namespace.

**Primary Roles:**
- `--mat-sys-primary` — primary actions, accent elements
- `--mat-sys-secondary` — secondary accents, filters
- `--mat-sys-tertiary` — tertiary accents, alternative emphasis
- `--mat-sys-error` — destructive actions, errors

**Neutral Roles:**
- `--mat-sys-surface` — backgrounds (main app background)
- `--mat-sys-surface-dim` — slightly darker surface
- `--mat-sys-surface-bright` — slightly lighter surface
- `--mat-sys-on-surface` — text on surface
- `--mat-sys-outline` — dividers, borders, unfocused states
- `--mat-sys-outline-variant` — subtle dividers

**Tonal Variants:**
- `--mat-sys-*-container` — tonal background for actions/chips
- `--mat-sys-on-*-container` — text on tonal backgrounds

**Usage Rule for AI:**
- Always use `--mat-sys-*` variables for colors, never hardcoded hex/rgb
- Never override `--mat-sys-*` variables outside the `mat.theme()` mixin
- For custom components, use semantic roles (primary, secondary, surface) not palette names

### Typography Scale

Material Design 3 defines a **typographic system** with named styles. Angular Material provides these via CSS variables and typography mixins.

**Scale Levels (M3 standard):**
- `display-large`, `display-medium`, `display-small` — large headings (32–28px, 500 weight)
- `headline-large`, `headline-medium`, `headline-small` — page/section headings (32–24px)
- `title-large`, `title-medium`, `title-small` — component titles (22–16px, 500 weight)
- `body-large`, `body-medium`, `body-small` — body text (16–12px)
- `label-large`, `label-medium`, `label-small` — labels, buttons (14–11px, 500 weight)

**Usage Rule for AI:**
- Use typography scale names (e.g., `--mat-sys-title-large`) not arbitrary font sizes
- Never set font-size/weight/line-height directly; use `mat.typography-level()` or CSS variables
- Button/label text should use `label-*` scale
- Component titles should use `title-*` scale
- Body text should use `body-*` scale

### Spacing & Density

**Spacing Unit:** 4px (base) — all spacing is a multiple of 4px
- Common: 4px, 8px, 12px, 16px, 24px, 32px, 48px

**Density:** Adjustable via `density` parameter in `mat.theme()`
- `0` (default) — standard spacing
- `-1`, `-2`, `-3` — increasingly compact (reduces padding/gaps)
- `1`, `2`, `3` — increasingly spacious (increases padding/gaps)

**Usage Rule for AI:**
- All padding/margin/gaps are multiples of 4px
- Use `--mat-spacing-*` CSS variables if available, or compute as `4px * N`
- Never set margins on host elements (styling host is done by parent container)
- Components should respect density adjustments—use `mat-density` mixin for custom components

### Elevation & Shadows

Material Design 3 defines **elevation levels** (0–5) with corresponding shadows. These map to `--mat-sys-shadow-*` CSS variables or shadow mixins.

**Usage Rule for AI:**
- Use Material Design 3 elevation levels, not custom shadows
- Apply shadows via `--mat-sys-shadow-*` variables or `mat.elevation()` mixin
- Don't hardcode box-shadow values

## Component Architecture

### Theming API (Sass)

All components use the **M3 theming system** via `mat.theme()` mixin:

```scss
@use '@angular/material' as mat;

html {
  color-scheme: light dark;
  @include mat.theme((
    color: mat.$violet-palette,
    typography: Roboto,
    density: 0,
  ));
}
```

**Outputs:** CSS variables `--mat-sys-*` at `:root` level (or custom selector).

**Theme-Type Options:**
- `'color-scheme'` (default) — uses `light-dark()` function for automatic light/dark switching
- `'light'` or `'dark'` — locks to single mode (for older browsers)

**Custom Palettes:**
Generate with: `ng generate @angular/material:theme-color`

**Usage Rule for AI:**
- Never hardcode theme variables; assume `mat.theme()` is applied once in `html` or `body`
- All component styles should reference `--mat-sys-*` variables
- Custom components must use `@forward '@angular/material' as mat;` to access theming functions

### Component Patterns

#### Structure
- **Host element:** Semantic tag (button, div, nav) with class `.mat-mdc-*`
- **Host bindings:** Minimal; only for disabled/aria states
- **Content projection:** Use `<ng-content>` to avoid redundant input elements
- **Sub-elements:** BEM-style flat class names (`.mat-mdc-button__icon`, not `.mat-mdc-button .mat-icon`)

#### Styling Host Elements
**Rule:** Never set margin on host. Host element styles are only padding/sizing/borders.
- Parent container controls positioning and spacing (via flexbox gap, margins on parent)
- This allows flexible reuse and avoids fighting specificity

#### State Handling
- **Disabled:** `[disabled]` attribute on host + `aria-disabled` for custom components
- **Focus:** Use `focus-visible` pseudo-class, never remove outline
- **Hover:** Only on interactive elements (buttons, links)
- **Active:** Use `:active` or `mat-ripple` for feedback

#### CSS Specificity
**Rule:** Lowest specificity wins. Flat selectors override more easily.
- Never nest SCSS selectors for organization
- Use single-class selectors (`.mat-mdc-button`, not `.mat-mdc > .button`)
- Avoid attribute selectors when class selectors work
- Override component styles only via theming variables, never via internal CSS classes

### Common Component Types

#### Buttons
- Use `<button mat-button>`, `<button mat-raised-button>`, `<button mat-stroked-button>`, `<button mat-flat-button>`
- Icon buttons: `<button mat-icon-button>`
- Always has `type="button"` unless form submission intended
- Avoid margin on host; use flex gap or margin on parent

#### Form Controls
- Wrap native inputs with `<mat-form-field>` for consistent styling
- Use `matInput`, `matSelect`, `matDatepicker` directives
- Labels must be associated via `matLabel`
- Errors/hints displayed via `matError`, `matHint`

#### Cards & Containers
- Use `<mat-card>` for grouped content
- Don't set margins on host; use gap on parent or margin on siblings
- Padding inside card is controlled by density and theme

#### Lists
- Use `<mat-list>` with `<mat-list-item>`
- Items have consistent height; don't override with custom styles
- Use `matListItemTitle`, `matListItemLine` for content structure

## Accessibility Requirements

### Color Contrast
- **WCAG AA:** 4.5:1 for text on backgrounds, 3:1 for large text
- **WCAG AAA:** 7:1 and 4.5:1
- Material Design 3 colors are WCAG AA compliant by default
- **Rule for AI:** Never change color contrast via custom theming; use M3 palettes directly

### Focus Management
- All interactive elements must have visible focus indicator
- Focus order should match visual/logical flow (use `tabindex` sparingly)
- Custom components: implement `FocusableOption` interface (CDK) if needed

### ARIA Patterns
- Buttons: `role="button"` (implicit on `<button>`)
- Links: `role="link"` (implicit on `<a>`)
- Form labels: `<label for="...">` or `matLabel`
- Icons as labels: use `aria-label` on icon element
- Disabled elements: `aria-disabled="true"` (in addition to `disabled` attribute)
- Modal dialogs: `role="dialog"`, `aria-modal="true"`, focus trap

**Rule for AI:** If using a component from Material, ARIA is already handled. Only add ARIA for custom interactive elements.

### High Contrast Mode
Support Windows High Contrast mode:
```scss
@include cdk-high-contrast(active, off) {
  .my-component {
    border: 1px solid #fff !important;
  }
}
```

## Code Conventions (from Angular Material Standards)

### TypeScript
- **Typing:** No `any`; use generics
- **Boolean inputs:** Use `@Input({transform: booleanAttribute})`
- **Access modifiers:** Omit `public`, use `private` with underscore, use `protected` with no prefix
- **Naming:** Descriptive names over abbreviations (e.g., `labelPosition` not `align`)
- **JsDoc:** Document public API with `/** */`, use `// ` for inline comments

### Sass / CSS
- **Specificity:** Always use lowest specificity; flat selectors
- **Class selectors:** Prefer over tag/attribute selectors
- **Nesting:** Don't nest for organization (breaks override ability)
- **Component margins:** Never set margin on host element
- **Flexbox:** Never `display: flex` on component host; never `flex` on elements with projected content
- **Comments:** Explain *what* the class represents (e.g., "Floating pane containing calendar")

### HTML
- **Semantic tags:** Use `<button>`, `<nav>`, `<article>` appropriately
- **Attributes:** `[attr.aria-label]`, `[attr.data-*]` for dynamic values
- **Content projection:** Use `<ng-content>` for flexibility
- **Class names:** kebab-case (`.mat-mdc-button`)

### Angular
- **Components:** Standalone preferred (Angular v14+); import only what's needed
- **Directives:** Use `host` config object over `@HostBinding` / `@HostListener`
- **Change detection:** Default `ChangeDetectionStrategy.Default` unless performance critical
- **RxJS:** Use observables for async data, avoid nested subscriptions

## Theming Custom Components

### Pattern
```scss
// Import Material theming
@use '@angular/material' as mat;
@use 'sass:map';

// Define component styles with theme reference
@mixin my-component-theme($theme) {
  $color-config: map.get($theme, color);
  $primary: map.get($color-config, primary);
  
  .my-component {
    background: var(--mat-sys-surface);
    color: var(--mat-sys-on-surface);
    border-color: var(--mat-sys-outline);
  }
}

// Include in app-level stylesheet
@include my-component-theme(mat.$theme);
```

**Rules:**
- Always reference `--mat-sys-*` CSS variables, never `$primary` map directly
- Never hardcode hex/rgb colors
- Use `mat.$theme` variable passed from `mat.theme()` output
- Expose mixin for custom theme overrides

## Design Patterns for AI

### When to Create Custom Components
- **Do:** If functionality is unique to your app and Material doesn't provide it
- **Don't:** If a Material component exists that covers the use case (customize via theming instead)

### Composition Over Customization
- Prefer wrapping/composing Material components over overriding their styles
- Custom container components should use `<ng-content>` to wrap Material components

### Avoiding Breaking Changes
- Don't override Material component internal CSS classes (use theming API)
- Don't change semantic HTML structure (Material relies on it)
- Don't set arbitrary z-index values (respect Material's z-index ladder)

### Common Mistakes to Avoid
- ❌ Setting margins on custom component host element
- ❌ Using hardcoded colors instead of `--mat-sys-*` variables
- ❌ Setting `display: flex` on component host (parent responsibility)
- ❌ Nesting SCSS selectors for organization (breaks override ability)
- ❌ Removing focus outlines for "design" reasons (accessibility issue)
- ❌ Using `any` in TypeScript (use generics)
- ❌ Overriding Material component internals via CSS (use theming API)
- ❌ Setting font-size directly (use typography scale variables)

## References

- **Material Design 3:** https://m3.material.io/
- **Angular Material Theming:** https://material.angular.dev/guide/theming
- **Angular Material Components:** https://material.angular.dev/components/categories
- **Angular Coding Standards:** https://github.com/angular/components/blob/main/CODING_STANDARDS.md
- **WCAG 2.1:** https://www.w3.org/WAI/WCAG21/quickref/
