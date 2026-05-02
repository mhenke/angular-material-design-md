# Getting Started with Angular Material

> Source: https://material.angular.dev/guides — https://github.com/angular/components/blob/main/guides/getting-started.md

## Install

```bash
ng add @angular/material
```

The `ng add` command installs Angular Material, CDK, and prompts for:

1. **Prebuilt theme** — choose a prebuilt theme or "custom" for Sass theming
2. **Typography styles** — apply global typography to the application

### What `ng add` does automatically

- Adds `@angular/material` and `@angular/cdk` to `package.json`
- Adds Roboto font to `index.html`
- Adds Material Design icon font to `index.html`
- Adds global CSS: removes `body` margins, sets `height: 100%` on `html`/`body`, sets Roboto as default font

## Use a Component

Import the component module, then use it in the template:

```ts
import {MatSlideToggle} from '@angular/material/slide-toggle';

@Component({
  imports: [MatSlideToggle],
})
class AppComponent {}
```

```html
<mat-slide-toggle>Toggle me!</mat-slide-toggle>
```

```bash
ng serve
```

Visit `http://localhost:4200` to verify.

## Next Steps

- [Theming](./theming.md) — customize colors, typography, density
- [Schematics](./schematics.md) — generate pre-built component scaffolds
