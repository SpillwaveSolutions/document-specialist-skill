---
name: "documentation-specialist"
description: |
  This skill should be used when creating professional software documentation (SRS, PRD, OpenAPI,
  SDD, architecture docs, user manuals, tutorials, runbooks) from templates (greenfield) or reverse-engineering
  documentation from existing code like Spring Boot or FastAPI (brownfield). Also handles documentation
  audits/reviews, format conversion (Markdown, DOCX, PDF), and diagram generation (Mermaid first: C4,
  sequence, class, ER, state, flowchart; PlantUML Salt for UI wireframes and leftover UML). Use when
  asked to "create documentation", "document my code", "write SRS", "generate PRD", "write DESIGN_DOC.md",
  "architecture document", "wireframe", or "documentation specialist".
version: "3.3.0"
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Bash", "Skill"]
---

# Documentation Specialist Skill

## Quick Start

Software documentation creation, extraction, conversion, and diagramming capabilities.

**Capabilities:**
1. **Greenfield** - Create documentation from templates (SRS, PRD, SDD/DESIGN_DOC.md, architecture, OpenAPI, User Manuals, Tutorials, Runbooks)
2. **Brownfield** - Reverse-engineer documentation from code (Spring Boot, FastAPI)
3. **Audit** - Review and improve existing documentation
4. **Convert** - Transform formats (MD to DOCX to PDF)
5. **Diagram** - Mermaid first (C4, sequence, class, ER, state, flowchart). PlantUML Salt for UI wireframes. PlantUML for leftover UML (use case, timing, ArchiMate, nwdiag, WBS).

**Example Requests:**
```
Create an SRS for a billing system with PCI-DSS compliance
Write DESIGN_DOC.md for this repository using arc42
Create an architecture document with C4-style Mermaid
Document my Spring Boot application at ~/projects/customer-api
Create a user manual for my SaaS product
Write a database failover runbook
Audit my API documentation at docs/api/openapi.yaml
Convert docs/srs.md to Word format
Create a C4 container diagram for my microservices
Draw a login wireframe
```

**Execution Flow:**
1. Classify intent to 2. Choose one voice pack to 3. Load workflow to 4. Execute steps to 5. Generate documentation to 6. Present post-processing options

---

## Voice pack (required, pick one)

Every document this skill writes uses **exactly one** voice pack. Do not mix them.

| Pack | When | Source |
|------|------|--------|
| **STE100** (default) | Procedures, runbooks, manuals, architecture docs, code walkthroughs, requirements, and any request that does not name Google style | `ste100` skill (`SpillwaveSolutions/ste100-agent-plugins`) |
| **google-docs-style** | User says "Google style", "Google docs style", or "developer style guide" | `google-docs-style` skill (`SpillwaveSolutions/google-docs-style`) |

**Default is STE100.** Switch only when the user names Google style. If both are named, ask which pack to use. Do not apply both.

### Hard bans (both packs)

These apply even if a template or prior draft used them:

- Do not use an em dash (`—`) or a double hyphen standing in for one (`--` as punctuation). Use a period or a comma.
- Do not start a sentence with **So**, **That**, **Thus**, or **Hence**.
- Do not start a sentence with a dangling demonstrative ("That is why..." as a lead).

STE100 also requires: short sentences, one instruction per step, active voice, no contractions, no `e.g.` / `i.e.` / `etc.`, no weak modals in steps. Load [11-voice-and-style.md](references/reference/11-voice-and-style.md).

After the draft exists, run the chosen pack:

- STE100: follow the local orchestrator / editor / adversary loop in the `ste100` skill. No network.
- Google style: run `python3 scripts/google_docs_style.py --lint --check` when that skill is installed.

---

## Intent Classification

| Intent | Keywords | Workflow |
|--------|----------|----------|
| **CREATE_NEW** | "create", "generate", "write" + doc type | [greenfield-workflow.md](references/workflows/greenfield-workflow.md) |
| **DESIGN** | "DESIGN_DOC.md", "SDD", "software design document", "arc42", "architecture document", "architecture.md" | [design-workflow.md](references/workflows/design-workflow.md) |
| **CODE_TO_DOCS** | "document", "extract", path reference | [brownfield-workflow.md](references/workflows/brownfield-workflow.md) |
| **AUDIT** | "audit", "review", "check", "improve" | [audit-workflow.md](references/workflows/audit-workflow.md) |
| **CONVERT** | "convert", "to Word", "to PDF" | [convert-workflow.md](references/workflows/convert-workflow.md) |
| **DIAGRAM** | "diagram", "C4", "sequence", "ER", "class", "state", "wireframe", "mock", "Salt" | [diagram-workflow.md](references/workflows/diagram-workflow.md) |
| **USER_DOCS** | "user manual", "how-to", "getting started" | [user-docs-workflow.md](references/workflows/user-docs-workflow.md) |
| **TUTORIAL** | "tutorial", "API guide", "CLI docs" | [tutorial-workflow.md](references/workflows/tutorial-workflow.md) |
| **RUNBOOK** | "runbook", "procedure", "incident" | [runbook-workflow.md](references/workflows/runbook-workflow.md) |

**CRITICAL**: Load only the workflow needed for the current intent. Avoid loading multiple workflows.

When intent is DESIGN, save the SDD as `DESIGN_DOC.md` (or `docs/DESIGN_DOC.md`). Save the short C4 form as `docs/architecture.md`.

---

## Document Type to Template

**Requirements and Design:**
| Type | Template | Default output |
|------|----------|----------------|
| SRS | [requirements-srs.md](references/templates/markdown/requirements-srs.md) | `docs/srs.md` |
| PRD | [requirements-prd.md](references/templates/markdown/requirements-prd.md) | `docs/prd.md` |
| SDD (arc42) | [DESIGN_DOC.md](references/templates/markdown/DESIGN_DOC.md) | `DESIGN_DOC.md` |
| Architecture (C4 short) | [architecture.md](references/templates/markdown/architecture.md) | `docs/architecture.md` |
| OpenAPI | [api-openapi.yaml](references/templates/markdown/api-openapi.yaml) | `openapi.yaml` |

**User Documentation:**
| Type | Template |
|------|----------|
| User Manual | [user-manual.md](references/templates/markdown/user-manual.md) |
| How-To Guide | [howto-guide.md](references/templates/markdown/howto-guide.md) |
| Getting Started | [getting-started.md](references/templates/markdown/getting-started.md) |

**Developer and Operations:**
| Type | Template |
|------|----------|
| Developer Tutorial | [developer-tutorial.md](references/templates/markdown/developer-tutorial.md) |
| Runbook | [runbook.md](references/templates/markdown/runbook.md) |

---

## Framework Detection (Brownfield)

| Framework | Detection | Mapping |
|-----------|-----------|---------|
| **Spring Boot** | `pom.xml`, `@SpringBootApplication` | [spring-boot-mapping.yaml](references/mappings/backend/spring-boot-mapping.yaml) |
| **FastAPI** | `requirements.txt`, `from fastapi import` | [fastapi-mapping.yaml](references/mappings/backend/fastapi-mapping.yaml) |

**Process**: Glob for detection files to Grep for patterns to Load mapping to Follow brownfield workflow

---

## On-Demand Resources

Load only what is needed for the current task.

### Workflows
- [Workflow TOC](references/workflows/TOC.md) - Navigation index
- [design-workflow.md](references/workflows/design-workflow.md)
- [greenfield-workflow.md](references/workflows/greenfield-workflow.md)
- [brownfield-workflow.md](references/workflows/brownfield-workflow.md)
- [audit-workflow.md](references/workflows/audit-workflow.md)
- [convert-workflow.md](references/workflows/convert-workflow.md)
- [diagram-workflow.md](references/workflows/diagram-workflow.md)
- [user-docs-workflow.md](references/workflows/user-docs-workflow.md)
- [tutorial-workflow.md](references/workflows/tutorial-workflow.md)
- [runbook-workflow.md](references/workflows/runbook-workflow.md)

### Reference Guides
- [comprehensive-guide.md](references/reference/comprehensive-guide.md) - Navigation to all 27 reference guides
- [11-voice-and-style.md](references/reference/11-voice-and-style.md) - STE100 vs Google style, hard bans
- [04-diagrams-selection.md](references/reference/04-diagrams-selection.md) - Mermaid first, PlantUML leftover types, Salt UI wireframes
- [03-design-arc42.md](references/reference/03-design-arc42.md) - The twelve arc42 sections

### Examples
- [Examples TOC](references/examples/TOC.md) - Navigation to all examples
- DESIGN: [ecommerce-sdd.md](references/examples/greenfield/ecommerce-sdd.md), [architecture-doc.md](references/examples/greenfield/architecture-doc.md), [ui-wireframes.md](references/examples/greenfield/ui-wireframes.md)
- Brownfield SDD: [spring-boot-sdd.md](references/examples/brownfield/spring-boot-sdd.md)
- This skill's own SDD: [DESIGN_DOC.md](DESIGN_DOC.md)

---

## Skill Integration

| Skill | Invocation Trigger |
|-------|-------------------|
| **ste100** | Default voice pack. Procedures, runbooks, architecture docs, walkthroughs, requirements |
| **google-docs-style** | User names Google style. Mutually exclusive with ste100 |
| **design-doc-mermaid** | Default diagrams: C4, flowchart, sequence, class, ER, state, component views. GitHub wiki renders the fence. |
| **plantuml** | UI wireframes (Salt), use case, timing, ArchiMate, nwdiag, WBS. Always PNG or SVG |
| **docx** | Request includes Word format |
| **pdf** | Request includes PDF format |

When WikiTicket SDD asks for an architecture doc, a code walkthrough, or a
requirements doc, use this skill for prose and wireframes, `design-doc-mermaid`
for every GitHub-safe diagram, and `plantuml` only for leftover types.

**GitHub wiki:** embed Mermaid. Upload PlantUML images with the page.
**Confluence:** render Mermaid and PlantUML to PNG or SVG and upload both.

---

## Error Handling

| Error | Response |
|-------|----------|
| Cannot detect framework | Ask: "Is this Spring Boot, FastAPI, or another framework?" |
| Missing template | Use closest match, inform user |
| Skill not available | Offer markdown-only alternative |
| Ambiguous request | Ask: "Would you prefer SRS (formal), PRD (agile), or DESIGN_DOC.md (arc42)?" |
| Both voice packs named | Ask which pack to use. Do not mix |
| User-facing UI with no Salt | Add one PlantUML Salt wireframe per screen. Do not use a Mermaid flowchart as a stand-in |

---

**End of SKILL.md (v3.3.0)**
