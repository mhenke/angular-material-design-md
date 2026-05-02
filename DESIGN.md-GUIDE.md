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
