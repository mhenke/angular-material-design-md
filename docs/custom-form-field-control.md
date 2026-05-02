# Creating a Custom Form Field Control

> Source: https://material.angular.dev/guide/creating-a-custom-form-field-control — https://github.com/angular/components/blob/main/guides/creating-a-custom-form-field-control.md

Lets you create a component that integrates with `<mat-form-field>` (floating label, hints,
errors, prefix/suffix).

## Step 1: Provide as `MatFormFieldControl`

```ts
@Component({
  providers: [{provide: MatFormFieldControl, useExisting: MyTelInput}],
})
export class MyTelInput implements MatFormFieldControl<MyTel> { ... }
```

## Step 2: Implement Required Interface Members

### `value`
The data value the control holds. Set/get with whatever type matches the generic parameter.

### `stateChanges` (Subject)
Emit whenever state changes so the form field runs change detection:

```ts
stateChanges = new Subject<void>();

set value(tel: MyTel | null) {
  // update internal state...
  this.stateChanges.next();
}

ngOnDestroy() { this.stateChanges.complete(); }
```

### `id`
Unique ID for the host element (used by `for`/`aria-labelledby`):

```ts
static nextId = 0;
@HostBinding() id = `my-tel-input-${MyTelInput.nextId++}`;
```

### `placeholder`
```ts
@Input()
get placeholder() { return this._placeholder; }
set placeholder(plh) {
  this._placeholder = plh;
  this.stateChanges.next();
}
```

### `ngControl`
The Angular Forms control bound to this component. Set via `@Self()` injection:

```ts
constructor(@Optional() @Self() public ngControl: NgControl) {
  if (this.ngControl != null) {
    this.ngControl.valueAccessor = this;  // avoids cyclic dependency
  }
}
```

### `focused`
```ts
focused = false;
onFocusIn(event: FocusEvent) { ... this.stateChanges.next(); }
onFocusOut(event: FocusEvent) { ... this.stateChanges.next(); }
```

### `empty`
```ts
get empty() { return !this.parts.value.area && ...; }
```

### `shouldLabelFloat`
```ts
@HostBinding('class.floating')
get shouldLabelFloat() { return this.focused || !this.empty; }
```

### `required`
```ts
@Input()
get required() { return this._required; }
set required(req: BooleanInput) {
  this._required = coerceBooleanProperty(req);
  this.stateChanges.next();
}
```

### `disabled`
```ts
@Input()
get disabled(): boolean { return this._disabled; }
set disabled(value: BooleanInput) {
  this._disabled = coerceBooleanProperty(value);
  this._disabled ? this.parts.disable() : this.parts.enable();
  this.stateChanges.next();
}
```

### `errorState`
Simple approach (misses parent form submissions):

```ts
get errorState(): boolean { return this.parts.invalid && this.touched; }
```

Robust approach with `ngDoCheck`:

```ts
errorState = false;

constructor(
  @Optional() private _parentForm: NgForm,
  @Optional() private _parentFormGroup: FormGroupDirective
) {}

ngDoCheck() {
  if (this.ngControl) { this.updateErrorState(); }
}

private updateErrorState() {
  const parentSubmitted = this._parentFormGroup?.submitted || this._parentForm?.submitted;
  const newState = (this.ngControl?.invalid || this.parts.invalid) && (this.touched || parentSubmitted);
  if (this.errorState !== newState) {
    this.errorState = newState;
    this.stateChanges.next();
  }
}
```

### `controlType`
A unique string that becomes a CSS class on the form field:

```ts
controlType = 'my-tel-input';
// → .mat-form-field-type-my-tel-input
```

### `setDescribedByIds(ids: string[])`
Called by form field when hints/errors appear/disappear (for `aria-describedby`):

```ts
@Input('aria-describedby') userAriaDescribedBy: string;

setDescribedByIds(ids: string[]) {
  const el = this._elementRef.nativeElement.querySelector('.my-input-container')!;
  el.setAttribute('aria-describedby', ids.join(' '));
}
```

### `onContainerClick(event: MouseEvent)`
Called when the form field wrapper is clicked:

```ts
onContainerClick(event: MouseEvent) {
  if ((event.target as Element).tagName.toLowerCase() !== 'input') {
    this._elementRef.nativeElement.querySelector('input').focus();
  }
}
```

## Accessibility

Group related inputs with `role="group"` and link to the form field label:

```ts
constructor(@Optional() public parentFormField: MatFormField) {}
```

```html
<div role="group" [formGroup]="parts"
     [attr.aria-labelledby]="parentFormField?.getLabelId()">
```

## Usage

```html
<mat-form-field>
  <my-tel-input placeholder="Phone" required></my-tel-input>
  <mat-icon matPrefix>phone</mat-icon>
  <mat-hint>Include area code</mat-hint>
</mat-form-field>
```
