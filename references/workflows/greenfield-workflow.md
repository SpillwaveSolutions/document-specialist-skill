# Greenfield Documentation Workflow

---
TOKEN_BUDGET: 350
TIER: 2
LOAD_TRIGGER: Intent = CREATE_NEW
DEPENDENCIES: SKILL.md
---

## Overview

Create professional documentation from templates for new projects.

**Supported**: SRS, PRD, OpenAPI, User Manuals, How-To Guides, Getting Started, Tutorials, Runbooks

## Workflow Steps

### Step 1: Identify Document Type

| Request Contains | Document Type | Template |
|------------------|---------------|----------|
| "SRS", "requirements specification" | SRS | templates/markdown/requirements-srs.md |
| "PRD", "product requirements" | PRD | templates/markdown/requirements-prd.md |
| "OpenAPI", "API spec" | OpenAPI | templates/markdown/api-openapi.yaml |
| "user manual", "user guide" | User Manual | templates/markdown/user-manual.md |
| "how-to", "step-by-step" | How-To | templates/markdown/howto-guide.md |
| "getting started", "quick start" | Getting Started | templates/markdown/getting-started.md |
| "tutorial" | Tutorial | templates/markdown/developer-tutorial.md |
| "runbook", "procedure" | Runbook | templates/markdown/runbook.md |

### Step 2: Load Template

Read the appropriate template file. For detailed guidance on specific document types, load:
- SRS: [greenfield/srs-guide.md](greenfield/srs-guide.md)
- PRD: [greenfield/prd-guide.md](greenfield/prd-guide.md)
- OpenAPI: [greenfield/openapi-guide.md](greenfield/openapi-guide.md)

### Step 3: Extract Context

From the user request, extract:
1. **Project/Feature Name** - Subject of documentation
2. **Domain** - Healthcare, finance, e-commerce, etc.
3. **Key Requirements** - Explicitly mentioned requirements
4. **Constraints** - Compliance (HIPAA, PCI-DSS), performance, security
5. **Audience** - Developers, users, executives, auditors

### Step 4: Generate Content

1. Replace all `[Placeholder]` markers with actual content
2. Use **Given-When-Then** format for acceptance criteria
3. Add domain-specific examples
4. Include compliance requirements if mentioned
5. Assign unique IDs (FR-XXX-001, NFR-XXX-001)

### Step 5: Add Visuals

Present diagram generation options:
- C4, flowchart, sequence, class, ER, state → invoke `design-doc-mermaid` skill
- Wireframes, use case, timing, ArchiMate → invoke `plantuml` skill (always PNG or SVG)

### Step 6: Format & Save

Verify document includes:
- Front matter (title, version, date, author, status)
- Table of contents (if > 3 pages)
- Glossary for technical terms
- Consistent heading hierarchy

Save to: `docs/{category}/{project}-{doc-type}.md`

### Step 7: Post-Processing

Present options to user:
1. Convert to Word (DOCX)
2. Generate PDF
3. Create diagrams
4. Generate related documentation

## Quality Checklist

- [ ] Front matter complete
- [ ] Clear purpose in introduction
- [ ] Audience defined
- [ ] Requirements have unique IDs
- [ ] Acceptance criteria in Given-When-Then
- [ ] Glossary included
- [ ] Visuals offered

## Example Snippet

```markdown
## 3.1 User Authentication

**FR-AUTH-001**: User Login

**Description**: The system shall authenticate users with email/password.

**Acceptance Criteria**:
- **Given** a registered user with verified email
- **When** they enter correct credentials
- **Then** the system grants access with JWT token (1-hour expiry)

**Priority**: Must Have
```

For complete examples, see [examples/TOC.md](../examples/TOC.md).

---

**For advanced topics** (multi-project, documentation packages): [greenfield/advanced.md](greenfield/advanced.md)
