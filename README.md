# Documentation Specialist Skill

**Version**: 3.0-PDA
**Status**: Production Ready (PDA-Compliant)
**Author**: Created with Claude Code
**Last Updated**: 2025-01-13

Transform Claude Code into an expert software documentation specialist with **Progressive Disclosure Architecture (PDA)** for maximum efficiency.

---

## Installation

### One-Click Install via Skilz Marketplace

Install this skill instantly from the [Skilz Marketplace](https://skillzwave.ai/skill/SpillwaveSolutions__document-specialist-skill__documentation-specialist__SKILL/):

```bash
skilz install SpillwaveSolutions_document-specialist-skill/documentation-specialist
```

### Manual Installation

Clone directly into your Claude Code skills directory:

```bash
# Navigate to your skills directory
cd ~/.claude/skills

# Clone the repository
git clone https://github.com/SpillwaveSolutions/document-specialist-skill.git
```

### Verify Installation

After installation, verify the skill is available:

```bash
# List installed skills
ls ~/.claude/skills/document-specialist-skill

# Or ask Claude Code
# "List my installed skills"
```

---

## Overview

### Two Primary Capabilities

1. **Greenfield Documentation**: Create professional documentation from templates for new projects
2. **Brownfield Documentation**: Reverse-engineer documentation from existing codebases

### PDA Architecture (54% Token Reduction)

This skill uses **Progressive Disclosure Architecture** to minimize token consumption while maintaining full functionality:

- **Core** (Auto-loaded): `SKILL.md` (~2,500 tokens) - Routing, execution logic, and quick start
- **On-demand**: Workflow guides, templates, mappings (~10,000 tokens, loaded selectively)

**Typical Token Load**: 2,500 tokens (just SKILL.md) to 5,000 tokens (with workflow) = **44-72% reduction vs v1.0**

---

## Key Features

### 1. Template-Based Creation (Greenfield)

Create professional documentation from scratch using industry-standard templates:

| Document Type | Standard | Status | Use Case |
|---------------|----------|--------|----------|
| **SRS** (Software Requirements Specification) | IEEE 830 | Complete | Formal requirements, compliance, contracts |
| **PRD** (Product Requirements Document) | Agile/Modern | Complete | Feature planning, sprint planning |
| **SDD** (Software Design Document) | arc42 | Template | Technical design, architecture |
| **OpenAPI** 3.0 | OpenAPI Spec | Complete | REST API documentation |
| **User Guides** | - | Template | End-user documentation |
| **Deployment Docs** | - | Template | DevOps, infrastructure |

### 2. Code-to-Docs Reverse Engineering (Brownfield)

Automatically generate documentation from existing code:

**Backend Frameworks:**
- **Spring Boot** (Fully mapped) - Controllers to OpenAPI, Entities to ER diagrams, Services to SDD
- FastAPI, Express.js, Django, Flask (Planned)

**Infrastructure:**
- **Pulumi** (Fully mapped) - Resources to deployment docs, architecture diagrams
- Terraform, AWS CDK (Planned)

**Frontend:**
- React, Next.js, Vue.js (Planned)

**Data and CLI:**
- Python ETL, Apache Airflow, CLIs (Planned)

### 3. Documentation Audit and Quality Control

- Automated quality checklists (SRS, PRD, SDD, OpenAPI, User Docs)
- Gap analysis and completeness scoring
- Best practices validation (IEEE, OpenAPI, WCAG)
- Improvement recommendations with examples
- Automated fixes for common issues

### 4. Multi-Format Output

- **Markdown** (Primary format, Git-friendly)
- **DOCX** (Microsoft Word via `docx` skill)
- **PDF** (Professional documents via `pdf` skill)
- **Diagrams** (Mermaid, PlantUML via skills)

### 5. Visual Documentation

**Mermaid Diagrams** (via `mermaid-architect` skill):
- C4 Model: Context, Container, Component
- Flowcharts and decision trees

**PlantUML Diagrams** (via `plantuml` skill):
- UML: Class, Sequence, Activity, State Machine
- ER Diagrams (database schema)
- Deployment diagrams

---

## Quick Start

### Example 1: Create a Requirements Document

```
Create a Software Requirements Specification for a payment processing system
```

**Generates**: IEEE-compliant SRS with functional requirements, NFRs, acceptance criteria

### Example 2: Document Existing Spring Boot App

```
Document my Spring Boot application at ~/projects/ecommerce-api
```

**Generates**: SDD (arc42), OpenAPI spec, C4 diagram, ER diagram, Component diagram

### Example 3: Audit API Documentation

```
Audit my OpenAPI specification at docs/api/openapi.yaml
```

**Generates**: Audit report with quality score, gap analysis, recommendations

### Example 4: Convert to Multiple Formats

```
Convert docs/requirements/billing-srs.md to Word format
```

**Generates**: Professionally styled DOCX with TOC, styles, formatting

### Example 5: Generate Architecture Diagrams

```
Create a C4 container diagram for my e-commerce microservices platform
```

**Generates**: C4 container diagram showing services, databases, external systems

---

## Directory Structure (PDA v3.0)

```
documentation-specialist/
|-- SKILL.md                           # Core routing logic + quick start (2,500 tokens)
|-- README.md                          # This file
|-- USER_GUIDE.md                      # Comprehensive user guide
|
|-- references/
|   |-- workflows/                     # On-demand workflow guides
|   |   |-- greenfield-workflow.md     # Template-based creation (1,500 tokens)
|   |   |-- brownfield-workflow.md     # Code-to-docs extraction (1,500 tokens)
|   |   |-- audit-workflow.md          # Documentation review (1,000 tokens)
|   |   |-- convert-workflow.md        # Format conversion (750 tokens)
|   |   |-- diagram-workflow.md        # Diagram generation (1,000 tokens)
|   |   |-- user-docs-workflow.md      # User documentation
|   |   |-- tutorial-workflow.md       # Tutorial creation
|   |   |-- runbook-workflow.md        # Operational runbooks
|   |   +-- TOC.md                     # Navigation index
|   |
|   |-- templates/                     # Document templates
|   |   +-- markdown/
|   |       |-- requirements-srs.md    # IEEE SRS (600+ lines)
|   |       |-- requirements-prd.md    # Agile PRD (500+ lines)
|   |       |-- api-openapi.yaml       # OpenAPI 3.0 (800+ lines)
|   |       |-- user-manual.md         # User manual template
|   |       |-- howto-guide.md         # How-to guide template
|   |       |-- getting-started.md     # Getting started template
|   |       |-- developer-tutorial.md  # Developer tutorial
|   |       +-- runbook.md             # Runbook template
|   |
|   |-- mappings/                      # Code-to-docs mappings
|   |   +-- backend/
|   |       |-- spring-boot-mapping.yaml  # Complete
|   |       +-- fastapi-mapping.yaml      # Complete
|   |
|   |-- reference/                     # Reference guides
|   |   |-- comprehensive-guide.md     # Navigation to all 27 guides
|   |   +-- 01-philosophy.md           # Docs-as-code principles
|   |
|   +-- examples/                      # Example documentation
|       |-- TOC.md                     # Navigation to all examples
|       |-- greenfield/                # Template-based examples
|       +-- brownfield/                # Code-to-docs examples
```

---

## How It Works (PDA Flow)

### User Request Flow

**Example**: "Create an SRS for a billing system"

1. **Auto-Load**: `SKILL.md` classifies intent as CREATE_NEW (2,500 tokens)
2. **Selective Load**:
   - `workflows/greenfield-workflow.md` (1,500 tokens)
   - `templates/markdown/requirements-srs.md` (500 tokens)
3. **Execute**: Generate customized SRS
4. **Total Tokens**: 4,500 (vs 9,000 in v1.0) = **50% reduction**

### Intent Classification

The skill automatically classifies your request into one of eight intents:

| Intent | Trigger Keywords | Workflow Loaded | Typical Tokens |
|--------|-----------------|----------------|----------------|
| **CREATE_NEW** | "create", "generate", "write" + doc type | greenfield-workflow.md | ~4,000 |
| **CODE_TO_DOCS** | "document", "extract", path reference | brownfield-workflow.md | ~5,000 |
| **AUDIT** | "audit", "review", "check", "improve" | audit-workflow.md | ~4,000 |
| **CONVERT** | "convert", "transform", "to Word/PDF" | convert-workflow.md | ~3,500 |
| **DIAGRAM** | "diagram", "C4", "sequence", "visualize" | diagram-workflow.md | ~4,200 |
| **USER_DOCS** | "user manual", "how-to", "getting started" | user-docs-workflow.md | ~3,500 |
| **TUTORIAL** | "tutorial", "API guide", "CLI docs" | tutorial-workflow.md | ~3,500 |
| **RUNBOOK** | "runbook", "procedure", "incident" | runbook-workflow.md | ~3,500 |

---

## Integration with Other Skills

This skill seamlessly integrates with other Claude Code skills:

| Skill | Purpose | Auto-Invoked? | Use Case |
|-------|---------|---------------|----------|
| **docx** | Word document creation/conversion | Yes when requested | MD to DOCX conversion, professional styling |
| **pdf** | PDF generation | Yes when requested | MD/DOCX to PDF, documentation packages |
| **plantuml** | UML diagram generation | Yes for UML diagrams | ER, sequence, class, state machine diagrams |
| **mermaid-architect** | C4 diagram generation | Yes for C4 diagrams | System context, container, component diagrams |

**Auto-invocation**: The skill automatically calls these skills when needed, you do not need to invoke them manually.

---

## Documentation Philosophy

This skill follows **Docs-as-Code** principles:

1. **Living Documentation**: Update docs in the same commit as code changes
2. **Minimum Viable Documentation**: Small, fresh, accurate docs over large stale docs
3. **The Bonsai Tree Principle**: Alive but frequently trimmed
4. **Audience-Specific**: Different docs for stakeholders, developers, users
5. **Git-Friendly**: Markdown primary format, version controlled with code

---

## Use Cases

### Use Case 1: Starting a New Project (Greenfield)

**Scenario**: Building a new SaaS product, need documentation from day one.

**Commands**:
```
1. Create a PRD for a team collaboration platform with real-time messaging
2. Create an SRS for the billing module (high-risk, compliance-critical)
3. Generate an arc42 architecture document for microservices
4. Create OpenAPI spec for the REST API
```

**Result**: Complete documentation suite ready for development kickoff.

---

### Use Case 2: Documenting Legacy Code (Brownfield)

**Scenario**: Inherited a Spring Boot application with zero documentation.

**Command**:
```
Document my Spring Boot application at ~/projects/customer-api
```

**Result**:
- Software Design Document (arc42 format, 20+ pages)
- OpenAPI specification (extracted from @RestController classes)
- C4 Container diagram (shows architecture)
- Component diagram (shows layer structure)
- ER diagram (from @Entity classes)
- Sequence diagrams (for key workflows)

---

### Use Case 3: Compliance Audit

**Scenario**: Company needs formal documentation for SOC 2 compliance.

**Commands**:
```
1. Create a formal SRS for our payment processing system
2. Audit the SRS for completeness
3. Convert to Word format with professional styling
4. Generate PDF documentation package
```

**Result**: Enterprise-grade, audit-ready documentation.

---

### Use Case 4: API Documentation

**Scenario**: Need to document API for external developers.

**Commands**:
```
1. Extract OpenAPI spec from my FastAPI application at ~/api
2. Audit the OpenAPI spec for best practices
3. Create sequence diagrams for key API workflows
4. Convert to PDF for distribution
```

**Result**: Professional API documentation ready for developer portal.

---

## Configuration

### Custom Templates

Override default templates:

```
Use my custom SRS template at templates/my-company-srs.md for this project
```

The skill will use your template instead of the default.

### Framework Mapping

To add support for a new framework:

1. Create `mappings/{category}/{framework}-mapping.yaml`
2. Define detection patterns, extraction rules
3. Test with real codebase

See `mappings/backend/spring-boot-mapping.yaml` for a complete example.

---

## Troubleshooting

### Issue: Framework not detected

**Solution**: Verify detection files exist:
```bash
# For Spring Boot:
ls pom.xml build.gradle
grep -r "@SpringBootApplication" src/
```

If detection fails, manually specify:
```
Document this as a Spring Boot application at [path]
```

---

### Issue: Generated docs too generic

**Solution**: Provide more context in your request:

**Generic**:
```
Create an SRS for an app
```

**Specific** (Better):
```
Create an SRS for a HIPAA-compliant telemedicine app with video consultations,
prescription management, and EHR integration. Must support 10,000 concurrent users.
```

---

### Issue: Diagrams not generated

**Solution**: Ensure required skills are installed:
```
/skill mermaid-architect
/skill plantuml
```

---

### Issue: Cannot convert to Word/PDF

**Solution**: Ensure format conversion skills are installed:
```
/skill docx
/skill pdf
```

---

## Performance Metrics (v3.0-PDA)

| Metric | v1.0 | v3.0-PDA | Improvement |
|--------|------|----------|-------------|
| **SKILL.md size** | 954 lines | ~140 lines | 85% reduction |
| **Typical token load** | ~9,000 | ~4,140 | 54% reduction |
| **Initial load** | 4,770 tokens | 2,750 tokens | 42% reduction |
| **Workflow files** | 1 monolithic | 8 focused | Better organization |

---

## Roadmap

### v3.1 (Planned)
- [ ] Complete React mapping
- [ ] Terraform infrastructure mapping
- [ ] Additional reference guides
- [ ] More brownfield examples

### v3.2 (Future)
- [ ] Confluence integration
- [ ] Multi-language support (ES, FR, DE)
- [ ] Custom template system
- [ ] Documentation validation/linting
- [ ] Automated change detection

### v4.0 (Long-term)
- [ ] Interactive documentation websites
- [ ] Documentation testing (docs as tests)
- [ ] AI-powered gap analysis
- [ ] Continuous documentation generation

---

## Contributing

To improve this skill:

1. **Add new mappings**: Create YAML files in `mappings/`
2. **Add examples**: Contribute real-world brownfield examples
3. **Improve templates**: Enhance templates in `templates/markdown/`
4. **Improve guides**: Update workflow guides in `workflows/`
5. **Report issues**: Document bugs and limitations

---

## Learning Resources

### For New Users
1. **Quick Start**: See examples above
2. **User Guide**: `USER_GUIDE.md` (comprehensive feature documentation)

### For Advanced Users
3. **PDA Architecture**: Understand token optimization details
4. **Workflow Guides**: `references/workflows/*.md` (detailed execution workflows)
5. **Reference Guides**: `references/reference/*.md` (best practices, philosophy)

### For Contributors
6. **Mappings**: `references/mappings/backend/spring-boot-mapping.yaml` (code-to-docs example)
7. **Templates**: `references/templates/markdown/*.md` (document structure examples)

---

## Quick Command Reference

| Task | Command Example |
|------|----------------|
| **Create SRS** | `Create an SRS for [project description]` |
| **Create PRD** | `Create a PRD for [feature description]` |
| **Document code** | `Document my [framework] app at [path]` |
| **Extract API docs** | `Generate OpenAPI spec from [path]` |
| **Audit docs** | `Audit my [doc type] at [path]` |
| **Convert format** | `Convert [file] to [Word/PDF]` |
| **Create diagram** | `Create a [diagram type] for [system]` |
| **Package docs** | `Generate PDF package from all docs` |
| **Create user manual** | `Create a user manual for [product]` |
| **Create tutorial** | `Create a tutorial for [topic]` |
| **Create runbook** | `Create a runbook for [procedure]` |

---

## License

This skill synthesizes best practices from:
- Industry standards (IEEE, ISO, OpenAPI)
- Open-source documentation projects
- Enterprise documentation patterns
- Academic software engineering research

---

## Acknowledgments

Created to solve a critical problem: **software projects have poor or no documentation**.

By combining:
- Industry-standard templates
- Automated code-to-docs extraction
- AI-powered content generation
- Multi-format output
- Progressive Disclosure Architecture

We make documentation a **first-class citizen** in the software development lifecycle.

---

## Related Skills

- **docx** - Microsoft Word document creation
- **pdf** - PDF generation and manipulation
- **plantuml** - PlantUML diagram generation
- **mermaid-architect** - Mermaid diagram creation

---

**Version**: 3.0-PDA
**Last Updated**: 2025-01-13
**Minimum Claude Code Version**: Latest
**PDA Compliant**: Yes (54% token reduction)

Ready to generate world-class software documentation!
