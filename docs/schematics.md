# Angular Material Schematics

> Source: https://material.angular.dev/guide/schematics — https://github.com/angular/components/blob/main/guides/schematics.md

## Installation

```bash
ng add @angular/material   # installs Material + CDK, runs install schematic
ng add @angular/cdk        # CDK only
```

## Component Schematics

Generate pre-built Material Design component scaffolds:

| Schematic | Command | Description |
|---|---|---|
| Address Form | `ng generate @angular/material:address-form <name>` | Form with Material form controls for shipping address |
| Navigation | `ng generate @angular/material:navigation <name>` | Responsive sidenav + toolbar |
| Dashboard | `ng generate @angular/material:dashboard <name>` | Grid of Material cards/menus |
| Table | `ng generate @angular/material:table <name>` | Data table with sorting + pagination |
| Tree | `ng generate @angular/material:tree <name>` | Interactive nested folder structure with `<mat-tree>` |

## CDK Schematics

| Schematic | Command | Description |
|---|---|---|
| Drag & Drop | `ng generate @angular/cdk:drag-drop <name>` | Interactive to-do list with CDK drag-drop |

## Theme Color Schematic (M3)

Generates Material 3 color palettes from input colors:

```bash
ng generate @angular/material:theme-color
```

Produces a file with M3 palettes and optional high-contrast override mixins. See the
[schematic README](https://github.com/angular/components/blob/main/src/material/schematics/ng-generate/theme-color/README.md)
for options.
