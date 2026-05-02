# Creating a Custom Stepper with CDK Stepper

> Source: https://material.angular.dev/guide/creating-a-custom-stepper-using-the-cdk-stepper — https://github.com/angular/components/blob/main/guides/creating-a-custom-stepper-using-the-cdk-stepper.md

The CDK stepper lets you build a fully custom stepper with no Material Design styling imposed.

## Create the Component

Extend `CdkStepper` and provide it as itself so other components can recognize it:

```ts
import {CdkStepper} from '@angular/cdk/stepper';

@Component({
  selector: 'app-custom-stepper',
  templateUrl: './custom-stepper.component.html',
  providers: [{provide: CdkStepper, useExisting: CustomStepperComponent}]
})
export class CustomStepperComponent extends CdkStepper {
  onClick(index: number): void {
    this.selectedIndex = index;
  }
}
```

## Template

Key `CdkStepper` properties available in the template:

| Property | Description |
|---|---|
| `selectedIndex` | Index of the active step |
| `steps` | QueryList of all `CdkStep` instances |
| `selected` | The currently active `CdkStep` |
| `linear` | Whether steps must be completed in order |

```html
<section class="container">
  <header><h2>Step {{selectedIndex + 1}}/{{steps.length}}</h2></header>

  <div [style.display]="selected ? 'block' : 'none'">
    <ng-container [ngTemplateOutlet]="selected.content"></ng-container>
  </div>

  <footer class="step-navigation-bar">
    <button cdkStepperPrevious>&larr;</button>
    @for (step of steps; track step; let i = $index) {
      <button [class.active]="selectedIndex === i" (click)="onClick(i)">
        Step {{i + 1}}
      </button>
    }
    <button cdkStepperNext>&rarr;</button>
  </footer>
</section>
```

## Usage

Wrap each step in `<cdk-step>`:

```html
<app-custom-stepper>
  <cdk-step><p>Step 1 content</p></cdk-step>
  <cdk-step><p>Step 2 content</p></cdk-step>
</app-custom-stepper>
```

Dynamic steps:

```html
<app-custom-stepper>
  @for (step of mySteps; track step) {
    <cdk-step>
      <my-step-component [step]="$index"></my-step-component>
    </cdk-step>
  }
</app-custom-stepper>
```

## Linear Mode

Prevents advancing until the current step is marked complete:

```html
<app-custom-stepper linear>
  <cdk-step editable="false" [completed]="completed">
    <input type="text" name="a" value="Must complete this step" />
    <button (click)="completeStep()">Complete step</button>
  </cdk-step>
  <cdk-step editable="false">
    <input type="text" name="b" value="Step 2" />
  </cdk-step>
</app-custom-stepper>
```

```ts
export class AppComponent {
  completed = false;
  completeStep(): void { this.completed = true; }
}
```

## CDK Stepper API Reference

Full API: https://material.angular.dev/cdk/stepper/api#CdkStepper
