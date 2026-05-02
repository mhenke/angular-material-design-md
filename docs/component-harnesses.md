# Using Angular Material Component Test Harnesses

> Source: https://material.angular.dev/guide/using-component-harnesses — https://github.com/angular/components/blob/main/guides/using-component-harnesses.md

Component harnesses are test classes that interact with Material components the way a user would.
They insulate tests from internal DOM structure changes.

## Why Use Harnesses

1. **Readable** — `await select.open()` vs `trigger.triggerEventHandler('click', {})`
2. **Robust** — no CSS class selectors into private DOM; no manual `detectChanges()`/`whenStable()`
3. **Async-normalized** — all harness APIs are async, regardless of underlying implementation

## Setup

```ts
import {HarnessLoader} from '@angular/cdk/testing';
import {TestbedHarnessEnvironment} from '@angular/cdk/testing/testbed';

let loader: HarnessLoader;

beforeEach(async () => {
  TestBed.configureTestingModule({imports: [MyModule]});
  fixture = TestBed.createComponent(UserProfile);
  loader = TestbedHarnessEnvironment.loader(fixture);
});
```

Package split:
- `@angular/cdk/testing` — shared, environment-agnostic
- `@angular/cdk/testing/testbed` — Karma/TestBed unit tests
- `@angular/cdk/testing/selenium-webdriver` — Selenium e2e tests

## Loading Harnesses

```ts
import {MatButtonHarness} from '@angular/material/button/testing';

const buttons = await loader.getAllHarnesses(MatButtonHarness);  // all instances
const first   = await loader.getHarness(MatButtonHarness);       // first instance
```

### Child Loaders (scope to a DOM subtree)

```ts
const footerLoader = await loader.getChildLoader('.footer');
const footerButton = await footerLoader.getHarness(MatButtonHarness);
```

### Filtering with `with()`

All harnesses support at minimum:
- `selector` — must match this CSS selector (in addition to host selector)
- `ancestor` — must have this ancestor

```ts
const info = await loader.getHarness(MatButtonHarness.with({selector: '#more-info'}));
const cancel = await loader.getHarness(MatButtonHarness.with({text: 'Cancel'}));
const ok = await loader.getHarness(
  MatButtonHarness.with({selector: '.confirm', text: /^(Ok|Okay)$/})
);
```

## Interacting with Components

```ts
it('should confirm when ok clicked', async () => {
  const okButton = await loader.getHarness(MatButtonHarness.with({selector: '.confirm'}));
  expect(fixture.componentInstance.confirmed).toBe(false);
  expect(await okButton.isDisabled()).toBe(false);
  await okButton.click();
  expect(fixture.componentInstance.confirmed).toBe(true);
});
```

No `fixture.detectChanges()` needed — harnesses handle change detection automatically.

## Comparison: Without vs With Harnesses

**Without harnesses:**
```ts
const selectTrigger = fixture.debugElement.query(By.css('.mat-select-trigger'));
selectTrigger.triggerEventHandler('click', {});
fixture.detectChanges();
await fixture.whenStable();
const options = document.querySelectorAll('.mat-select-panel mat-option');
options[1].click();
fixture.detectChanges();
await fixture.whenStable();
```

**With harnesses:**
```ts
const select = await loader.getHarness(MatSelectHarness);
await select.open();
const bugOption = await select.getOption({text: 'Bug'});
await bugOption.click();
```

## Supported Environments

- TestBed (Karma unit tests)
- Selenium WebDriver (e2e tests)
- Custom environments via `HarnessEnvironment` + `TestElement`
