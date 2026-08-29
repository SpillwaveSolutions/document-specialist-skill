# Design document workflow

TOKEN_BUDGET: 480  
TIER: 2  
LOAD_TRIGGER: Intent = DESIGN  
DEPENDENCIES: SKILL.md

## Overview

Write a software design document or a shorter architecture document. Default filename is `DESIGN_DOC.md`. Default outline is arc42. Default diagrams are Mermaid. PlantUML is leftover types only.

## Step 1: Identify the document shape

| Request contains | Document | Template | Example |
|------------------|----------|----------|---------|
| SDD, software design, DESIGN_DOC, arc42 | SDD | templates/markdown/DESIGN_DOC.md | examples/greenfield/ecommerce-sdd.md |
| architecture document, C4, system context | Architecture | templates/markdown/architecture.md | examples/greenfield/architecture-doc.md |
| ADR, architecture decision | ADR | reference/03-design-adrs.md | examples/greenfield/adr-microservices.md |
| document my code, brownfield, existing service | Brownfield SDD | templates/markdown/DESIGN_DOC.md | examples/brownfield/spring-boot-sdd.md |

If the user says "design document" without naming arc42, use the SDD template and save `DESIGN_DOC.md`.

## Step 2: Pick the voice pack

One pack per document.

- Default: STE100
- If the user names Google style, Google docs style, or developer style guide: google-docs-style
- Hard bans always: no em dash, no leading So / That / Thus / Hence

## Step 3: Load one template and one example

Do not load every example. Load the matching row from Step 1. For brownfield, also load the framework mapping (Spring Boot or FastAPI).

## Step 4: Extract facts

Greenfield: name, domain, actors, quality goals, constraints, major use cases.  
Brownfield: tree, entrypoints, datastores, message buses, deploy manifests. Quote file paths. Do not invent classes.

## Step 5: Write the twelve sections (SDD) or the C4 set (architecture)

Fill every `[placeholder]`. Give requirements stable IDs. Map building blocks back to those IDs.

## Step 6: Draw figures

Follow diagram-workflow.md.

Required for an SDD:

- Context flowchart
- Building-block flowchart
- One sequence, five participants or fewer
- State or ER when the domain has a lifecycle or a schema
- Deployment flowchart
- PlantUML Salt wireframe for every user-facing screen

Cap nodes at about 16. If GitHub cannot render C4, use `flowchart TD`.

PlantUML for UI wireframes (Salt), use case, timing, ArchiMate, nwdiag, WBS. Always render PNG or SVG and link the image. Do not use a Mermaid flowchart as a stand-in for a screen. Load `examples/greenfield/ui-wireframes.md` as the Salt few-shot.

## Step 7: Save and offer next steps

Save as:

- `DESIGN_DOC.md` or `docs/DESIGN_DOC.md` for an SDD
- `docs/architecture.md` for the short form
- `docs/adr/ADR-NNN-title.md` for a decision

Then offer: Word, PDF, extra diagrams, related SRS or OpenAPI.

## Quality checklist

- Front matter complete
- All twelve arc42 sections present for an SDD
- At least the required figures
- No em dash
- One voice pack
- Paths and type names verified against the repo for brownfield
- Glossary covers every acronym introduced
