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
