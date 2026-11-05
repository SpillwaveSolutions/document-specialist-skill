# Documentation Examples - Table of Contents

---
TOKEN_BUDGET: 150
TIER: 3
LOAD_TRIGGER: On-demand when user needs examples or few-shot learning
DEPENDENCIES: None
---

## Overview

This directory contains **complete, working examples** of professional software documentation. Use these as few-shot examples when generating documentation.

**Load on-demand**: Reference specific examples by their links below, not all at once.

---

## Greenfield Examples (Template-Based)

Examples of creating documentation from scratch using templates.

### Requirements Documentation

**1. Software Requirements Specification (SRS)**
- [greenfield/billing-srs.md](greenfield/billing-srs.md) - Payment processing system (IEEE 830 compliant)
- **Domain**: E-commerce, payments
- **Use for**: High-risk, compliance-critical features

**2. Product Requirements Document (PRD)**
- [greenfield/collaboration-prd.md](greenfield/collaboration-prd.md) - Team collaboration platform
- **Domain**: SaaS, productivity
- **Use for**: Agile feature development

### API Documentation

**3. OpenAPI 3.0 Specification**
- [greenfield/task-api-openapi.yaml](greenfield/task-api-openapi.yaml) - Task management REST API
- **Domain**: Task management
- **Use for**: REST API documentation

### Design Documentation

**4. Software Design Document (SDD)**
- [greenfield/ecommerce-sdd.md](greenfield/ecommerce-sdd.md) - Northstar commerce (arc42, Mermaid, Salt wireframes)
- [greenfield/document-specialist-sdd.md](greenfield/document-specialist-sdd.md) - This skill, same content as root `DESIGN_DOC.md`
- **Template**: [templates/markdown/DESIGN_DOC.md](../templates/markdown/DESIGN_DOC.md)
- **Use for**: System architecture documentation. Save as `DESIGN_DOC.md`.

**5. Architecture document (C4 short form)**
- [greenfield/architecture-doc.md](greenfield/architecture-doc.md) - Northstar C4-first architecture
- **Template**: [templates/markdown/architecture.md](../templates/markdown/architecture.md)
- **Use for**: Context, containers, one sequence, deployment. Save as `docs/architecture.md`.

**6. UI wireframes (PlantUML Salt)**
- [greenfield/ui-wireframes.md](greenfield/ui-wireframes.md) - Folio, Northstar, Pet Clinic screens
- **Use for**: Every user-facing screen. Mermaid does not sketch UI.

**7. Architecture Decision Record (ADR)**
- [greenfield/adr-microservices.md](greenfield/adr-microservices.md) - Choosing microservices over monolith
- **Use for**: Recording architectural decisions

---

## Brownfield Examples (Code-to-Docs)

Examples of documentation reverse-engineered from existing codebases.

### Spring Boot Application
- [brownfield/spring-boot-sdd.md](brownfield/spring-boot-sdd.md) - Pet Clinic SDD recovered from packages, endpoints, and persistence
- **Use for**: Reverse-engineering an arc42 DESIGN_DOC.md from Spring Boot

### FastAPI Application
- [brownfield/fastapi-todo-app/](brownfield/fastapi-todo-app/) - Todo REST API
  - `api-docs.md` - API documentation
  - `openapi.yaml` - Generated OpenAPI spec

### Pulumi Infrastructure
- [brownfield/pulumi-aws-infra/](brownfield/pulumi-aws-infra/) - AWS infrastructure
  - `deployment-docs.md` - Deployment documentation
  - `architecture-diagram.md` - Infrastructure architecture

### Other brownfield
- [brownfield/database-failover-runbook.md](brownfield/database-failover-runbook.md) - Operational runbook example

---

## How to Use These Examples

### For an SDD or architecture document

1. Read `reference/03-design-arc42.md`
2. Load `workflows/design-workflow.md`
3. Load one example: `greenfield/ecommerce-sdd.md` (new system) or `brownfield/spring-boot-sdd.md` (existing code)
4. Use `templates/markdown/DESIGN_DOC.md` or `templates/markdown/architecture.md`
5. If the system has a UI, load `greenfield/ui-wireframes.md` and add Salt screens

### For Greenfield Documentation (Template-Based)

**When creating an SRS:**
1. Read `reference/02-requirements-srs-vs-prd.md` for guidance
2. Load `examples/greenfield/billing-srs.md` as few-shot example
3. Use template from `templates/markdown/requirements-srs.md`
4. Customize with user's context

**When creating a PRD:**
1. Read `reference/02-requirements-srs-vs-prd.md` for guidance
2. Load `examples/greenfield/collaboration-prd.md` as few-shot example
3. Use template from `templates/markdown/requirements-prd.md`
4. Customize with user's context

**When creating OpenAPI spec:**
1. Read `reference/05-api-openapi.md` for guidance
2. Load `examples/greenfield/task-api-openapi.yaml` as few-shot example
3. Use template from `templates/markdown/api-openapi.yaml`
4. Customize with user's API

---

### For Brownfield Documentation (Code-to-Docs)

**When documenting a Spring Boot app:**
1. Read `reference/09-code-to-docs-workflow.md`
2. Load `examples/brownfield/spring-boot-sdd.md` as example output
3. Follow brownfield-workflow.md extraction steps
4. Generate similar documentation as `DESIGN_DOC.md`

**When documenting a FastAPI app:**
1. Read `reference/09-code-to-docs-detection.md`
2. Load `examples/brownfield/fastapi-todo-app/openapi.yaml` as example output
3. Extract from code using brownfield-workflow.md
4. Generate similar documentation

---

## Example Selection Guide

| User Request | Load This Example |
|--------------|-------------------|
| "Create an SRS for a payment system" | `greenfield/billing-srs.md` |
| "Create a PRD for a collaboration tool" | `greenfield/collaboration-prd.md` |
| "Generate OpenAPI spec for a REST API" | `greenfield/task-api-openapi.yaml` |
| "Write DESIGN_DOC.md" / "Document microservices architecture" | `greenfield/ecommerce-sdd.md` |
| "Create an architecture document" | `greenfield/architecture-doc.md` |
| "Draw UI wireframes" | `greenfield/ui-wireframes.md` |
| "Record an architectural decision" | `greenfield/adr-microservices.md` |
| "Document my Spring Boot app" | `brownfield/spring-boot-sdd.md` |
| "Extract API docs from FastAPI" | `brownfield/fastapi-todo-app/openapi.yaml` |
| "Document my infrastructure" | `brownfield/pulumi-aws-infra/deployment-docs.md` |

---

## Progressive Loading Strategy

**Do NOT load all examples upfront.**

1. Classify intent: DESIGN, CREATE_NEW, or CODE_TO_DOCS
2. Identify document type: SRS, PRD, OpenAPI, SDD, architecture
3. Load ONE relevant example
4. Generate documentation

**Example workflow:**
```
User: "Write DESIGN_DOC.md for this checkout service"

Step 1: Intent = DESIGN, DocType = SDD
Step 2: Load workflows/design-workflow.md
Step 3: Load examples/greenfield/ecommerce-sdd.md
Step 4: Load templates/markdown/DESIGN_DOC.md
Step 5: If UI exists, load examples/greenfield/ui-wireframes.md
Step 6: Emit DESIGN_DOC.md
```

---

**End of Examples TOC**
