# DESIGN.md Guide — Spec

**Date:** 2026-05-02
**Topic:** A practitioner's guide to writing DESIGN.md files
**Research source:** github.com/VoltAgent/awesome-design-md (70+ files, 69k stars)

---

## Goal

Produce a single markdown guide saved as `DESIGN.md-GUIDE.md` in the project root that teaches any reader — developer, designer, or AI agent — how to write a high-quality DESIGN.md file. The guide is distilled from patterns found across 70+ real-world examples in the VoltAgent awesome-design-md collection.

---

## Structure: Three Layers

### Layer 1 — Introduction (~150 words)

- What DESIGN.md is and where it came from (Google Stitch origin)
- Why plain markdown beats JSON schemas, Figma exports, and design tokens for LLM consumption
- The AGENTS.md analogy table:

| File | Who reads it | What it defines |
|------|-------------|-----------------|
| `AGENTS.md` | Coding agents | How to build the project |
| `DESIGN.md` | Design agents | How the project should look and feel |

- Where to place the file (project root)

---

### Layer 2 — Section-by-Section Reference

Nine sections, each entry includes:
- **Purpose** — one-sentence description
- **What to include** — concrete requirements
- **Minimal example** — real annotated snippet
- **YAML variant note** — where the structured frontmatter format differs significantly (applies primarily to Colors and Typography)

#### Sections covered:

1. **Visual Theme & Atmosphere**
   - 2–3 paragraphs of evocative prose naming the emotional register, not just specs
   - Key Characteristics bullet list (5–8 items)
   - Names the defining element (font, shadow, color philosophy)

2. **Color Palette & Roles**
   - Organized by function: Primary, Secondary/Accent, Surfaces, Neutrals, Shadows, Semantic
   - Each color: name + hex + CSS variable (if known) + functional role
   - Shadow colors included as named entries (not afterthoughts)
   - YAML variant: flat `colors:` map with semantic keys

3. **Typography Rules**
   - Font family with fallback stack
   - OpenType features enabled globally (e.g., `"ss01"`, `"liga"`, `"tnum"`)
   - Hierarchy table: Role | Font | Size | Weight | Line Height | Letter Spacing | Notes
   - Typography principles (3–5 bullets on the "why" behind the choices)

4. **Component Stylings**
   - Buttons: every variant (primary, secondary, ghost, disabled) with all states
   - Cards & containers
   - Inputs & forms
   - Navigation
   - Badges/tags
   - Each component: background, text, padding, radius, border, hover/focus/active states

5. **Layout Principles**
   - Base spacing unit and scale
   - Max container width
   - Grid structure (columns, gutters)
   - Whitespace philosophy (prose, not just numbers)
   - Border radius scale as named levels

6. **Depth & Elevation**
   - Named levels (Flat → Ambient → Standard → Elevated → Deep)
   - Exact shadow values per level
   - Shadow philosophy (why the shadow color was chosen)

7. **Do's and Don'ts**
   - Minimum 6 items per side
   - Specific, not generic ("don't use weight 700 for headlines" not "don't make it ugly")
   - Tied to the system's actual rules, not general advice

8. **Responsive Behavior**
   - Breakpoint table: Name | Width | Key Changes
   - Touch target minimums
   - Collapsing strategy for: nav, hero type scale, feature grids, spacing

9. **Agent Prompt Guide**
   - Quick color reference table (role → hex)
   - 4–5 example component prompts (ready-to-paste)
   - Iteration tips numbered list

---

### Layer 3 — Patterns & Anti-Patterns

Distilled from 70+ files. Grouped into five areas:

**Colors**
- Semantic naming beats hex dumps — agents need role context, not a palette dump
- Shadow colors belong in the palette — they are brand decisions, not CSS implementation details
- Include at least one "dark surface" color even for light-mode systems

**Typography**
- Always include font fallback stacks — agents use fallbacks when custom fonts are unavailable
- Letter-spacing is identity — document exact values, not just "tight" or "loose"
- Note OpenType features; skipping them produces generic output even with the right font
- Two-column tables (role + specs) outperform prose lists for hierarchy

**Section 1 (Visual Theme) writing quality**
- Name the emotional register explicitly ("clinical", "luxurious", "terminal-native")
- Reference a defining differentiator — the thing that makes this system unmistakable
- Avoid vague descriptors ("clean", "modern", "minimal") without anchoring them to a specific choice

**Section 9 (Agent Prompt Guide) — most skipped, highest value**
- This is the section agents use most in practice
- Concrete prompts let agents generate correct output on the first attempt
- Include at least one prompt per major surface (hero, card, nav)

**Anti-patterns observed**
- Color sections that list hex values with no role context
- Typography sections with no line-height or letter-spacing
- Components described in prose only (no state breakdown)
- Section 9 absent or reduced to a single sentence
- No font fallback stack listed
- Responsive section missing touch targets
- Shadows omitted entirely

---

### Closing — Quick-Start Checklist

Nine checkboxes, one per section. Suitable for human use and for an agent to verify a DESIGN.md before shipping.

---

## Format Notes

- File written as standard markdown (`.md`), no special tooling required
- Code blocks for all example snippets
- Tables for hierarchy, color roles, breakpoints
- Prose for philosophy/principles sections
- Both pure-markdown and YAML-frontmatter format styles documented side by side where they differ
- Target length: 600–900 lines (comprehensive but not padded)
