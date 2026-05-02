# Angular Material Design System (M3)

A **reusable, machine-readable design system specification** for Angular Material Design 3 projects.

This repository provides a complete `DESIGN.md` file that serves as the single source of truth for Angular Material M3 design tokens and component specifications. It's designed for AI coding agents, design tools (Figma), and developer reference.

## 📋 What's in This Repository

### Core Files

- **`DESIGN.md`** — The authoritative design system file
  - YAML frontmatter with design tokens (colors, typography, spacing, shapes, components)
  - Complete Material Design 3 specification
  - Mapped to Angular Material v19+ CSS variables (`--mat-sys-*`)
  - 9 sections: Overview, Colors, Typography, Layout, Elevation, Shapes, Components, Do's/Don'ts
  - **Machine-readable format** for AI agents, design tools, and code generators
  - **New in v1.1**: Added Animation specs, Z-Index ladder, Composition rules, RTL support, and Agent Prompt Guide

- **`DESIGN.md-GUIDE.md`** — How to write DESIGN.md files
  - Complete practitioner's guide
  - Format reference and best practices
  - Examples from real design systems (Stripe, Paws & Paths, etc.)

### Supporting Documentation

- `docs/design-md-format.md` — Reference documentation on the DESIGN.md format standard
- `docs/theming.md` — Angular Material M3 theming guide
- `docs/theming-your-components.md` — How to create theme-aware custom components
- `docs/coding-standards.md` — Angular Material coding standards
- `docs/getting-started.md` — Installation and setup

## 🎯 How to Use DESIGN.md

### For AI Code Generation

Pass the `DESIGN.md` file to AI agents (Claude, ChatGPT, Copilot) when asking them to generate Angular Material components. The YAML tokens + prose specification gives agents:

- Exact color values and semantic roles
- Typography hierarchy (display, headline, title, body, label)
- Component specifications (buttons, cards, forms, etc.)
- Do's and don'ts to avoid common mistakes
- Angular Material-specific patterns

Example:
```
"Generate a Material Design 3 card component for Angular using this DESIGN.md specification..."
[Include DESIGN.md in context]
```

### For Figma / Design Tools

Extract the YAML frontmatter from `DESIGN.md` to sync design tokens:
- Use a design token plugin to import the YAML
- Tokens automatically map to Figma variables
- Keeps design and code in sync

### For Developers

Reference `DESIGN.md` when:
- Building custom components that follow Material Design 3
- Ensuring color/typography consistency
- Understanding component variants and states
- Checking accessibility requirements

Start with the **Do's and Don'ts** section for quick implementation guidance.

## 🎨 Design System Highlights

### Colors
- **Role-based system** (primary, secondary, tertiary, error, surface, outline)
- **Light + Dark modes** via CSS `light-dark()` function
- **WCAG AA compliant** by default
- Maps to `--mat-sys-{name}` CSS variables

### Typography
- **5 categories**: Display, Headline, Title, Body, Label
- **3 sizes each**: Large, Medium, Small
- **M3-compliant** font weights and line heights
- Ready for `mat.theme()` configuration

### Components
- **8 button variants** (filled, tonal, elevated, outlined, text, icon)
- **Form fields** (filled + outlined appearances)
- **Cards** (elevated, filled, outlined)
- **Navigation** patterns (top app bar, navigation rail, drawer, bottom nav)
- **Feedback** (dialogs, snackbars, tooltips, badges)

### Spacing & Shapes
- **8px base grid** with 4px micro-adjustments
- **7-tier radius system** (none → 0px, full → 9999px)
- **Density levels** for compact/comfortable/spacious layouts

## 🚀 Getting Started

1. **View the DESIGN.md file:**
   ```bash
   cat DESIGN.md
   ```

2. **Use it in your project:**
   - Copy `DESIGN.md` to your Angular Material project root
   - Reference it when building components
   - Pass it to AI agents for code generation

3. **Customize for your brand:**
   - Update color hex values in the YAML section
   - Adjust typography families and weights
   - Modify spacing/density preferences
   - Keep the structure and format intact

## 📖 Format Standard

`DESIGN.md` follows the [Google Stitch / design.md](https://stitch.withgoogle.com/docs/design-md/overview/) format:

- **YAML frontmatter** (lines 1-313)
  - Machine-readable tokens
  - Portable to Figma, Tailwind, tokens.json
  - Cross-references: `{colors.primary}`, `{typography.title-lg}`

- **Markdown body** (lines 315+)
  - Human-readable specifications
  - Context and reasoning for design decisions
  - Component usage patterns

This format is **universal** — the same DESIGN.md can be consumed by:
- AI coding agents (Claude, ChatGPT, Copilot)
- Design tools (Figma, Adobe XD)
- Token systems (Tokens Studio, Style Dictionary)
- Code generators (Storybook, Component Kit)

## 🔗 References

- **Material Design 3**: https://m3.material.io/
- **Angular Material**: https://material.angular.dev/
- **DESIGN.md Format**: https://github.com/google-labs-code/design.md
- **Angular Material v19+ Theming**: https://material.angular.dev/guide/theming

## 📝 License

This repository is documentation and reference material. Use it freely in your projects.

---

## Repository Contents

```
.
├── DESIGN.md                          # ⭐ The design system (YAML + prose)
├── DESIGN.md-GUIDE.md                 # Complete guide on writing DESIGN.md
├── README.md                          # This file
├── docs/
│   ├── design-md-format.md           # DESIGN.md format reference
│   ├── theming.md                     # Angular Material M3 theming
│   ├── theming-your-components.md     # Custom component theming
│   ├── theming-material-2.md          # Legacy M2 API reference
│   ├── coding-standards.md            # Code style + API design
│   ├── getting-started.md             # Installation guide
│   ├── component-harnesses.md         # Testing guide
│   ├── custom-form-field-control.md   # Custom form field tutorial
│   ├── custom-stepper.md              # Custom stepper tutorial
│   ├── schematics.md                  # Component generation
│   ├── bidirectionality.md            # RTL support
│   └── repo-overview.md               # Angular Components repo guide
└── .claude/                            # Claude.dev settings
```

---

**Start with `DESIGN.md` and pass it to your AI agent. That's the complete design system.**
