---
name: "documentation-specialist"
description: |
  This skill should be used when creating professional software documentation (SRS, PRD, OpenAPI,
  user manuals, tutorials, runbooks) from templates (greenfield) or reverse-engineering documentation
  from existing code like Spring Boot or FastAPI (brownfield). Also handles documentation audits/reviews,
  format conversion (Markdown, DOCX, PDF), and diagram generation (C4, Mermaid, PlantUML, ER, sequence).
  Use when asked to "create documentation", "document my code", "write SRS", "generate PRD", or "documentation specialist".
version: "3.1-PDA"
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Bash", "Skill"]
---

# Documentation Specialist Skill

## Quick Start

Software documentation creation, extraction, conversion, and diagramming capabilities.

**Capabilities:**
1. **Greenfield** - Create documentation from templates (SRS, PRD, OpenAPI, User Manuals, Tutorials, Runbooks)
2. **Brownfield** - Reverse-engineer documentation from code (Spring Boot, FastAPI)
3. **Audit** - Review and improve existing documentation
4. **Convert** - Transform formats (MD → DOCX → PDF)
5. **Diagram** - Generate visuals (Mermaid C4, PlantUML UML)

**Example Requests:**
```
Create an SRS for a billing system with PCI-DSS compliance
Document my Spring Boot application at ~/projects/customer-api
Create a user manual for my SaaS product
Write a database failover runbook
Audit my API documentation at docs/api/openapi.yaml
Convert docs/srs.md to Word format
Create a C4 container diagram for my microservices
```

**Execution Flow:**
1. Classify intent → 2. Choose one voice pack → 3. Load workflow → 4. Execute steps → 5. Generate documentation → 6. Present post-processing options

---

## Voice pack (required, pick one)

Every document this skill writes uses **exactly one** voice pack. Do not mix them.

| Pack | When | Source |
|------|------|--------|
| **STE100** (default) | Procedures, runbooks, manuals, architecture docs, code walkthroughs, and any request that does not name Google style | `ste100` skill (`SpillwaveSolutions/ste100-agent-plugins`) |
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
| **CODE_TO_DOCS** | "document", "extract", path reference | [brownfield-workflow.md](references/workflows/brownfield-workflow.md) |
| **AUDIT** | "audit", "review", "check", "improve" | [audit-workflow.md](references/workflows/audit-workflow.md) |
| **CONVERT** | "convert", "to Word", "to PDF" | [convert-workflow.md](references/workflows/convert-workflow.md) |
| **DIAGRAM** | "diagram", "C4", "sequence", "ER" | [diagram-workflow.md](references/workflows/diagram-workflow.md) |
| **USER_DOCS** | "user manual", "how-to", "getting started" | [user-docs-workflow.md](references/workflows/user-docs-workflow.md) |
| **TUTORIAL** | "tutorial", "API guide", "CLI docs" | [tutorial-workflow.md](references/workflows/tutorial-workflow.md) |
| **RUNBOOK** | "runbook", "procedure", "incident" | [runbook-workflow.md](references/workflows/runbook-workflow.md) |

**CRITICAL**: Load only the workflow needed for the current intent. Avoid loading multiple workflows.

---

## Document Type → Template

**Requirements & Design:**
| Type | Template |
|------|----------|
| SRS | [requirements-srs.md](references/templates/markdown/requirements-srs.md) |
| PRD | [requirements-prd.md](references/templates/markdown/requirements-prd.md) |
| OpenAPI | [api-openapi.yaml](references/templates/markdown/api-openapi.yaml) |

**User Documentation:**
| Type | Template |
|------|----------|
| User Manual | [user-manual.md](references/templates/markdown/user-manual.md) |
| How-To Guide | [howto-guide.md](references/templates/markdown/howto-guide.md) |
| Getting Started | [getting-started.md](references/templates/markdown/getting-started.md) |

**Developer & Operations:**
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

**Process**: Glob for detection files → Grep for patterns → Load mapping → Follow brownfield workflow

---

## On-Demand Resources

Load only what is needed for the current task.

### Workflows
- [Workflow TOC](references/workflows/TOC.md) - Navigation index
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

### Examples
- [Examples TOC](references/examples/TOC.md) - Navigation to all examples

---

## Skill Integration

| Skill | Invocation Trigger |
|-------|-------------------|
| **ste100** | Default voice pack. Procedures, runbooks, architecture docs, walkthroughs |
| **google-docs-style** | User names Google style. Mutually exclusive with ste100 |
| **design-doc-mermaid** | C4, flowchart, architecture, sequence for GitHub/wiki Markdown |
| **plantuml** | UML that needs class/ER/state/component depth, or image export |
| **docx** | Request includes Word format |
| **pdf** | Request includes PDF format |

When WikiTicket SDD asks for an architecture doc or a code walkthrough, use this skill for prose, `design-doc-mermaid` for GitHub-safe diagrams, and `plantuml` when a class, ER, or component diagram needs UML precision. Embed Mermaid in the Markdown. Keep PlantUML as `.puml` plus a rendered PNG/SVG link.

---

## Error Handling

| Error | Response |
|-------|----------|
| Cannot detect framework | Ask: "Is this Spring Boot, FastAPI, or another framework?" |
| Missing template | Use closest match, inform user |
| Skill not available | Offer markdown-only alternative |
| Ambiguous request | Ask: "Would you prefer SRS (formal) or PRD (agile)?" |
| Both voice packs named | Ask which pack to use. Do not mix |

---

**End of SKILL.md (v3.1-PDA)**
