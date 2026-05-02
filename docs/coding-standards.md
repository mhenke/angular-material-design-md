# Angular Material Coding Standards

> Source: https://github.com/angular/components/blob/main/CODING_STANDARDS.md

Base style: [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)

## General

- **100 column limit** for all files (TS, SCSS, HTML, bash, markdown)
- Prefer focused, granular components over complex, configurable ones
- Prefer small, focused modules (200–300 lines; consider refactoring at ~400)
- **Less is more** — avoid features that don't offer high value; prefer a single API per capability

## Comments

- Explain **why**, not what
- TypeScript: JsDoc (`/** */`) for public API, `//` for everything else
- SCSS: always `//`
- HTML: `<!-- -->` (stripped at build time)

## API Design

- Avoid boolean arguments that mean "do something extra" — split into separate functions
- Prefer exact, descriptive names over short abbreviations (`labelPosition` over `align`)
- Use `is`/`has` prefixes for boolean properties/methods (except `@Input` properties)
- Don't suffix observables with `$`

## TypeScript

### Typing
- Avoid `any` — prefer generics
- All public API members must have explicit types (docs tooling requirement)

### Access Modifiers
- Omit `public` (it's the default)
- `private` + underscore prefix for private members
- `protected` with no prefix
- Internal (public for Angular but not user-facing): underscore prefix without `private`, or use `@docs-private` JsDoc annotation

### Getters/Setters
- Only for `@Input` properties or API compatibility
- Keep logic short (≤3 lines); extract longer logic into methods
- Getter immediately precedes its setter
- `@Input` decorator on the getter, not setter
- Prefer `readonly` property over a getter-only accessor

### JsDoc
```ts
/** The label position relative to the checkbox. Defaults to 'after' */
@Input() labelPosition: 'before' | 'after' = 'after';

/**
 * Opens a modal dialog.
 * @param component Type of the component to load.
 * @param config Dialog configuration options.
 * @returns Reference to the newly-opened dialog.
 */
open<T>(component: ComponentType<T>, config?: MatDialogConfig): MatDialogRef<T> { ... }

/** Whether the button is disabled. */  // use "Whether..." not "True if..."
disabled = false;
```

### Coercion (Boolean/Number Inputs)
```ts
import {Input, booleanAttribute} from '@angular/core';

@Input({transform: booleanAttribute}) disabled: boolean = false;
```

### Class Naming
- Name captures what it *does*, not how it is used
- `Mat` prefix for directives with `mat-` selector; `Cdk` prefix for CDK directives
- Avoid "Service" suffix

### Inheritance
Avoid inheritance for reusable behaviors — use TypeScript mixins instead.

## Angular

### Host Bindings
Prefer `host` object in `@Directive`/`@Component` config over `@HostBinding`/`@HostListener`
(prevents type-preservation issues in SSR for native `Event` types).

### Expose Native Inputs
Use `ng-content` to expose native inputs instead of wrapping them:

```html
<!-- Do: -->
<ng-content></ng-content>

<!-- Don't: -->
<input>
```

## CSS / SCSS

### Specificity
- Always prioritize **lowest specificity**
- Avoid SCSS nesting for organization — flat selectors override more easily
- Use flat class names (e.g., `.mat-calendar-month`) not nested (`.mat-calendar .mat-month`)

### Component Styles
- Never set `margin` on a host element
- Prefer styling the host element over internal elements (easier to override)
- Never override component internal CSS classes outside the theming API

### Flexbox
- Component outermost elements are never `display: flex`
- Don't use `flex` on elements containing projected content (baseline calculation issues)

### Windows High Contrast
Support high-contrast mode:
```scss
@include cdk-high-contrast(active, off) {
  .my-component { border: 1px solid #fff !important; }
}
```

### Class vs Tag/Attribute Selectors
Prefer CSS classes to tag names and attributes:
```scss
.mat-mdc-slider { ... }     /* Do */
mdc-slider { ... }           /* Don't */
.mat-mdc-slider-input { ... } /* Do */
input[type="button"] { ... }  /* Don't */
```

### CSS Comments
Explain what a class represents when not obvious:
```scss
// Floating pane containing the calendar below the input.
.mat-datepicker-calendar-pane { ... }
```
