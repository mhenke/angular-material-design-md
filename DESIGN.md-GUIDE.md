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

### 4. Component Stylings

**Purpose:** Give agents exact, state-complete specs for every interactive UI element so generated components match the system without guessing.

**What to include:**
- Buttons: every variant (primary, secondary/ghost, disabled, destructive) with all states
- Cards & containers
- Inputs & forms (label, placeholder, focus, error states)
- Navigation (desktop and mobile treatment)
- Badges / tags / pills
- Per component: background, text color, padding, border-radius, border, hover state, focus state, active/pressed state

**Annotated example:**

~~~markdown
## 4. Component Stylings

### Buttons

**Primary**
- Background: `#533afd`
- Text: `#ffffff`, 16px sohne-var weight 400, `"ss01"`
- Padding: `8px 16px`
- Radius: `4px`
- Hover: background `#4434d4`
- Focus: `2px solid #533afd` outline offset `2px`
- Disabled: `opacity: 0.4`, cursor not-allowed

**Ghost / Outlined**
- Background: transparent
- Text: `#533afd`
- Border: `1px solid #b9b9f9`
- Padding: `8px 16px`
- Radius: `4px`
- Hover: background `rgba(83,58,253,0.05)`

### Cards
- Background: `#ffffff`
- Border: `1px solid #e5edf5`
- Radius: `6px`
- Shadow: `rgba(50,50,93,0.25) 0px 30px 45px -30px, rgba(0,0,0,0.1) 0px 18px 36px -18px`
- Hover: shadow intensifies

### Inputs
- Border: `1px solid #e5edf5`
- Radius: `4px`
- Focus: `1px solid #533afd`
- Label: `#273951`, 14px
- Placeholder: `#64748d`
- Error: `1px solid #ea2261`, label color `#ea2261`
~~~

**Writing guidance:**
- State completeness is the most common failure: a component described only in its default state will be generated with no hover/focus/disabled behavior
- Padding values must be explicit (`8px 16px`), not described in prose ("comfortable padding")
- Navigation must address both desktop (horizontal links + CTA) and mobile (hamburger collapse) — agents building responsive layouts need both
- If a component variant is used only in specific contexts, note when to use it

---

### 5. Layout Principles

**Purpose:** Define the spatial system — the spacing unit, grid, container widths, and whitespace philosophy.

**What to include:**
- Base spacing unit (commonly 4px or 8px) and the scale built from it
- Max container/content width
- Grid structure (columns, gutters, breakpoint behavior)
- Whitespace philosophy in prose — the *feel* of the spacing, not just the numbers
- Border radius scale as named levels (xs/sm/md/lg or Micro/Standard/Large)

**Annotated example:**

~~~markdown
## 5. Layout Principles

### Spacing System
- Base unit: `8px`
- Scale: `4px, 8px, 12px, 16px, 24px, 32px, 48px, 64px`

### Grid & Container
- Max content width: `1080px`, centered
- Hero: single-column, generous horizontal padding
- Feature sections: 3-column grid → 2-column → 1-column on mobile
- Full-width dark brand sections maintain padding rhythm

### Whitespace Philosophy
Stripe uses precision spacing, not generous emptiness. Every gap is a deliberate typographic choice — financial data displays are dense, but the chrome around them is generously spaced.

### Border Radius Scale
| Name | Value | Use |
|------|-------|-----|
| Standard | 4px | Buttons, inputs, badges |
| Comfortable | 6px | Navigation, larger interactive elements |
| Large | 8px | Featured cards, hero elements |
~~~

**Writing guidance:**
- The whitespace philosophy prose is what separates distinctive systems from generic ones — don't skip it
- Name each border-radius level; "shadow-sm / shadow-md" is more useful to agents than anonymous pixel values
- Grid structure should describe behavior across breakpoints, not just column count

---

### 6. Depth & Elevation

**Purpose:** Document the shadow system as a named hierarchy — not as scattered CSS snippets but as a deliberate elevation language.

**What to include:**
- Named levels from flat to highest elevation (typically 4–5 levels)
- Exact shadow CSS value at each level
- A shadow philosophy paragraph explaining why the shadow color was chosen

**Annotated example:**

~~~markdown
## 6. Depth & Elevation

| Level | Shadow | Use |
|-------|--------|-----|
| Flat | none | Page background, inline text |
| Ambient | `rgba(23,23,23,0.06) 0px 3px 6px` | Subtle card lift |
| Standard | `rgba(23,23,23,0.08) 0px 15px 35px` | Standard cards |
| Elevated | `rgba(50,50,93,0.25) 0px 30px 45px -30px, rgba(0,0,0,0.1) 0px 18px 36px -18px` | Featured cards, dropdowns |
| Deep | `rgba(3,3,39,0.25) 0px 14px 21px -14px, rgba(0,0,0,0.1) 0px 8px 17px -8px` | Modals |

**Shadow Philosophy:** Stripe's primary shadow color (`rgba(50,50,93,0.25)`) is a deep blue-gray echoing the navy-purple brand palette. Shadows don't just add depth — they add brand atmosphere. The multi-layer approach pairs the brand-tinted shadow (far, soft) with a neutral black layer (near, tight) to create parallax-like depth.
~~~

**Writing guidance:**
- Always name your shadow levels — agents query by semantic name, not by CSS value
- The shadow philosophy paragraph is not optional: agents that don't understand why the shadow color was chosen will replace it with neutral gray
- Multi-layer shadows should be shown verbatim; agents cannot infer the formula from a description

---

### 7. Do's and Don'ts

**Purpose:** State the design guardrails as explicit rules — the constraints agents must respect even when generating output that "looks fine" to a human eye.

**What to include:**
- Minimum 6 items per side
- Each rule tied to the system's actual design decisions, not generic advice
- Rules phrased specifically enough that violating them produces a measurably wrong output

**Annotated example:**

~~~markdown
## 7. Do's and Don'ts

### Do
- Use sohne-var with `"ss01"` on every text element — the stylistic set IS the brand
- Use weight 300 for all headlines — lightness is the signature
- Apply blue-tinted shadows (`rgba(50,50,93,0.25)`) for all elevated elements
- Use `#061b31` (deep navy) for headings, not `#000000` — the warmth matters
- Keep border-radius between 4px–8px — conservative rounding is intentional
- Use `"tnum"` for any tabular or financial number display

### Don't
- Don't use weight 600–700 for sohne-var headlines — weight 300 is the brand voice
- Don't use large border-radius (12px+, pill shapes) on cards or buttons
- Don't use neutral gray shadows — always tint with blue (`rgba(50,50,93,...)`)
- Don't skip `"ss01"` on any sohne-var text
- Don't use pure black (`#000000`) for headings — always `#061b31`
- Don't apply positive letter-spacing at display sizes — Stripe tracks tight
~~~

**Writing guidance:**
- Vague don'ts are worse than no don'ts: "don't make it look bad" provides no constraint
- The best rules are counterintuitive ones — things an agent would get "wrong" by default (weight 300 at hero size, blue-tinted shadows, navy instead of black)
- Each "Don't" should have a corresponding "Do" — agents need the correct path, not just the wrong one

---

### 8. Responsive Behavior

**Purpose:** Define how the system degrades across viewport widths so agents building responsive layouts have an unambiguous strategy.

**What to include:**
- Breakpoint table: Name | Width | Key Changes
- Touch target minimums (mobile tap targets)
- Collapsing strategy for: navigation, hero type scale, feature grids, section spacing

**Annotated example:**

~~~markdown
## 8. Responsive Behavior

### Breakpoints

| Name | Width | Key Changes |
|------|-------|-------------|
| Mobile | <640px | Single column, reduced heading sizes, stacked cards |
| Tablet | 640–1024px | 2-column grids, moderate padding |
| Desktop | 1024–1280px | Full layout, 3-column feature grids |
| Large | >1280px | Centered content, generous margins |

### Touch Targets
- Minimum tap target: 44×44px on mobile
- Buttons: at least 8px vertical padding
- Nav links: adequate horizontal spacing for thumb navigation

### Collapsing Strategy
- Hero type: 56px → 32px, weight 300 maintained
- Navigation: horizontal links + CTAs → hamburger toggle
- Feature cards: 3-column → 2-column → single column
- Section spacing: `64px` → `40px` on mobile
~~~

**Writing guidance:**
- The collapsing strategy section is what most agents actually need — breakpoints alone don't explain *how* things change
- Touch targets are almost always omitted; include them to prevent agents from generating untappable mobile UI
- Name what stays the same across breakpoints, not just what changes (e.g., "weight 300 maintained")

---

### 9. Agent Prompt Guide

**Purpose:** The section agents reach for first. Provides ready-to-paste color references and component prompts that generate correct output on the first attempt.

**What to include:**
- Quick color reference table: Role → Hex (8–12 rows, the colors agents use most)
- 4–5 example component prompts, one per major surface (hero, card, nav, badge, dark section)
- Iteration tips: numbered list of rules for agents to apply when refining generated output

**This is the most-skipped and highest-value section.** Files without it require agents to re-read the entire document and reconstruct prompts themselves, producing inconsistent output.

**Annotated example:**

~~~markdown
## 9. Agent Prompt Guide

### Quick Color Reference
| Role | Hex |
|------|-----|
| Primary CTA | `#533afd` |
| CTA Hover | `#4434d4` |
| Background | `#ffffff` |
| Heading text | `#061b31` |
| Body text | `#64748d` |
| Border | `#e5edf5` |
| Dark section bg | `#1c1e54` |
| Success | `#15be53` |

### Example Component Prompts

**Hero section:**
"White background. Headline 48px sohne-var weight 300, line-height 1.15, letter-spacing -0.96px, color #061b31, font-feature-settings 'ss01'. Subtitle 18px weight 300, line-height 1.40, color #64748d. Purple CTA (#533afd, 4px radius, 8px 16px padding, white text). Ghost button (transparent, 1px solid #b9b9f9, #533afd text)."

**Card:**
"White background, 1px solid #e5edf5 border, 6px radius. Shadow: rgba(50,50,93,0.25) 0px 30px 45px -30px, rgba(0,0,0,0.1) 0px 18px 36px -18px. Title 22px sohne-var weight 300, letter-spacing -0.22px, color #061b31, 'ss01'. Body 16px weight 300, #64748d."

**Navigation:**
"White sticky header, backdrop-filter blur(12px). Links: 14px sohne-var weight 400, #061b31, 'ss01'. Purple CTA 'Start now' right-aligned (#533afd, white text, 4px radius)."

### Iteration Tips
1. Always set `font-feature-settings: "ss01"` on sohne-var — this is non-negotiable
2. Weight 300 is the default; use 400 only for buttons, links, and navigation
3. Shadow formula: `rgba(50,50,93,0.25) 0px Y1 B1 -S1, rgba(0,0,0,0.1) 0px Y2 B2 -S2`
4. Heading color is `#061b31`, body is `#64748d`, labels are `#273951`
5. Dark sections use `#1c1e54` — not black, not gray
~~~

**Writing guidance:**
- The quick color reference table should cover the ~10 colors agents reach for when writing prompts — not the full palette
- Component prompts should be dense and literal — agents paste them into their context, so they must be self-contained
- Iteration tips should address the most counterintuitive rules (the things agents override by default)
- One prompt per major surface minimum: hero, card, nav. Add badge, dark section, and form if your system has them.

---
