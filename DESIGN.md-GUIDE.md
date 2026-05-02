# How to Write a DESIGN.md

A practitioner's guide distilled from 70+ real-world examples at [github.com/VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md).

---

## What Is DESIGN.md?

DESIGN.md is a plain-text design system document introduced by [Google Stitch](https://stitch.withgoogle.com/docs/design-md/overview/). Drop it in your project root and any AI coding agent instantly understands how your UI should look and feel.

It sits alongside AGENTS.md in the same mental model:

| File | Who reads it | What it defines |
|------|-------------|-----------------|
| `AGENTS.md` | Coding agents | How to build the project |
| `DESIGN.md` | Design agents | How the project should look and feel |

**Why markdown?** LLMs read markdown best. No Figma exports, no JSON schemas, no token pipelines — just a file any editor can open. The constraint is the feature: because it's plain text, every AI agent can consume it without tooling.

**Where does it live?** Project root, alongside `README.md`. One file per project.

---
