# DESIGN.md Format Reference

> Source: https://github.com/google-labs-code/design.md — Google open-source format, ~8.5k ★
>
> **Purpose:** DESIGN.md is a self-contained, plain-text representation of a design system for AI
> coding agents. It gives agents like Claude Code, Cursor, and Kiro your exact design rules —
> colors, typography, components — in one Markdown file. It is the format our `DESIGN.md` must
> follow.

## Why DESIGN.md (not a generic doc)

- Machine-readable YAML tokens + human-readable prose in a single file
- Tokens are the **normative** values; prose provides context for how to apply them
- Compatible with Figma variables, `tokens.json`, and Tailwind theme configs
- Reduces LLM hallucinations by giving agents explicit, structured design constraints

---

## File Structure

```
---
<YAML frontmatter: design tokens>
---

## Overview
## Colors
## Typography
## Layout
## Elevation & Depth
## Shapes
## Components
## Do's and Don'ts
```

Two parts:
1. **YAML frontmatter** — machine-readable design tokens (colors, typography, spacing, rounded, components)
2. **Markdown body** — human-readable rationale and application guidance

---

## YAML Frontmatter Schema

```yaml
---
version: alpha          # optional
name: <string>          # required
description: <string>   # optional

colors:
  <token-name>: "#hexvalue"   # must be #RRGGBB in sRGB

typography:
  <token-name>:
    fontFamily: <string>
    fontSize: <dimension>       # e.g., 16px, 1rem
    fontWeight: <number>        # 400, 500, 700
    lineHeight: <dimension|number>  # 1.5 or 24px
    letterSpacing: <dimension>  # optional
    fontFeature: <string>       # optional, font-feature-settings
    fontVariation: <string>     # optional, font-variation-settings

rounded:
  <scale-level>: <dimension>   # e.g., sm: 4px, full: 9999px

spacing:
  <scale-level>: <dimension|number>  # e.g., base: 8px, md: 16px

components:
  <component-name>:
    backgroundColor: <Color | token-ref>
    textColor: <Color | token-ref>
    typography: <token-ref>
    rounded: <token-ref>
    padding: <dimension | token-ref>
    size: <dimension>
    height: <dimension>
    width: <dimension>
  <component-name>-hover:      # variant pattern for states
    backgroundColor: <token-ref>
---
```

### Token References

Use `{path.to.token}` to cross-reference values:

```yaml
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    rounded: "{rounded.md}"
    padding: "{spacing.md}"
```

---

## Section Order (must follow this sequence)

| # | Section | Also known as |
|---|---|---|
| 1 | **Overview** | "Brand & Style" |
| 2 | **Colors** | — |
| 3 | **Typography** | — |
| 4 | **Layout** | "Layout & Spacing" |
| 5 | **Elevation & Depth** | "Elevation" |
| 6 | **Shapes** | — |
| 7 | **Components** | — |
| 8 | **Do's and Don'ts** | — |

Sections can be **omitted** if not relevant. Present sections must appear in this order.
Duplicate section headings cause file rejection.

---

## Section Guidance

### Overview
Brand personality, target audience, emotional intent. Guides high-level stylistic decisions when
no specific token applies.

### Colors
Semantic role per palette (primary, secondary, tertiary, neutral, surface, error). Prose describes
the palette's personality; tokens define exact hex values.

Recommended token names: `primary`, `secondary`, `tertiary`, `neutral`, `surface`, `on-surface`, `error`

### Typography
9–15 levels typical. Common naming: `headline-lg`, `headline-md`, `body-lg`, `body-md`, `body-sm`,
`label-lg`, `label-md`, `label-sm`.

### Layout
Grid model (fluid vs fixed), spacing philosophy (8px scale is standard).

### Elevation & Depth
For Material Design: tonal surfaces + box-shadow levels. For flat designs: describe alternative
hierarchy methods (borders, color contrast).

### Shapes
Corner radius philosophy. Describe the emotional intent (sharp = engineering precision,
rounded = friendly).

### Components
Cover at minimum: buttons, chips, inputs, cards, lists, tooltips, checkboxes, radio buttons.
Define variants per state (hover, active, disabled).

### Do's and Don'ts
Practical guardrails. Examples:
- "Do use primary color only for the single most important action per screen"
- "Don't override component internal CSS classes — use the overrides mixin"

---

## Recommended Color Token Names (non-normative)

```
primary             on-primary          primary-container    on-primary-container
secondary           on-secondary        secondary-container  on-secondary-container
tertiary            on-tertiary         tertiary-container   on-tertiary-container
error               on-error            error-container      on-error-container
surface             on-surface          surface-variant      on-surface-variant
surface-container   surface-container-low   surface-container-high
inverse-surface     inverse-on-surface  outline             outline-variant
background          on-background
```

---

## Real Example (condensed from paws-and-paths)

```yaml
---
name: Paws & Paths
colors:
  primary: "#855300"
  on-primary: "#ffffff"
  primary-container: "#f59e0b"
  surface: "#f9f9ff"
  on-surface: "#151c27"
  error: "#ba1a1a"
typography:
  display:
    fontFamily: Plus Jakarta Sans
    fontSize: 44px
    fontWeight: "800"
    lineHeight: 52px
  body-md:
    fontFamily: Plus Jakarta Sans
    fontSize: 16px
    fontWeight: "400"
    lineHeight: 1.6
rounded:
  sm: 0.25rem
  md: 0.75rem
  lg: 1rem
  full: 9999px
spacing:
  base: 8px
  xs: 4px
  sm: 12px
  md: 24px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    rounded: "{rounded.lg}"
    padding: "{spacing.md}"
  button-primary-hover:
    backgroundColor: "{colors.primary-container}"
---

## Brand & Style
[prose describing personality...]

## Colors
[prose describing semantic roles...]
```

---

## Angular Material Considerations

Angular Material M3 uses **CSS variables** (`--mat-sys-*`) rather than static hex values. The
DESIGN.md YAML requires concrete hex values. Strategy:

- Use **light-mode** hex values in YAML tokens (the AI generates light-mode UI by default)
- Document dark-mode counterparts in prose
- Map `--mat-sys-*` variable names to DESIGN.md token names in the prose section

Angular Material typography is configured via Sass (`mat.theme()`) and emitted as CSS variables.
Use concrete pixel values and font names in the YAML; reference the Sass configuration in prose.
