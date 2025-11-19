# Documentation Specialist Skill

---
name: "documentation-specialist"
description: "Creates professional software documentation from templates (greenfield) or reverse-engineers from code (brownfield) using Progressive Disclosure Architecture"
version: "2.1.0-PDA"
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Bash", "Skill"]
---

## Quick Start

Transform Claude Code into an expert software documentation specialist using Progressive Disclosure Architecture for efficient token management.

**Primary Capabilities:**

1. **Greenfield**: Create documentation from templates (SRS, PRD, SDD, arc42, OpenAPI)
2. **Brownfield**: Reverse-engineer documentation from code (Spring Boot, Pulumi, FastAPI, etc.)
3. **Audit**: Review and improve existing documentation
4. **Convert**: Transform between formats (MD, DOCX, PDF)
5. **Diagram**: Generate visual documentation (Mermaid, PlantUML)

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
- Software Requirements Specification (SRS) - IEEE-compliant
- Product Requirements Document (PRD) - Agile-friendly
- Software Design Document (SDD) - arc42-based
- OpenAPI 3.0 API Specification
- User Guides and KB Articles
- Deployment Documentation

### 2. Code-to-Docs Reverse Engineering (Brownfield)
**Supported Frameworks:**
- **Backend**: Spring Boot ✅, FastAPI, Express.js, Django, Flask
- **Infrastructure**: Pulumi ✅, Terraform, AWS CDK
- **Frontend**: React, Next.js, Vue.js
- **Data**: Python ETL, Apache Airflow
- **CLI**: Python CLI, Node CLI

(✅ = Fully mapped with `mappings/{framework}-mapping.yaml`)

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
| **CREATE_NEW** | "create", "generate", "write", "new" + document type | `workflows/greenfield-workflow.md` |
| **CODE_TO_DOCS** | "document", "extract", "generate from code", path reference | `workflows/brownfield-workflow.md` |
| **AUDIT** | "audit", "review", "check", "improve", "validate" | `workflows/audit-workflow.md` |
| **CONVERT** | "convert", "transform", "generate PDF", "to Word" | `workflows/convert-workflow.md` |
| **DIAGRAM** | "diagram", "C4", "sequence", "ER", "flowchart", "visualize" | `workflows/diagram-workflow.md` |

**IMPORTANT**: After classifying intent, immediately load ONLY the corresponding workflow guide. Do NOT load multiple workflows or all templates upfront.

### Stage 2: Document Type Identification (for CREATE_NEW)

| Keywords | Document Type | Template |
|----------|---------------|----------|
| "SRS", "requirements specification", "formal requirements" | SRS | `templates/markdown/requirements-srs.md` |
| "PRD", "product requirements", "feature" | PRD | `templates/markdown/requirements-prd.md` |
| "SDD", "design document" | SDD | `templates/markdown/design-sdd.md` |
| "arc42", "architecture" | arc42 | `templates/markdown/design-arc42.md` |
| "OpenAPI", "API spec", "REST API" | OpenAPI | `templates/markdown/api-openapi.yaml` |

### Stage 3: Framework Detection (for CODE_TO_DOCS)

| Framework | Detection Files | Detection Patterns | Mapping File |
|-----------|----------------|-------------------|--------------|
| **Spring Boot** | `pom.xml`, `build.gradle` | `@SpringBootApplication` | `mappings/backend/spring-boot-mapping.yaml` |
| **FastAPI** | `requirements.txt` | `from fastapi import` | `mappings/backend/fastapi-mapping.yaml` |
| **Pulumi** | `Pulumi.yaml` | `import pulumi` | `mappings/infrastructure/pulumi-mapping.yaml` |

**Detection Process:**
1. Use Glob to find detection files
2. Use Grep to confirm framework patterns
3. Load framework-specific mapping: `mappings/{category}/{framework}-mapping.yaml`

### Stage 4: Load Knowledge (On-Demand)

**CRITICAL**: Load ONLY what is needed for the current task. Use Progressive Disclosure.

**For CREATE_NEW (Greenfield):**
```
Load: workflows/greenfield-workflow.md (1,500 tokens)
Load: templates/markdown/{doc-type}.md (500-800 tokens)
Optional: reference/02-requirements.md OR reference/03-design.md (400 tokens)
Total: ~2,400 tokens
```

**For CODE_TO_DOCS (Brownfield):**
```
Load: workflows/brownfield-workflow.md (1,500 tokens)
Load: mappings/{framework}-mapping.yaml (500 tokens)
Optional: reference/09-code-to-docs.md (385 tokens)
Total: ~2,385 tokens
```

**For AUDIT:**
```
Load: workflows/audit-workflow.md (1,000 tokens)
Optional: reference/quality-checklist.md (250 tokens)
Total: ~1,250 tokens
```

**For CONVERT:**
```
Load: workflows/convert-workflow.md (750 tokens)
Total: ~750 tokens
```

**For DIAGRAM:**
```
Load: workflows/diagram-workflow.md (1,000 tokens)
Optional: reference/04-diagrams.md (435 tokens)
Total: ~1,435 tokens
```

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

1. **Load workflow**: Read `workflows/greenfield-workflow.md`
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

1. **Load workflow**: Read `workflows/brownfield-workflow.md`
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

1. **Load workflow**: Read `workflows/audit-workflow.md`
2. **Follow workflow steps**:
   - Identify document type
   - Run quality checklist
   - Identify gaps and issues
   - Generate audit report
   - Offer automatic fixes

3. **Token budget check**: ~4,000 tokens total

### For CONVERT

1. **Load workflow**: Read `workflows/convert-workflow.md`
2. **Follow workflow steps**:
   - Identify source and target formats
   - Prepare source document
   - Invoke skill (docx or pdf)
   - Verify output quality
   - Offer additional conversions

3. **Token budget check**: ~3,500 tokens total

### For DIAGRAM

1. **Load workflow**: Read `workflows/diagram-workflow.md`
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
├── workflows/                         # On-demand workflows
│   ├── greenfield-workflow.md         # CREATE_NEW
│   ├── brownfield-workflow.md         # CODE_TO_DOCS
│   ├── audit-workflow.md              # AUDIT
│   ├── convert-workflow.md            # CONVERT
│   └── diagram-workflow.md            # DIAGRAM
│
├── templates/                         # Document templates
│   └── markdown/
│       ├── requirements-srs.md        # IEEE SRS
│       ├── requirements-prd.md        # Agile PRD
│       ├── api-openapi.yaml           # OpenAPI 3.0
│       ├── design-sdd.md              # Software Design Doc
│       └── design-arc42.md            # arc42 Architecture
│
├── mappings/                          # Code-to-docs mappings
│   ├── backend/
│   │   ├── spring-boot-mapping.yaml   # ✅ Complete
│   │   └── fastapi-mapping.yaml
│   └── infrastructure/
│       └── pulumi-mapping.yaml
│
└── reference/                         # Reference guides
    ├── 01-philosophy.md               # Docs-as-code philosophy
    ├── 02-requirements.md             # Requirements writing
    ├── 03-design.md                   # Design documentation
    ├── 04-diagrams.md                 # Diagram selection
    ├── 05-api-docs.md                 # API documentation
    ├── 09-code-to-docs.md             # Reverse engineering
    └── comprehensive-guide.md.backup  # Original (archived)
```

**Navigation Principle**: Load files from on-demand resources only when explicitly required by the workflow.

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
- `workflows/greenfield-workflow.md` - Template-based creation
- `workflows/brownfield-workflow.md` - Code-to-docs extraction
- `workflows/audit-workflow.md` - Documentation review
- `workflows/convert-workflow.md` - Format conversion
- `workflows/diagram-workflow.md` - Diagram generation

### Reference Guides (Load when deep dive needed)
- `reference/01-philosophy.md` - Docs-as-code principles
- `reference/02-requirements.md` - Requirements writing best practices
- `reference/03-design.md` - Design documentation guidance
- `reference/04-diagrams.md` - Diagram type selection
- `reference/05-api-docs.md` - API documentation (Stripe analysis)
- `reference/09-code-to-docs.md` - Reverse engineering methodology
- `reference/comprehensive-guide.md.backup` - Original complete guide (archived)

### Templates (Load based on document type)
- `templates/markdown/requirements-srs.md` - IEEE SRS
- `templates/markdown/requirements-prd.md` - Agile PRD
- `templates/markdown/api-openapi.yaml` - OpenAPI 3.0
- `templates/markdown/design-sdd.md` - Software Design Doc
- `templates/markdown/design-arc42.md` - arc42 Architecture

### Examples (Few-Shot Learning - Load via TOC)
- **`examples/TOC.md`** - Navigation index to all examples (150 tokens)
  - `examples/greenfield/billing-srs.md` - Payment processing SRS (1,200 tokens)
  - `examples/greenfield/collaboration-prd.md` - Team collaboration PRD (1,000 tokens)
  - `examples/greenfield/task-api-openapi.yaml` - Task management API (1,500 tokens)
  - `examples/greenfield/adr-microservices.md` - Microservices ADR (400 tokens)

**IMPORTANT**: Load examples/TOC.md first, then load ONLY the relevant example via link, not all examples.

### Mappings (Load based on detected framework)
- `mappings/backend/spring-boot-mapping.yaml` - Spring Boot (complete)
- `mappings/backend/fastapi-mapping.yaml` - FastAPI (planned)
- `mappings/infrastructure/pulumi-mapping.yaml` - Pulumi (planned)

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
