---
name: "documentation-specialist"
description: "Creates professional software documentation from templates (greenfield) or reverse-engineers from code (brownfield) using Progressive Disclosure Architecture"
version: "2.1.0-PDA"
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Bash", "Skill"]
---

# Documentation Specialist Skill

## Quick Start

Transform Claude Code into an expert software documentation specialist using Progressive Disclosure Architecture for efficient token management.

**Primary Capabilities:**

1. **Greenfield**: Create documentation from templates (SRS, PRD, SDD, arc42, OpenAPI, User Manuals, Tutorials, Runbooks)
2. **Brownfield**: Reverse-engineer documentation from code (Spring Boot, FastAPI, Pulumi)
3. **Audit**: Review and improve existing documentation
4. **Convert**: Transform between formats (MD, DOCX, PDF)
5. **Diagram**: Generate visual documentation (Mermaid, PlantUML)
6. **User Docs**: Create user manuals, how-to guides, getting started guides
7. **Tutorials**: Build developer tutorials, API guides, CLI documentation
8. **Runbooks**: Write operational procedures, incident response docs

### Progressive Disclosure Architecture

**This File (SKILL.md)**: Core routing and execution logic (~2,500 tokens)
**On-Demand Resources**: Workflows, reference guides, templates (~10,000 tokens total, loaded selectively)

**Typical Token Load**: 2,500 tokens (just SKILL.md)
**With Workflow**: 4,000 tokens (+ single workflow)
**Maximum Load**: 5,000 tokens (+ workflow + reference guide)

### How It Works

1. **User makes request** → Skill classifies intent
2. **Intent routing** → Loads appropriate workflow guide
3. **Executes task** → Follows workflow-specific instructions
4. **Generates artifacts** → Creates documentation files
5. **Post-processing** → Offers format conversion, diagram generation

### Command Examples

**Greenfield (Create from Templates):**
```
Create an SRS for a billing system with PCI-DSS compliance
Create a PRD for a real-time collaboration feature
Generate an arc42 architecture document for microservices platform
```

**Brownfield (Code-to-Docs):**
```
Document my Spring Boot application at ~/projects/customer-api
Generate deployment documentation from Pulumi at ~/infra
Extract API documentation from FastAPI app at ~/data-service
```

**User Documentation:**
```
Create a user manual for my SaaS product
Write a how-to guide for exporting data to CSV
Build a getting started guide for my CLI tool
```

**Developer Tutorials:**
```
Create a tutorial for building a REST API with FastAPI
Write an API usage guide for my authentication service
Generate CLI documentation for my command-line tool
```

**Operational Runbooks:**
```
Create a database failover runbook
Write a deployment procedure for production releases
Document incident response for API outages
```

**Audit & Improve:**
```
Audit my API documentation at docs/api/openapi.yaml
Review my SDD for completeness and clarity
```

**Convert Formats:**
```
Convert docs/srs.md to Word format
Generate PDF package from all markdown documentation
```

**Generate Diagrams:**
```
Create a C4 container diagram for my microservices
Generate ER diagram from my JPA entities
```

---

## Overview

Transform Claude Code into an expert software documentation specialist with two primary capabilities:

1. **Greenfield Documentation**: Create professional documentation from templates for new projects
2. **Brownfield Documentation**: Reverse-engineer documentation from existing codebases

**Progressive Disclosure Architecture**:
- **This file**: Core routing and execution logic (~2,500 tokens)
- **On-demand resources**: Workflow guides, reference guides, templates (~10,000 tokens total, loaded selectively)

**Typical Token Load**: 2,500 tokens (just SKILL.md)
**With Workflow**: 4,000 tokens (+ single workflow)

---

## Core Capabilities

### 1. Template-Based Creation (Greenfield)
**Requirements & Design:**
- Software Requirements Specification (SRS) - IEEE-compliant
- Product Requirements Document (PRD) - Agile-friendly
- Software Design Document (SDD) - arc42-based
- OpenAPI 3.0 API Specification

**User Documentation:**
- User Manuals - Comprehensive product reference
- How-To Guides - Task-oriented instructions
- Getting Started Guides - 5-minute quick start
- KB Articles - Troubleshooting and support

**Developer Documentation:**
- Developer Tutorials - Project-based learning
- API Usage Guides - Integration tutorials
- CLI Documentation - Command reference

**Operational Documentation:**
- Runbooks - Incident response, deployment procedures
- Maintenance Tasks - Backup, scaling, monitoring
- On-Call Procedures - Alert handling, escalation

### 2. Code-to-Docs Reverse Engineering (Brownfield)
**Supported Frameworks:**
- **Backend**: Spring Boot ✅ (Complete), FastAPI ✅ (Complete), Express.js, Django, Flask
- **Infrastructure**: Pulumi ✅, Terraform, AWS CDK
- **Frontend**: React, Next.js, Vue.js
- **Data**: Python ETL, Apache Airflow
- **CLI**: Python CLI, Node CLI

(✅ = Fully mapped with `references/mappings/{framework}-mapping.yaml`)

### 3. Documentation Audit & Improvement
- Review existing docs against best practices
- Identify gaps and quality issues
- Suggest specific improvements

### 4. Format Conversion
- Markdown ↔ Word (DOCX) ↔ PDF
- Professional styling for enterprise use
- Integrates with `docx` and `pdf` skills

### 5. Diagram Generation
- **Mermaid**: C4 diagrams, flowcharts (via `mermaid-architect` skill)
- **PlantUML**: UML diagrams, ER diagrams (via `plantuml` skill)

---

## Decision Tree & Routing Logic

### Stage 1: Intent Classification

Parse user request and classify intent:

| Intent | Keywords | Workflow |
|--------|----------|----------|
| **CREATE_NEW** | "create", "generate", "write", "new" + document type | [greenfield-workflow.md](references/workflows/greenfield-workflow.md) |
| **CODE_TO_DOCS** | "document", "extract", "generate from code", path reference | [brownfield-workflow.md](references/workflows/brownfield-workflow.md) |
| **AUDIT** | "audit", "review", "check", "improve", "validate" | [audit-workflow.md](references/workflows/audit-workflow.md) |
| **CONVERT** | "convert", "transform", "generate PDF", "to Word" | [convert-workflow.md](references/workflows/convert-workflow.md) |
| **DIAGRAM** | "diagram", "C4", "sequence", "ER", "flowchart", "visualize" | [diagram-workflow.md](references/workflows/diagram-workflow.md) |
| **CREATE_USER_DOCS** | "user manual", "how-to", "getting started", "KB article" | [user-docs-workflow.md](references/workflows/user-docs-workflow.md) |
| **CREATE_TUTORIAL** | "tutorial", "API guide", "CLI docs", "developer guide" | [tutorial-workflow.md](references/workflows/tutorial-workflow.md) |
| **CREATE_RUNBOOK** | "runbook", "procedure", "incident", "deployment", "on-call" | [runbook-workflow.md](references/workflows/runbook-workflow.md) |

**IMPORTANT**: After classifying intent, immediately load ONLY the corresponding workflow guide. Do NOT load multiple workflows or all templates upfront.

### Stage 2: Document Type Identification (for CREATE_NEW, CREATE_USER_DOCS, CREATE_TUTORIAL, CREATE_RUNBOOK)

**Requirements & Design:**
| Keywords | Document Type | Template |
|----------|---------------|----------|
| "SRS", "requirements specification" | SRS | [requirements-srs.md](references/templates/markdown/requirements-srs.md) |
| "PRD", "product requirements" | PRD | [requirements-prd.md](references/templates/markdown/requirements-prd.md) |
| "SDD", "design document" | SDD | [design-sdd.md](references/templates/markdown/design-sdd.md) |
| "arc42", "architecture" | arc42 | [design-arc42.md](references/templates/markdown/design-arc42.md) |
| "OpenAPI", "API spec" | OpenAPI | [api-openapi.yaml](references/templates/markdown/api-openapi.yaml) |

**User Documentation:**
| Keywords | Document Type | Template |
|----------|---------------|----------|
| "user manual", "user guide" | User Manual | [user-manual.md](references/templates/markdown/user-manual.md) |
| "how-to", "step-by-step" | How-To Guide | [howto-guide.md](references/templates/markdown/howto-guide.md) |
| "getting started", "quick start" | Getting Started | [getting-started.md](references/templates/markdown/getting-started.md) |

**Developer Documentation:**
| Keywords | Document Type | Template |
|----------|---------------|----------|
| "tutorial", "walkthrough" | Developer Tutorial | [developer-tutorial.md](references/templates/markdown/developer-tutorial.md) |
| "API guide", "integration" | API Usage Guide | (use tutorial template) |
| "CLI docs", "command reference" | CLI Documentation | (use getting-started template) |

**Operational Documentation:**
| Keywords | Document Type | Template |
|----------|---------------|----------|
| "runbook", "procedure" | Runbook | [runbook.md](references/templates/markdown/runbook.md) |
| "incident response" | Incident Runbook | (use runbook template) |
| "deployment", "release" | Deployment Runbook | (use runbook template) |

### Stage 3: Framework Detection (for CODE_TO_DOCS)

| Framework | Detection Files | Detection Patterns | Mapping File | Status |
|-----------|----------------|-------------------|--------------|--------|
| **Spring Boot** | `pom.xml`, `build.gradle` | `@SpringBootApplication` | [spring-boot-mapping.yaml](references/mappings/backend/spring-boot-mapping.yaml) | ✅ Complete |
| **FastAPI** | `requirements.txt` | `from fastapi import` | [fastapi-mapping.yaml](references/mappings/backend/fastapi-mapping.yaml) | ✅ Complete |
| **Pulumi** | `Pulumi.yaml` | `import pulumi` | [pulumi-mapping.yaml](references/mappings/infrastructure/pulumi-mapping.yaml) | 📋 Planned |

**Detection Process:**
1. Use Glob to find detection files
2. Use Grep to confirm framework patterns
3. Load framework-specific mapping: `references/mappings/{category}/{framework}-mapping.yaml`

### Stage 4: Load Knowledge (On-Demand)

**CRITICAL**: Load ONLY what is needed for the current task. Use Progressive Disclosure.

**For CREATE_NEW (Greenfield):**
- Load: [greenfield-workflow.md](references/workflows/greenfield-workflow.md) (1,500 tokens)
- Load: [templates/markdown/{doc-type}.md](references/templates/markdown/) (500-800 tokens)
- Optional: [02-requirements-writing.md](references/reference/02-requirements-writing.md) OR [03-design-arc42.md](references/reference/03-design-arc42.md) (400 tokens)
- Total: ~2,400 tokens

**For CODE_TO_DOCS (Brownfield):**
- Load: [brownfield-workflow.md](references/workflows/brownfield-workflow.md) (1,500 tokens)
- Load: [mappings/{framework}-mapping.yaml](references/mappings/) (500 tokens)
- Optional: [09-code-to-docs-workflow.md](references/reference/09-code-to-docs-workflow.md) (385 tokens)
- Total: ~2,385 tokens

**For AUDIT:**
- Load: [audit-workflow.md](references/workflows/audit-workflow.md) (1,000 tokens)
- Optional: [10-quality-checklist.md](references/reference/10-quality-checklist.md) (250 tokens)
- Total: ~1,250 tokens

**For CONVERT:**
- Load: [convert-workflow.md](references/workflows/convert-workflow.md) (750 tokens)
- Total: ~750 tokens

**For DIAGRAM:**
- Load: [diagram-workflow.md](references/workflows/diagram-workflow.md) (1,000 tokens)
- Optional: [04-diagrams-selection.md](references/reference/04-diagrams-selection.md) (435 tokens)
- Total: ~1,435 tokens

### Stage 5: Execute

Follow the instructions in the loaded workflow guide. Each workflow guide contains:
- Step-by-step execution instructions
- Examples
- Quality checklists
- Best practices

**Do NOT attempt to execute without loading the workflow guide first.**

### Stage 6: Post-Processing

After generating documentation, offer user options:
- Format conversion (MD → DOCX → PDF)
- Diagram generation
- Additional related documentation
- Audit/review

---

## Command Patterns

### Creating Documentation

**Greenfield (Template-based):**
```
Create a Software Requirements Specification for [project description]
Create a PRD for [feature description]
Generate OpenAPI spec for [API description]
```

**Brownfield (Code-to-docs):**
```
Document my Spring Boot application at [path]
Generate API documentation from my FastAPI app at [path]
Extract deployment docs from my Pulumi infrastructure at [path]
```

### Auditing Documentation

```
Audit my SRS at [path]
Review my API documentation at [path] for OpenAPI compliance
Check my design document for completeness
```

### Converting Formats

```
Convert [file].md to Word format
Generate PDF from [file].md
Create a PDF documentation package from all docs
```

### Generating Diagrams

```
Create a C4 container diagram for [system description]
Generate an ER diagram from my JPA entities
Create a sequence diagram for [workflow description]
```

---

## Execution Instructions

### For CREATE_NEW (Greenfield)

1. **Load workflow**: Read [greenfield-workflow.md](references/workflows/greenfield-workflow.md)
2. **Follow workflow steps**:
   - Identify document type
   - Load appropriate template
   - Customize template with user's context
   - Generate content following template structure
   - Add visual elements (offer diagrams)
   - Apply professional formatting
   - Save and offer post-processing

3. **Token budget check**: ~4,000 tokens total (SKILL.md + workflow + template)

### For CODE_TO_DOCS (Brownfield)

1. **Load workflow**: Read [brownfield-workflow.md](references/workflows/brownfield-workflow.md)
2. **Follow workflow steps**:
   - Detect framework (Glob + Grep)
   - Load framework mapping
   - Execute 6-step code analysis:
     - Architecture extraction
     - API extraction
     - Data model extraction
     - Business logic extraction
     - Security extraction
     - Deployment extraction
   - Generate documentation artifacts (SDD, OpenAPI, diagrams)
   - Invoke diagram skills (mermaid-architect, plantuml)
   - Save and offer post-processing

3. **Token budget check**: ~5,000 tokens total (SKILL.md + workflow + mapping)

### For AUDIT

1. **Load workflow**: Read [audit-workflow.md](references/workflows/audit-workflow.md)
2. **Follow workflow steps**:
   - Identify document type
   - Run quality checklist
   - Identify gaps and issues
   - Generate audit report
   - Offer automatic fixes

3. **Token budget check**: ~4,000 tokens total

### For CONVERT

1. **Load workflow**: Read [convert-workflow.md](references/workflows/convert-workflow.md)
2. **Follow workflow steps**:
   - Identify source and target formats
   - Prepare source document
   - Invoke skill (docx or pdf)
   - Verify output quality
   - Offer additional conversions

3. **Token budget check**: ~3,500 tokens total

### For DIAGRAM

1. **Load workflow**: Read [diagram-workflow.md](references/workflows/diagram-workflow.md)
2. **Follow workflow steps**:
   - Identify diagram type
   - Gather diagram content
   - Invoke skill (mermaid-architect or plantuml)
   - Offer diagram rendering

3. **Token budget check**: ~4,200 tokens total

---

## Best Practices

### Documentation Philosophy
- **Docs-as-Code**: Update docs in same commit as code
- **Minimum Viable Documentation**: Small, fresh, accurate docs > large stale docs
- **Audience-Specific**: Stakeholders (Why/What), Developers (How), Users (How-To)

### Writing Style
- Clear, concise language
- Active voice
- Short paragraphs (3-5 sentences)
- Bullet points for lists
- Tables for structured data
- Code examples where appropriate

### Structure Guidelines
- Hierarchical headings (H1 → H2 → H3)
- Table of contents for docs > 3 pages
- Introduction explaining purpose and scope
- Glossary for technical terms
- Consistent formatting throughout

---

## Knowledge Base Organization

```
documentation-specialist/
├── SKILL.md                           # This file (core routing + quick start)
│
└── references/                        # On-demand resources (loaded selectively)
    │
    ├── workflows/                     # Workflow guides
    │   ├── greenfield-workflow.md     # CREATE_NEW
    │   ├── brownfield-workflow.md     # CODE_TO_DOCS
    │   ├── audit-workflow.md          # AUDIT
    │   ├── convert-workflow.md        # CONVERT
    │   └── diagram-workflow.md        # DIAGRAM
    │
    ├── templates/                     # Document templates
    │   └── markdown/
    │       ├── requirements-srs.md    # IEEE SRS
    │       ├── requirements-prd.md    # Agile PRD
    │       ├── api-openapi.yaml       # OpenAPI 3.0
    │       ├── design-sdd.md          # Software Design Doc
    │       └── design-arc42.md        # arc42 Architecture
    │
    ├── mappings/                      # Code-to-docs mappings
    │   ├── backend/
    │   │   ├── spring-boot-mapping.yaml   # ✅ Complete
    │   │   └── fastapi-mapping.yaml
    │   └── infrastructure/
    │       └── pulumi-mapping.yaml
    │
    ├── examples/                      # Few-shot learning examples
    │   ├── TOC.md                     # Navigation index
    │   ├── greenfield/                # Template-based examples
    │   └── brownfield/                # Code-to-docs examples
    │
    └── reference/                     # Reference guides
        ├── 01-philosophy.md           # Docs-as-code philosophy
        ├── 02-requirements.md         # Requirements writing
        ├── 03-design.md               # Design documentation
        ├── 04-diagrams.md             # Diagram selection
        ├── 05-api-docs.md             # API documentation
        └── 09-code-to-docs.md         # Reverse engineering
```

**Navigation Principle**: Load files from references/ only when explicitly required by the workflow.

---

## Integration with Other Skills

### docx Skill
**When**: User requests Word format or DOCX → MD conversion
**Invoke**: After generating markdown documentation
**Pass**: Source file path, styling requirements, output path

### pdf Skill
**When**: User requests PDF format or documentation package
**Invoke**: After generating markdown or DOCX documentation
**Pass**: Source file(s), formatting options, output path

### plantuml Skill
**When**: Generating UML diagrams (ER, sequence, component, state machine)
**Invoke**: During documentation generation or on-demand
**Pass**: Diagram type, content, output path

### mermaid-architect Skill
**When**: Generating C4 diagrams or flowcharts
**Invoke**: During documentation generation or on-demand
**Pass**: Diagram type (C4 context/container/component), system elements, output path

---

## Error Handling

**Cannot detect framework/technology:**
→ Ask user: "I couldn't detect your framework. Is this a Spring Boot, FastAPI, React, or other application?"

**Missing template:**
→ Use closest available template and inform user: "Using SDD template as closest match. Would you like to customize?"

**Skill integration failure (docx/pdf/plantuml/mermaid-architect not available):**
→ Inform user: "The [skill] skill is not installed. Would you like me to proceed with markdown only?"

**User request ambiguous:**
→ Ask clarifying questions: "I can create either an SRS (formal) or PRD (agile). Which would you prefer?"

**File not found:**
→ Inform user and suggest alternatives: "I couldn't find [file]. Did you mean [similar file]?"

---

## Token Budget Management

**Target per request**: <10,000 tokens total

**Breakdown**:
- SKILL.md: 2,500 tokens
- Single workflow: 750-1,500 tokens
- Template or mapping: 400-800 tokens
- Optional reference: 200-700 tokens

**Maximum load**: 2,500 + 1,500 + 800 + 700 = 5,500 tokens (well under 10K budget)

**Cost savings vs v1.0**: ~39% reduction in typical load (9,000 tokens → 5,500 tokens)

---

## On-Demand Resource Links

**Do NOT load these unless explicitly needed for the current task:**

### Workflow Guides (Load based on intent)
- [greenfield-workflow.md](references/workflows/greenfield-workflow.md) - Template-based creation
- [brownfield-workflow.md](references/workflows/brownfield-workflow.md) - Code-to-docs extraction
- [audit-workflow.md](references/workflows/audit-workflow.md) - Documentation review
- [convert-workflow.md](references/workflows/convert-workflow.md) - Format conversion
- [diagram-workflow.md](references/workflows/diagram-workflow.md) - Diagram generation
- [user-docs-workflow.md](references/workflows/user-docs-workflow.md) - User documentation
- [tutorial-workflow.md](references/workflows/tutorial-workflow.md) - Developer tutorials
- [runbook-workflow.md](references/workflows/runbook-workflow.md) - Operational runbooks

### Reference Guides (Load when deep dive needed)
- [01-philosophy.md](references/reference/01-philosophy.md) - Docs-as-code principles
- [02-requirements-writing.md](references/reference/02-requirements-writing.md) - Requirements writing best practices
- [03-design-arc42.md](references/reference/03-design-arc42.md) - Design documentation guidance
- [04-diagrams-selection.md](references/reference/04-diagrams-selection.md) - Diagram type selection
- [05-api-stripe-gold-standard.md](references/reference/05-api-stripe-gold-standard.md) - API documentation (Stripe analysis)
- [09-code-to-docs-workflow.md](references/reference/09-code-to-docs-workflow.md) - Reverse engineering methodology
- [10-quality-checklist.md](references/reference/10-quality-checklist.md) - Quality checklist

### Templates (Load based on document type)
- [requirements-srs.md](references/templates/markdown/requirements-srs.md) - IEEE SRS
- [requirements-prd.md](references/templates/markdown/requirements-prd.md) - Agile PRD
- [api-openapi.yaml](references/templates/markdown/api-openapi.yaml) - OpenAPI 3.0
- [user-manual.md](references/templates/markdown/user-manual.md) - User Manual
- [developer-tutorial.md](references/templates/markdown/developer-tutorial.md) - Developer Tutorial
- [getting-started.md](references/templates/markdown/getting-started.md) - Getting Started Guide
- [howto-guide.md](references/templates/markdown/howto-guide.md) - How-To Guide
- [runbook.md](references/templates/markdown/runbook.md) - Operational Runbook

### Examples (Few-Shot Learning - Load via TOC)
- **[TOC.md](references/examples/TOC.md)** - Navigation index to all examples (150 tokens)
  - [billing-srs.md](references/examples/greenfield/billing-srs.md) - Payment processing SRS (1,200 tokens)
  - [collaboration-prd.md](references/examples/greenfield/collaboration-prd.md) - Team collaboration PRD (1,000 tokens)
  - [adr-microservices.md](references/examples/greenfield/adr-microservices.md) - Microservices ADR (400 tokens)
  - [taskmanager-user-manual.md](references/examples/greenfield/taskmanager-user-manual.md) - User Manual example
  - [rest-api-tutorial.md](references/examples/greenfield/rest-api-tutorial.md) - REST API tutorial
  - [cli-getting-started.md](references/examples/greenfield/cli-getting-started.md) - CLI getting started
  - [database-failover-runbook.md](references/examples/brownfield/database-failover-runbook.md) - Database failover runbook

**IMPORTANT**: Load [TOC.md](references/examples/TOC.md) first, then load ONLY the relevant example via link, not all examples.

### Mappings (Load based on detected framework)
- [spring-boot-mapping.yaml](references/mappings/backend/spring-boot-mapping.yaml) - Spring Boot (complete)
- [fastapi-mapping.yaml](references/mappings/backend/fastapi-mapping.yaml) - FastAPI (complete)

---

## Quick Reference

| Task | Intent | Workflow | Typical Tokens |
|------|--------|----------|----------------|
| Create SRS | CREATE_NEW | greenfield-workflow.md | ~4,000 |
| Document Spring Boot app | CODE_TO_DOCS | brownfield-workflow.md | ~5,000 |
| Audit OpenAPI spec | AUDIT | audit-workflow.md | ~4,000 |
| Convert MD to DOCX | CONVERT | convert-workflow.md | ~3,500 |
| Generate C4 diagram | DIAGRAM | diagram-workflow.md | ~4,200 |

**Average token load**: 4,140 tokens (vs 9,000 in v1.0) = **54% reduction**

---

**End of Documentation Specialist Skill (PDA v2.1)**

**This skill uses Progressive Disclosure Architecture to minimize token consumption while maintaining full functionality. Workflow guides are loaded on-demand based on user intent.**
