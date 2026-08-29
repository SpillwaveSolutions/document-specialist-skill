# SDD Generation Guide

---
TOKEN_BUDGET: 280
TIER: 3
LOAD_TRIGGER: DESIGN or CREATE_NEW + SDD / DESIGN_DOC.md
DEPENDENCIES: design-workflow.md
---

## Default output

Save as `DESIGN_DOC.md` at the project root, or `docs/DESIGN_DOC.md`.

Template: [templates/markdown/DESIGN_DOC.md](../../templates/markdown/DESIGN_DOC.md)
Few-shot: [examples/greenfield/ecommerce-sdd.md](../../examples/greenfield/ecommerce-sdd.md)
This skill: [DESIGN_DOC.md](../../../DESIGN_DOC.md)

## The twelve arc42 sections

1. Introduction and goals
2. Constraints
3. Context and scope
4. Solution strategy
5. Building block view
6. Runtime view
7. Deployment view
8. Crosscutting concepts
9. Architectural decisions
10. Quality requirements
11. Risks and technical debt
12. Glossary

## Required figures

- Context flowchart (section 3)
- Building-block flowchart (section 5)
- One sequence, five participants or fewer (section 6)
- State or ER when the domain has a lifecycle or a schema
- Deployment flowchart (section 7)
- PlantUML Salt wireframe for every user-facing screen

Mermaid first. PlantUML leftover types always PNG or SVG.

## Voice

STE100 default. Google docs style only when named. No em dash. No leading So / That / Thus / Hence.

If the user asked for a short architecture document instead, use [architecture-guide.md](architecture-guide.md).
