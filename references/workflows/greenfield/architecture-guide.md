# Architecture Document Guide

---
TOKEN_BUDGET: 220
TIER: 3
LOAD_TRIGGER: DESIGN + architecture document / C4
DEPENDENCIES: design-workflow.md
---

## Default output

Save as `docs/architecture.md`.

Template: [templates/markdown/architecture.md](../../templates/markdown/architecture.md)
Few-shot: [examples/greenfield/architecture-doc.md](../../examples/greenfield/architecture-doc.md)

## Cover

- Purpose
- System context (flowchart)
- Containers
- One sequence, five participants or fewer
- Deployment
- PlantUML Salt for every user-facing screen

This is the short C4 form. For regulated reviews, expand into `DESIGN_DOC.md` using [sdd-guide.md](sdd-guide.md).
