---
name: write-sdd
description: Write DESIGN_DOC.md using the arc42 SDD template, Mermaid-first diagrams, one voice pack.
---

Write a software design document.

1. Load `references/workflows/design-workflow.md`.
2. Load `references/templates/markdown/DESIGN_DOC.md`.
3. Load one example: greenfield `ecommerce-sdd.md` or brownfield `spring-boot-sdd.md`.
4. Apply STE100 unless the user named Google docs style.
5. Save as `DESIGN_DOC.md` (or `docs/DESIGN_DOC.md`).
6. Include context, building-block, sequence, and deployment Mermaid figures.
7. PlantUML Salt wireframe for every user-facing screen. Always PNG or SVG.
8. PlantUML leftover types (use case, timing, ArchiMate, nwdiag, WBS) only when needed, always with PNG or SVG.
