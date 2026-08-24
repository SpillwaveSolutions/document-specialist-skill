# Documentation Specialist Skill - User Guide

**Version**: 2.0.0-PDA
**Audience**: Developers, Technical Writers, Product Managers
**Last Updated**: 2025-01-13

---

## Table of Contents

1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Feature 1: Greenfield Documentation (Create from Templates)](#feature-1-greenfield-documentation)
4. [Feature 2: Brownfield Documentation (Code-to-Docs)](#feature-2-brownfield-documentation)
5. [Feature 3: Documentation Audit](#feature-3-documentation-audit)
6. [Feature 4: Format Conversion](#feature-4-format-conversion)
7. [Feature 5: Diagram Generation](#feature-5-diagram-generation)
8. [Advanced Usage](#advanced-usage)
9. [Troubleshooting](#troubleshooting)
10. [Best Practices](#best-practices)

---

## Introduction

The **Documentation Specialist** skill transforms Claude Code into an expert software documentation specialist. It supports two primary workflows:

- **Greenfield**: Create professional documentation from templates
- **Brownfield**: Reverse-engineer documentation from existing code

### What You Can Do

✅ Create IEEE-compliant Software Requirements Specifications (SRS)
✅ Generate modern Product Requirements Documents (PRD)
✅ Extract OpenAPI specs from Spring Boot/FastAPI code
✅ Generate architecture diagrams (C4, UML)
✅ Audit existing documentation for quality
✅ Convert between formats (Markdown, DOCX, PDF)

### Prerequisites

**Required**:
- Claude Code (latest version)
- This skill installed at `~/.claude/skills/documentation-specialist/`

**Optional** (for full functionality):
- `docx` skill (for Word document conversion)
- `pdf` skill (for PDF generation)
- `design-doc-mermaid` skill (default diagrams: C4, sequence, class, ER, state)
- `plantuml` skill (wireframes and leftover UML; always PNG or SVG)

**Install optional skills**:
```
/skill docx
/skill pdf
/skill design-doc-mermaid
/skill plantuml
```

---

## Getting Started

### Basic Workflow

1. **Describe what you need** in natural language
2. **The skill classifies your intent** (create, document code, audit, convert, diagram)
3. **Workflow guide loads** automatically based on intent
4. **Documentation generates** following best practices
5. **Post-processing options** offered (convert format, add diagrams)

### First Example: Create an SRS

**Command**:
```
Create a Software Requirements Specification for a library management system
```

**What happens**:
1. Skill classifies intent as `CREATE_NEW` (SRS)
2. Loads `workflows/greenfield-workflow.md`
3. Loads `templates/markdown/requirements-srs.md`
4. Generates customized SRS with library domain context
5. Saves to `docs/requirements/library-management-srs.md`

**Output**: IEEE-compliant SRS (~12-20 pages) with:
- Introduction (purpose, scope, audience)
- Overall description (system context, constraints)
- Functional requirements (FR-XXX-001 format)
- Non-functional requirements (performance, security, usability)
- Acceptance criteria (Given-When-Then format)
- Requirements traceability matrix

---

## Feature 1: Greenfield Documentation

**Use when**: Starting a new project or feature, need documentation from scratch.

### Supported Document Types

#### 1.1 Software Requirements Specification (SRS)

**Trigger keywords**: "SRS", "requirements specification", "formal requirements"

**Standard**: IEEE 830-1998

**Command examples**:
```
Create an SRS for a healthcare patient portal with HIPAA compliance
Generate a Software Requirements Specification for an e-commerce checkout flow
Write requirements documentation for a real-time chat application
```

**Generated structure**:
1. Introduction
2. Overall Description
3. System Features (with FR-XXX-001 IDs)
4. Non-Functional Requirements (NFR-XXX-001 IDs)
5. External Interface Requirements
6. Appendix (Glossary, Traceability Matrix)

**Acceptance criteria format**:
```markdown
**Given** a user has a valid account
**When** they enter correct credentials
**Then** the system shall grant access
**And** redirect to the dashboard within 2 seconds
```

**Output location**: `docs/requirements/{project}-srs.md`

**Token cost**: ~4,000 tokens (Tier 1 + Tier 2 + greenfield workflow + SRS template)

---

#### 1.2 Product Requirements Document (PRD)

**Trigger keywords**: "PRD", "product requirements", "feature", "agile"

**Standard**: Modern agile format (not IEEE)

**Command examples**:
```
Create a PRD for a task assignment feature with notifications
Generate a Product Requirements Document for user profile customization
Write a PRD for implementing SSO authentication
```

**Generated structure**:
1. Objective (Problem, Solution, Why Now)
2. Success Metrics (Primary, Secondary, Counter-metrics)
3. User Personas & Use Cases
4. User Stories & Acceptance Criteria
5. Out of Scope
6. Technical Considerations
7. Timeline & Milestones
8. Risks & Mitigations

**User story format**:
```markdown
**As a** project manager
**I want to** assign tasks to team members with due dates
**so that** I can track project progress and accountability

**Priority**: Must Have (MoSCoW)
```

**Output location**: `docs/requirements/{feature}-prd.md`

**Token cost**: ~4,000 tokens

---

#### 1.3 OpenAPI 3.0 Specification

**Trigger keywords**: "OpenAPI", "API spec", "REST API documentation"

**Standard**: OpenAPI 3.0.3

**Command examples**:
```
Create OpenAPI documentation for a REST API with authentication
Generate an API spec for a product catalog with search and filtering
Write OpenAPI documentation for a task management API
```

**Generated structure**:
```yaml
openapi: 3.0.3
info:
  title: [API Name]
  version: 1.0.0
servers:
  - url: https://api.example.com/v1
components:
  securitySchemes:
    BearerAuth: ...
  schemas:
    User: ...
    Task: ...
  responses:
    UnauthorizedError: ...
paths:
  /api/v1/tasks:
    get: ...
    post: ...
  /api/v1/tasks/{taskId}:
    get: ...
    put: ...
    delete: ...
```

**Output location**: `docs/api/{project}-openapi.yaml`

**Token cost**: ~4,000 tokens

---

#### 1.4 Software Design Document (SDD)

**Trigger keywords**: "SDD", "design document", "technical design"

**Standard**: arc42 architecture template

**Command examples**:
```
Create a Software Design Document for a microservices architecture
Generate design documentation for a data processing pipeline
Write an SDD for a mobile app backend
```

**Generated structure** (arc42 sections):
1. Introduction and Goals
2. Constraints
3. System Context
4. Solution Strategy
5. Building Block View (Components)
6. Data Design
7. Deployment View
8. Crosscutting Concepts (Security, Logging, Error Handling)

**Output location**: `docs/design/{project}-sdd.md`

**Token cost**: ~4,000 tokens

---

### Customization Tips

**Provide specific context** for better results:

❌ **Generic** (avoid):
```
Create an SRS for an application
```

✅ **Specific** (better):
```
Create an SRS for a HIPAA-compliant telemedicine application with:
- Video consultations (WebRTC)
- Prescription management (e-prescription integration)
- EHR integration (HL7 FHIR)
- Patient scheduling (Google Calendar sync)
- Must support 10,000 concurrent users
- 99.99% uptime SLA
- SOC 2 Type II compliance required
```

**Result**: Highly customized SRS with healthcare-specific requirements, security considerations, and compliance sections.

---

## Feature 2: Brownfield Documentation

**Use when**: You have existing code with little or no documentation.

### Supported Frameworks

#### 2.1 Spring Boot (Backend) ✅ Fully Supported

**Detection**: Automatic via `pom.xml`, `build.gradle`, or `@SpringBootApplication` annotation

**Command examples**:
```
Document my Spring Boot application at ~/projects/customer-api
Generate documentation for the Spring Boot service at ~/services/order-service
Extract API docs from my Spring Boot app
```

**What happens**:
1. **Framework Detection**:
   ```
   Glob: pom.xml → Found
   Grep: "@SpringBootApplication" → Found
   Framework: Spring Boot 3.x detected
   ```

2. **Code Analysis** (6 steps):
   - **Architecture**: Scans `application.yml` for database, ports, external APIs
   - **API**: Extracts all `@RestController` classes → OpenAPI paths
   - **Data Model**: Extracts all `@Entity` classes → ER diagram
   - **Business Logic**: Scans `@Service` classes → SDD components
   - **Security**: Reads `SecurityConfig` → authentication/authorization docs
   - **Deployment**: Reads config files, Dockerfile → deployment section

3. **Generated Documentation**:
   - **SDD** (`docs/design/{project}-sdd.md`):
     - Section 3: System Context (external systems from config)
     - Section 5: Building Block View (Controllers, Services, Repositories)
     - Section 6: Data Design (Entities with relationships)
     - Section 7: Deployment (ports, database, external APIs)
     - Section 8: Security (JWT, roles, permissions)

   - **OpenAPI Spec** (`docs/api/{project}-openapi.yaml`):
     - Paths extracted from `@RestController` methods
     - Schemas from DTOs
     - Security schemes from `SecurityConfig`

   - **Diagrams** (`docs/diagrams/`):
     - C4 Container diagram (Mermaid)
     - Component diagram (PlantUML)
     - ER diagram from `@Entity` classes (PlantUML)
     - Sequence diagrams for key flows (PlantUML)

**Example output** (for e-commerce API):
```
docs/
├── design/
│   └── ecommerce-api-sdd.md          (25 pages, arc42 format)
├── api/
│   └── ecommerce-openapi.yaml        (800 lines, 40 endpoints)
└── diagrams/
    ├── c4-container.md                (Mermaid C4)
    ├── component-diagram.puml         (PlantUML)
    ├── er-diagram.puml                (12 tables)
    └── sequence-create-order.puml     (Order creation flow)
```

**Token cost**: ~5,000 tokens (Tier 1 + Tier 2 + brownfield workflow + Spring Boot mapping)

---

#### 2.2 Pulumi (Infrastructure) ✅ Fully Supported

**Detection**: Automatic via `Pulumi.yaml` and `import pulumi` in `__main__.py`

**Command examples**:
```
Generate deployment documentation from my Pulumi infrastructure at ~/infra
Document my Pulumi AWS setup at ~/projects/aws-infra
Extract infrastructure docs from Pulumi code
```

**What happens**:
1. **Framework Detection**:
   ```
   Glob: Pulumi.yaml → Found
   Grep: "import pulumi" → Found in __main__.py
   Framework: Pulumi (Python, AWS provider)
   ```

2. **Code Analysis**:
   - Reads `__main__.py`
   - Extracts all `pulumi.aws.*` resources:
     - VPC, subnets, NAT Gateway, Internet Gateway
     - ECS clusters, services, task definitions
     - RDS instances, S3 buckets
     - CloudFront distributions
     - Security groups, IAM roles

3. **Generated Documentation**:
   - **Deployment Architecture Doc** (`docs/deployment/{project}-infrastructure.md`):
     - Network Architecture (VPC, subnets, CIDR blocks)
     - Compute Resources (ECS, Fargate, EC2)
     - Data Layer (RDS, S3, caching)
     - CDN (CloudFront)
     - Security (SGs, IAM)

   - **Diagrams** (`docs/diagrams/`):
     - C4 Level 2 infrastructure diagram (Mermaid)
     - Deployment topology diagram (PlantUML)

**Token cost**: ~5,000 tokens

---

#### 2.3 FastAPI, React, Terraform (Planned)

**Status**: Mapping files not yet created, but generic documentation still possible.

**Command examples**:
```
Document this as a FastAPI application at ~/projects/data-api
Document this as a React application at ~/projects/web-app
Document this as Terraform infrastructure at ~/infra/terraform
```

**Fallback behavior**:
- Skill will use generic code analysis
- Ask user for additional context
- Generate documentation using best practices
- Still produces SDD, README, and basic diagrams

**To add full support**:
1. Create `mappings/{category}/{framework}-mapping.yaml`
2. Define detection patterns and extraction rules
3. See `mappings/backend/spring-boot-mapping.yaml` for reference

---

### Brownfield Workflow Details

**6-Step Code Analysis Process**:

1. **Architecture Extraction** (~30 seconds)
   - Configuration files (`application.yml`, `Pulumi.yaml`)
   - Entry points (`@SpringBootApplication`, `main.py`)
   - External dependencies (database URLs, APIs)

2. **API Extraction** (~60 seconds)
   - REST endpoints (`@RestController`, `@app.get`)
   - HTTP methods, paths, parameters
   - Request/response schemas

3. **Data Model Extraction** (~45 seconds)
   - Entities (`@Entity`, Pydantic models)
   - Relationships (One-to-Many, Many-to-Many)
   - Constraints (nullable, unique)

4. **Business Logic Extraction** (~30 seconds)
   - Services (`@Service`, service functions)
   - Key workflows (method signatures)
   - Transaction boundaries

5. **Security Extraction** (~30 seconds)
   - Authentication (`SecurityConfig`, OAuth2)
   - Authorization (roles, permissions)
   - CORS, CSRF settings

6. **Deployment Extraction** (~30 seconds)
   - Ports, environment variables
   - Docker configuration
   - Database connections
   - Infrastructure resources

**Total time**: ~3-5 minutes for typical application

---

## Feature 3: Documentation Audit

**Use when**: You have existing documentation that needs quality review.

### Supported Document Types

- Software Requirements Specification (SRS)
- Product Requirements Document (PRD)
- Software Design Document (SDD)
- OpenAPI specifications
- User documentation

### Command Examples

```
Audit my OpenAPI specification at docs/api/customer-api.yaml
Review my SRS at docs/requirements/billing-srs.md
Check my design document for completeness
Audit my PRD for best practices
```

### What Happens

1. **Document Type Identification**:
   - Reads the file
   - Classifies type (SRS, PRD, OpenAPI, etc.)

2. **Quality Checklist Execution**:
   - **All Documents**:
     - ✅ Clear title
     - ✅ Version and date
     - ✅ Author identified
     - ✅ Table of contents (if > 3 pages)
     - ✅ Introduction
     - ✅ Glossary
     - ✅ Consistent formatting

   - **Requirements Documents**:
     - ✅ Unique requirement IDs
     - ✅ Testable requirements
     - ✅ Acceptance criteria
     - ✅ Non-functional requirements
     - ✅ Priorities (MoSCoW)
     - ✅ Traceability matrix

   - **API Documentation**:
     - ✅ Base URL and versioning
     - ✅ Authentication method
     - ✅ All endpoints documented
     - ✅ Request/response schemas
     - ✅ Error responses
     - ✅ Rate limiting
     - ✅ Code examples

3. **Gap Analysis**:
   - Missing sections
   - Incomplete content
   - Outdated information
   - Formatting inconsistencies

4. **Audit Report Generation**:
   ```markdown
   # Documentation Audit Report

   **Document**: docs/api/customer-api.yaml
   **Type**: OpenAPI 3.0.3
   **Audit Date**: 2025-01-13
   **Overall Quality**: Good (75%)
   **Recommendation**: Minor Revisions

   ## Critical Issues (Must Fix)
   1. Missing securitySchemes definition

   ## High Priority Issues (Should Fix)
   2. Incomplete error response coverage (missing 401, 403, 404)
   3. No rate limiting documentation

   ## Medium Priority Issues (Could Fix)
   4. Inconsistent schema usage (mix of $ref and inline)

   ## Improvement Recommendations
   - Add JWT Bearer authentication to components.securitySchemes
   - Document all HTTP error codes (400, 401, 403, 404, 500)
   - Standardize schema references
   ```

5. **Offer Automatic Fixes**:
   ```
   Would you like me to:
   1. Add missing securitySchemes section?
   2. Generate comprehensive error response definitions?
   3. Standardize all schemas to use $ref?
   ```

**Token cost**: ~4,000 tokens (Tier 1 + Tier 2 + audit workflow + quality checklist)

---

## Feature 4: Format Conversion

**Use when**: You need to convert documentation between formats.

### Supported Conversions

| Source | Target | Skill Used | Use Case |
|--------|--------|------------|----------|
| Markdown | DOCX | docx | Stakeholder reviews, formal delivery |
| Markdown | PDF | pdf | Distribution, archival |
| DOCX | Markdown | docx | Import into docs-as-code workflow |
| Multiple MD | PDF Package | pdf | Complete documentation release |

### Command Examples

#### Markdown → Word (DOCX)

```
Convert docs/requirements/billing-srs.md to Word format
Generate DOCX from my SRS markdown file
Transform my design document to Word with professional styling
```

**What happens**:
1. Skill classifies intent as `CONVERT` (MD → DOCX)
2. Loads `workflows/convert-workflow.md`
3. Validates markdown source
4. Invokes `docx` skill with styling requirements:
   - Cover page with metadata
   - Table of contents (auto-generated)
   - Heading styles (H1: 18pt Arial Bold Blue, H2: 16pt Arial Bold)
   - Body text: 12pt Times New Roman
   - Code blocks: 10pt Courier New, gray background
   - Professional table formatting
   - Page numbers (footer, centered)

**Output**: `docs/requirements/billing-srs.docx`

**Token cost**: ~3,500 tokens

---

#### Markdown → PDF

```
Convert docs/design/architecture.md to PDF
Generate PDF from my requirements document
Create a PDF version of my API documentation
```

**What happens**:
1. Invokes `pdf` skill with formatting options:
   - Page size: Letter (8.5" x 11")
   - Margins: 1" all sides
   - Header: Document title
   - Footer: Page numbers
   - Syntax highlighting for code blocks

**Output**: `docs/design/architecture.pdf`

**Token cost**: ~3,500 tokens

---

#### Multiple Documents → PDF Package

```
Create a PDF documentation package from all markdown files
Generate PDF package from docs/ directory
Combine all documentation into a single PDF
```

**What happens**:
1. Scans for all `docs/**/*.md` files
2. Organizes by category (requirements, design, api, user)
3. Invokes `pdf` skill to create combined PDF:
   - Cover page (project name, version, date)
   - Table of contents with page numbers
   - Bookmarks for navigation
   - All documents in sequence
   - Continuous page numbering

**Output**: `docs/pdf/{project}-documentation-v{version}.pdf`

**Token cost**: ~3,500 tokens

---

## Feature 5: Diagram Generation

**Use when**: You need visual documentation (architecture diagrams, UML, flowcharts).

### Diagram Types

#### 5.1 Default diagrams (Mermaid)

**Tool**: `design-doc-mermaid` skill (auto-invoked)

**Diagram types**:
1. **C4 Context**: System boundaries, external dependencies
2. **C4 Container**: Applications, databases, microservices
3. **C4 Component**: Internal structure of a single container
4. **Sequence**: Time-ordered interactions, API flows
5. **ER**: Database schema, table relationships
6. **Class**: Object-oriented structure
7. **State**: Entity lifecycle with states
8. **Flowchart**: Process, activity, component boxes

**Command examples**:

**C4 Context**:
```
Create a C4 context diagram for my e-commerce platform
Show system boundaries and external dependencies
Generate a high-level architecture diagram
```

**C4 Container**:
```
Create a C4 container diagram for my microservices architecture
Show all services, databases, and message queues
Generate a container-level diagram for deployment planning
```

**C4 Component**:
```
Create a C4 component diagram for the Order Service
Show internal modules and dependencies
Generate a component view of the API layer
```

**Output**: `docs/diagrams/c4-{type}.md` (Mermaid format)

**Token cost**: ~4,200 tokens

---

#### 5.2 Leftover UML and wireframes (PlantUML)

**Tool**: `plantuml` skill (auto-invoked). Always render PNG or SVG.
GitHub wiki does not render PlantUML source.

**Diagram types**:
1. **Salt wireframe**: UI mocks and screen sketches
2. **Use case**: Actors and goals
3. **Timing**: Clock, waveform
4. **ArchiMate**: Enterprise layers
5. **nwdiag / WBS**: Network racks and work breakdown

**Command examples**:

**Wireframe**:
```
Draw a login wireframe
Sketch the checkout screen
```

**Use case**:
```
Create a use case diagram for the billing actors
```

**Output**: `docs/diagrams/{diagram-type}.puml` plus PNG or SVG

**Token cost**: ~4,200 tokens

---

### Diagram Selection Guide

**When to use C4 (Mermaid)**:
- 🎯 High-level system overview (executives, stakeholders)
- 🎯 Application architecture (containers, microservices)
- 🎯 Internal component structure
- ✅ Simple, clean visuals
- ✅ Fast generation

**When to use UML (PlantUML)**:
- 🎯 Time-sequenced interactions (API flows, method calls)
- 🎯 Database schema (ER diagrams)
- 🎯 Object-oriented design (class relationships)
- 🎯 Stateful entities (state machines)
- 🎯 Business processes (activity diagrams)
- ✅ Detailed, technical documentation
- ✅ Advanced customization

---

## Advanced Usage

### Multi-Project Documentation

**Scenario**: Monorepo with multiple microservices

**Command**:
```
Generate documentation for all services in ~/projects/ecommerce-platform
```

**What happens**:
1. Discovers all projects in directory
2. Detects framework for each (Spring Boot, React, etc.)
3. Generates individual documentation per service
4. Creates overview document linking all services
5. Generates system-wide C4 context diagram

**Output**:
```
docs/
├── overview.md                        # Links to all services
├── diagrams/
│   └── c4-system-context.md           # All services in one diagram
├── user-service/
│   ├── design/user-service-sdd.md
│   └── api/user-service-openapi.yaml
├── order-service/
│   ├── design/order-service-sdd.md
│   └── api/order-service-openapi.yaml
└── payment-service/
    ├── design/payment-service-sdd.md
    └── api/payment-service-openapi.yaml
```

---

### Custom Templates

**Scenario**: Your organization has custom documentation standards

**Command**:
```
Use my custom SRS template at templates/acme-srs-template.md for this project
```

**What happens**:
1. Reads your custom template
2. Identifies placeholders
3. Uses your template instead of default
4. Preserves your company's formatting, sections, terminology

**Custom template example**:
```markdown
# [PROJECT_NAME] - Software Requirements Specification

**Company**: ACME Corporation
**Department**: [DEPARTMENT]
**Project Code**: [PROJECT_CODE]

... your custom sections ...
```

---

### Continuous Documentation (CI/CD Integration)

**Scenario**: Auto-generate docs on every commit

**Setup**:
```
Help me set up automated documentation generation in my CI/CD pipeline
```

**What the skill provides**:
1. **Git hooks** for documentation updates:
   ```bash
   #!/bin/bash
   # pre-commit hook
   claude-code "/skill documentation-specialist" "Update docs for changed files"
   ```

2. **GitHub Actions workflow**:
   ```yaml
   name: Generate Documentation
   on: [push]
   jobs:
     docs:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v2
         - name: Generate docs
           run: |
             claude-code "/skill documentation-specialist" \
               "Document all Spring Boot services"
         - name: Commit docs
           run: |
             git add docs/
             git commit -m "docs: auto-generate documentation"
             git push
   ```

3. **Documentation validation scripts**:
   ```bash
   # Validate all OpenAPI specs
   find docs/api -name "*.yaml" -exec \
     claude-code "/skill documentation-specialist" \
     "Audit {}" \;
   ```

---

## Troubleshooting

### Issue: "Framework not detected"

**Symptom**: Skill says "I couldn't detect your framework"

**Causes**:
1. Detection files missing (pom.xml, Pulumi.yaml, etc.)
2. Code patterns not found (no @SpringBootApplication, etc.)
3. Framework not yet supported

**Solutions**:
```bash
# Verify detection files exist
ls pom.xml build.gradle Pulumi.yaml package.json

# Verify code patterns
grep -r "@SpringBootApplication" src/
grep -r "import pulumi" .
grep -r "from fastapi import" .

# Manually specify framework
Document this as a Spring Boot application at ~/projects/api
```

---

### Issue: "Generated documentation is too generic"

**Symptom**: SRS lacks specific details about your project

**Cause**: Insufficient context in command

**Solution**: Provide detailed context

❌ **Too generic**:
```
Create an SRS for a web app
```

✅ **Detailed context**:
```
Create an SRS for a HIPAA-compliant patient portal web application with:
- User authentication (SSO via OAuth2, MFA)
- Electronic Health Records integration (HL7 FHIR)
- Appointment scheduling (Google Calendar sync)
- Secure messaging (encrypted, audit-logged)
- Prescription management (e-prescription via SureScripts)
- Must support 50,000 patients
- 99.95% uptime SLA
- HIPAA BAA compliance required
- SOC 2 Type II audit ready
```

**Result**: Highly specific SRS with healthcare regulations, security requirements, compliance sections.

---

### Issue: "Diagrams not generated"

**Symptom**: Skill generates docs but no diagrams

**Causes**:
1. `design-doc-mermaid` or `plantuml` skills not installed
2. Diagram generation not offered
3. Diagram type not supported

**Solutions**:
```bash
# Install diagram skills
/skill design-doc-mermaid
/skill plantuml

# Explicitly request diagrams
Generate C4 container diagram for my architecture
Create ER diagram from my database entities
Add sequence diagrams to the API documentation
```

---

### Issue: "Cannot convert to Word/PDF"

**Symptom**: Conversion fails or skill says skill not available

**Causes**:
1. `docx` or `pdf` skills not installed
2. Source file not found
3. Markdown syntax errors

**Solutions**:
```bash
# Install conversion skills
/skill docx
/skill pdf

# Verify source file exists
ls docs/requirements/billing-srs.md

# Fix markdown syntax errors
# (headings must be sequential: H1 → H2 → H3)
```

---

## Best Practices

### 1. Docs-as-Code

✅ **Update docs in the same commit as code**:
```bash
git add src/controllers/OrderController.java
git add docs/api/ecommerce-openapi.yaml
git commit -m "feat: add order cancellation endpoint"
```

✅ **Review docs in pull requests**:
- Include documentation changes in PRs
- Treat docs like code (code review applies)

✅ **Automate with CI/CD**:
- Generate docs on every push
- Validate OpenAPI specs in CI
- Fail build if docs are outdated

---

### 2. Living Documentation (The Bonsai Tree Principle)

✅ **Keep docs alive but trimmed**:
- Small, fresh, accurate docs > large stale docs
- Delete outdated documentation
- Quarterly doc review sprints

❌ **Avoid**:
- Exhaustive documentation that becomes unmaintainable
- Documentation that duplicates code
- Over-engineered doc processes

---

### 3. Audience-Specific Documentation

**Different docs for different audiences**:

| Audience | Documents | Focus |
|----------|-----------|-------|
| **Stakeholders** (Executives, PMs) | PRD, SRS, Use Cases | Why & What |
| **Developers** (Engineers) | SDD, arc42, OpenAPI, Deployment | How |
| **End-Users** (Customers) | User Guides, KB Articles | How-To |

❌ **Don't**: Force all documentation into a single tool
✅ **Do**: Use the right tool for each audience

---

### 4. Minimum Viable Documentation (MVD)

✅ **Focus on**:
- Documents that answer specific questions
- Documentation that reduces support burden
- Short, useful docs essential for target audience

❌ **Avoid**:
- Exhaustive "complete" documentation
- Documentation that duplicates code comments
- Docs nobody reads

---

### 5. Progressive Enhancement

**Start minimal, add as needed**:

**Phase 1** (Week 1):
- README.md (project overview)
- API documentation (OpenAPI spec)

**Phase 2** (Month 1):
- SDD (architecture overview)
- Deployment docs (how to run/deploy)

**Phase 3** (Quarter 1):
- User guides (for complex features)
- SRS (for compliance-critical modules)

**Phase 4** (As needed):
- PRDs (for major features)
- Detailed diagrams (for onboarding)

---

## Conclusion

The **Documentation Specialist** skill provides:

✅ **Greenfield**: Professional docs from templates (SRS, PRD, OpenAPI)
✅ **Brownfield**: Auto-generated docs from code (Spring Boot, Pulumi)
✅ **Audit**: Quality control and improvement recommendations
✅ **Convert**: Multi-format output (Markdown, DOCX, PDF)
✅ **Diagrams**: Visual documentation (C4, UML)

**Token Efficiency**: 54% reduction via Progressive Disclosure Architecture

**Next Steps**:
1. Try the Quick Start examples in README.md
2. Experiment with your own projects
3. Review the workflow guides in `workflows/`
4. Check the PDA_MIGRATION_SUMMARY.md for architecture details

---

**Questions?**
- Review `reference/comprehensive-guide.md.backup` for deep dive
- Check `workflows/*.md` for detailed execution workflows
- Examine `mappings/backend/spring-boot-mapping.yaml` for code-to-docs examples

---

**Happy Documenting!** 🚀

**Version**: 2.0.0-PDA
**Last Updated**: 2025-01-13
