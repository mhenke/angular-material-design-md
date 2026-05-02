# How to Write a DESIGN.md

A practitioner's guide to authoring DESIGN.md files, with patterns from [github.com/VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md).

---

## What Is DESIGN.md?

DESIGN.md is a plain-text design system document introduced by [Google Stitch](https://stitch.withgoogle.com/docs/design-md/overview/). Drop it in your project root and any AI coding agent understands how your UI should look and feel.

It sits alongside AGENTS.md in the same mental model:

| File | Who reads it | What it defines |
|------|-------------|-----------------|
| `AGENTS.md` | Coding agents | How to build the project |
| `DESIGN.md` | Design agents | How the project should look and feel |

**Why markdown?** LLMs process markdown natively — it's universally readable, requires no conversion tooling, and every editor can open it. Plain text is the feature.

**Where does it live?** Project root, alongside `README.md`. One file per project.

---

## Section Reference

The nine sections below are the standard structure. Every DESIGN.md should include all nine. Each entry shows: purpose, what to include, an annotated example, and (where relevant) the YAML-frontmatter variant.

---

### 1. Visual Theme & Atmosphere

**Purpose:** Set the emotional register and identify the single most distinctive design decision.

**What to include:**
- 2–3 paragraphs of evocative prose — not a spec list, but a description of what someone *feels* when they land on the site
- Name the defining element explicitly: the custom font, the shadow system, the color philosophy, the density
- Close with a **Key Characteristics** bullet list (5–8 items) that gives agents a scannable summary

**Annotated example:**

~~~markdown
## 1. Visual Theme & Atmosphere

Stripe's website is the gold standard of fintech design — a system that manages to feel
simultaneously technical and luxurious. The page opens on a clean white canvas (`#ffffff`)
with deep navy headings (`#061b31`) and a signature purple (`#533afd`) that functions as
both brand anchor and interactive accent.

The custom `sohne-var` variable font is the defining element. Every text element enables
the OpenType `"ss01"` stylistic set, which modifies character shapes for a distinctly
geometric, modern feel.

**Key Characteristics:**
- sohne-var with OpenType `"ss01"` on all text — a custom stylistic set that defines letterforms
- Weight 300 as the signature headline weight — light, confident, anti-convention
- Negative letter-spacing at display sizes (-1.4px at 56px)
- Blue-tinted multi-layer shadows using `rgba(50,50,93,0.25)`
- Deep navy (`#061b31`) headings instead of black
- Conservative border-radius (4px–8px)
~~~

**Writing guidance:**
- Name the emotional register explicitly: "clinical", "luxurious", "terminal-native", "editorial warmth"
- Every vague word ("clean", "minimal", "modern") must be anchored to a specific value or technique
- The Key Characteristics list should be what agents scan first — make each bullet self-contained

---

### 2. Color Palette & Roles

**Purpose:** Define every color the system uses, organized by function — not as a gallery, but as a lookup table agents can query by role.

**What to include:**
- Organized sub-groups: Primary, Secondary/Accent, Surfaces, Neutrals, Shadows, Semantic (success/error/warning)
- Per color: semantic name + hex value + CSS variable name (if known) + one-sentence functional role
- Shadow colors as first-class entries — they are brand decisions, not implementation details
- At least one dark surface even in light-mode systems

**Annotated example (markdown format):**

~~~markdown
## 2. Color Palette & Roles

### Primary
- **Stripe Purple** (`#533afd`): Primary brand color, CTA backgrounds, link text, interactive highlights.
- **Deep Navy** (`#061b31`): `--hds-color-heading-solid`. Primary heading color — not black, a very dark blue adding warmth.
- **Pure White** (`#ffffff`): Page background, card surfaces, button text on dark.

### Shadow Colors
- **Shadow Blue** (`rgba(50,50,93,0.25)`): The signature — blue-tinted primary shadow. Echoes the navy-purple brand palette.
- **Shadow Black** (`rgba(0,0,0,0.1)`): Secondary shadow layer for depth reinforcement.
~~~

**YAML-frontmatter variant:**

~~~yaml
colors:
  primary: "#533afd"
  on-primary: "#ffffff"
  ink: "#061b31"
  canvas: "#ffffff"
  surface-1: "#f6f9fc"
  hairline: "#e5edf5"
  shadow-brand: "rgba(50,50,93,0.25)"
  shadow-neutral: "rgba(0,0,0,0.1)"
~~~

In the YAML variant, use semantic key names (`ink`, `canvas`, `hairline`, `on-primary`) rather than brand names. The YAML format is consumed programmatically; the markdown format is read by agents as prose.

**Writing guidance:**
- Never list colors without roles — a hex dump with no context is useless to an agent
- Group shadows separately; agents treat them as elevation tokens, not palette entries
- Include the CSS variable name when you know it — agents can use it to reference the live site's token

---

### 3. Typography Rules

**Purpose:** Give agents the complete typographic system — fonts, fallbacks, the full hierarchy, and the principles behind size/weight/spacing choices.

**What to include:**
- Font family declaration with full fallback stack
- OpenType features enabled globally (e.g., `"ss01"` for stylistic sets, `"liga"` for ligatures, `"tnum"` for tabular numerals)
- Hierarchy table with columns: Role | Font | Size | Weight | Line Height | Letter Spacing | Notes
- 3–5 typography principles explaining the *why* behind distinctive choices

**Annotated example:**

~~~markdown
## 3. Typography Rules

### Font Family
- **Primary**: `sohne-var`, fallback: `SF Pro Display, -apple-system, sans-serif`
- **Monospace**: `SourceCodePro`, fallback: `SFMono-Regular, Menlo, monospace`
- **OpenType Features**: `"ss01"` on all sohne-var text; `"tnum"` for financial data.

### Hierarchy

| Role | Font | Size | Weight | Line Height | Letter Spacing | Notes |
|------|------|------|--------|-------------|----------------|-------|
| Display Hero | sohne-var | 56px | 300 | 1.03 | -1.4px | ss01 |
| Section Heading | sohne-var | 32px | 300 | 1.10 | -0.64px | ss01 |
| Body | sohne-var | 16px | 300–400 | 1.40 | normal | ss01 |
| Code Body | SourceCodePro | 12px | 500 | 2.00 | normal | — |

### Principles
- Weight 300 at display sizes is the brand's signature — lightness as luxury
- `"ss01"` is non-negotiable; it modifies glyphs to create the geometric, contemporary feel
- Progressive tracking: letter-spacing tightens proportionally with size
~~~

**YAML-frontmatter variant:**

~~~yaml
typography:
  display-xl:
    fontFamily: sohne-var
    fontSize: 56px
    fontWeight: 300
    lineHeight: 1.03
    letterSpacing: -1.4px
  body:
    fontFamily: sohne-var
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.40
    letterSpacing: normal
~~~

**Writing guidance:**
- Fallback stacks are not optional — agents render with system fonts when custom fonts are unavailable; without fallbacks the output looks broken
- Letter-spacing must be exact pixel values, not relative words like "tight" — agents cannot translate "tight" to a number
- The principles section is where you explain the *why*; without it, agents will override correct but counterintuitive choices (e.g., weight 300 at 56px)
- OpenType features are often skipped and almost always important — `"ss01"` can change the entire character of a font

---
