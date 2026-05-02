# Bi-directionality (RTL/LTR)

> Source: https://material.angular.dev/guide/bidirectionality — https://github.com/angular/components/blob/main/guides/bidirectionality.md

## How Angular Material Handles Direction

All Angular Material components automatically reflect the LTR/RTL direction of their container.
Set the `dir` attribute on `<html>`, `<body>`, or any ancestor element to control text direction.

## Reading Direction in Your Own Components

Import `BidiModule` from `@angular/cdk/bidi`, then inject `Directionality`:

```ts
import {BidiModule, Directionality, Direction} from '@angular/cdk/bidi';

@Component({ /* ... */ })
export class MyComponent {
  private dir: Direction;

  constructor(directionality: Directionality) {
    this.dir = directionality.value;  // 'ltr' | 'rtl'

    directionality.change.subscribe(() => {
      this.dir = directionality.value;
    });
  }
}
```

### `Directionality` API

| Property | Type | Description |
|---|---|---|
| `value` | `'ltr' \| 'rtl'` | Current text direction |
| `change` | `Observable<Direction>` | Emits when direction changes via `dir` attribute inside the Angular app |

**Note:** `change` does NOT emit for `dir` attribute changes on `<html>` or `<body>` — those are
assumed static. It only captures changes from `dir` attributes inside the Angular application
context.
