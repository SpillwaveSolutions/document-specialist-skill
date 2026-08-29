# Brownfield Code-to-Docs Workflow

---
TOKEN_BUDGET: 400
TIER: 2
LOAD_TRIGGER: Intent = CODE_TO_DOCS
DEPENDENCIES: SKILL.md
---

## Overview

Reverse-engineer professional documentation from existing codebases.

**Supported Frameworks**:
- **Backend**: Spring Boot, FastAPI, Express.js, Django
- **Infrastructure**: Pulumi, Terraform
- **Frontend**: React, Next.js

## Workflow Steps

### Step 1: Framework Detection

Use Glob + Grep to identify framework:

| Framework | Detection Files | Confirm Pattern |
|-----------|----------------|-----------------|
| Spring Boot | `pom.xml`, `build.gradle` | `@SpringBootApplication` |
| FastAPI | `requirements.txt` | `from fastapi import` |
| Express.js | `package.json` | `const express =` |
| Pulumi | `Pulumi.yaml` | `import pulumi` |
| Terraform | `*.tf` | `resource "aws_` |
| React | `package.json` | `"react":` |

**If detected**: Load mapping from `mappings/{category}/{framework}-mapping.yaml`
**If not detected**: Request framework clarification from user

### Step 2: Load Framework Mapping

Read the framework-specific mapping file for extraction rules.

For detailed guidance, load:
- Spring Boot: [brownfield/springboot-guide.md](brownfield/springboot-guide.md)
- FastAPI: [brownfield/fastapi-guide.md](brownfield/fastapi-guide.md)
- Pulumi: [brownfield/pulumi-guide.md](brownfield/pulumi-guide.md)

### Step 3: 6-Step Code Analysis

| Step | What to Extract | How |
|------|-----------------|-----|
| 3.1 Architecture | Entry point, external systems, config | Read config files, main class |
| 3.2 API | Endpoints, methods, parameters | Grep for route decorators |
| 3.3 Data Model | Entities, relationships, constraints | Grep for entity annotations |
| 3.4 Business Logic | Services, workflows, transactions | Grep for service classes |
| 3.5 Security | Auth method, authorization rules | Read security config |
| 3.6 Deployment | Database, Docker, K8s config | Read deployment files |

### Step 4: Generate Documentation

**For Backend Apps**:
1. Software Design Document (SDD) - arc42. Save as `DESIGN_DOC.md`. Template: templates/markdown/DESIGN_DOC.md. Few-shot: examples/brownfield/spring-boot-sdd.md.
2. OpenAPI 3.0 Specification
3. Diagrams: C4 Container, Component, ER, Sequence (Mermaid)
4. PlantUML Salt wireframe for every user-facing screen

**For Infrastructure**:
1. Deployment Architecture Document (`docs/architecture.md` or `DESIGN_DOC.md`)
2. Diagrams: C4 Infrastructure, Deployment Topology

**Save to**: `DESIGN_DOC.md`, `docs/api/`, `docs/diagrams/`

If the user asked only for an SDD, load [design-workflow.md](design-workflow.md) after extraction.

### Step 5: Invoke Diagram Skills

Invoke appropriate diagram skills:
- **design-doc-mermaid**: C4, flowchart, sequence, class, ER, state, component views
- **plantuml**: Salt wireframes, use case, timing, ArchiMate. Always PNG or SVG.

### Step 6: Format & Save

Verify documents include:
- Front matter (title, version, date, generator)
- Table of contents
- Code references with file paths
- Glossary of framework terms

### Step 7: Post-Processing

Present options to user:
1. Convert SDD to Word (DOCX)
2. Generate PDF package
3. Render diagrams to PNG
4. Create sequence diagrams for specific flows

## Quality Checklist

- [ ] Framework detected and confirmed
- [ ] Mapping file loaded
- [ ] All 6 extraction steps completed
- [ ] SDD generated as DESIGN_DOC.md (arc42 format)
- [ ] Salt wireframes for user-facing screens
- [ ] OpenAPI generated (backend only)
- [ ] Diagrams generated
- [ ] Code references include file paths
- [ ] Glossary includes framework terms

## Example Snippet

```markdown
### 3.2 API Extraction (Spring Boot)

Grep: "@RestController" → Found OrderController.java

Endpoints extracted:
- GET /api/v1/orders → List orders
- POST /api/v1/orders → Create order
- GET /api/v1/orders/{id} → Get order by ID
```

For complete examples: [examples/brownfield/](../examples/brownfield/)

---

**Framework-specific guides**: See `brownfield/` subdirectory
