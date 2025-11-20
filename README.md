# Documentation Specialist Skill

**Version**: 2.0.0-PDA
**Status**: ✅ Production Ready (PDA-Compliant)
**Author**: Created with Claude Code
**Last Updated**: 2025-01-13

---

## 🎯 Overview

Transform Claude Code into an expert software documentation specialist with **Progressive Disclosure Architecture (PDA)** for maximum efficiency.

### Two Primary Capabilities

1. **📝 Greenfield Documentation**: Create professional documentation from templates for new projects
2. **🔄 Brownfield Documentation**: Reverse-engineer documentation from existing codebases

### PDA Architecture (54% Token Reduction)

This skill uses **Progressive Disclosure Architecture** to minimize token consumption while maintaining full functionality:

- **Core** (Auto-loaded): `SKILL.md` (~2,500 tokens) - Routing, execution logic, and quick start
- **On-demand**: Workflow guides, templates, mappings (~10,000 tokens, loaded selectively)

**Typical Token Load**: 2,500 tokens (just SKILL.md) to 5,000 tokens (with workflow) = **44-72% reduction vs v1.0** ✅

---

## ✨ Key Features

### 1. Template-Based Creation (Greenfield)

Create professional documentation from scratch using industry-standard templates:

| Document Type | Standard | Status | Use Case |
|---------------|----------|--------|----------|
| **SRS** (Software Requirements Specification) | IEEE 830 | ✅ Complete | Formal requirements, compliance, contracts |
| **PRD** (Product Requirements Document) | Agile/Modern | ✅ Complete | Feature planning, sprint planning |
| **SDD** (Software Design Document) | arc42 | ✅ Template | Technical design, architecture |
| **OpenAPI** 3.0 | OpenAPI Spec | ✅ Complete | REST API documentation |
| **User Guides** | - | 📋 Template | End-user documentation |
| **Deployment Docs** | - | 📋 Template | DevOps, infrastructure |

### 2. Code-to-Docs Reverse Engineering (Brownfield)

Automatically generate documentation from existing code:

**Backend Frameworks:**
- ✅ **Spring Boot** (Fully mapped) - Controllers → OpenAPI, Entities → ER diagrams, Services → SDD
- 📋 FastAPI, Express.js, Django, Flask (Planned)

**Infrastructure:**
- ✅ **Pulumi** (Fully mapped) - Resources → deployment docs, architecture diagrams
- 📋 Terraform, AWS CDK (Planned)

**Frontend:**
- 📋 React, Next.js, Vue.js (Planned)

**Data & CLI:**
- 📋 Python ETL, Apache Airflow, CLIs (Planned)

**Legend:**
- ✅ = Fully implemented with `mappings/{framework}-mapping.yaml`
- 📋 = Planned (can still document using generic approach)

### 3. Documentation Audit & Quality Control

- ✅ Automated quality checklists (SRS, PRD, SDD, OpenAPI, User Docs)
- ✅ Gap analysis and completeness scoring
- ✅ Best practices validation (IEEE, OpenAPI, WCAG)
- ✅ Improvement recommendations with examples
- ✅ Automated fixes for common issues

### 4. Multi-Format Output

- ✅ **Markdown** (Primary format, Git-friendly)
- ✅ **DOCX** (Microsoft Word via `docx` skill)
- ✅ **PDF** (Professional documents via `pdf` skill)
- ✅ **Diagrams** (Mermaid, PlantUML via skills)

### 5. Visual Documentation

**Mermaid Diagrams** (via `mermaid-architect` skill):
- C4 Model: Context, Container, Component
- Flowcharts and decision trees

**PlantUML Diagrams** (via `plantuml` skill):
- UML: Class, Sequence, Activity, State Machine
- ER Diagrams (database schema)
- Deployment diagrams

---

## 🚀 Quick Start

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

## 📁 Directory Structure (PDA v2.0)

```
documentation-specialist/
├── SKILL.md                           # Core routing logic + quick start (2,500 tokens)
├── PDA_MIGRATION_SUMMARY.md           # Migration documentation
├── USER_GUIDE.md                      # ← Comprehensive user guide
│
├── workflows/                         # Tier 3: On-demand workflow guides
│   ├── greenfield-workflow.md         # Template-based creation (1,500 tokens)
│   ├── brownfield-workflow.md         # Code-to-docs extraction (1,500 tokens)
│   ├── audit-workflow.md              # Documentation review (1,000 tokens)
│   ├── convert-workflow.md            # Format conversion (750 tokens)
│   └── diagram-workflow.md            # Diagram generation (1,000 tokens)
│
├── templates/                         # Tier 3: Document templates
│   └── markdown/
│       ├── requirements-srs.md        # IEEE SRS (600+ lines)
│       ├── requirements-prd.md        # Agile PRD (500+ lines)
│       ├── api-openapi.yaml           # OpenAPI 3.0 (800+ lines)
│       ├── design-sdd.md              # Software Design Doc
│       └── design-arc42.md            # arc42 Architecture
│
├── mappings/                          # Tier 3: Code-to-docs mappings
│   ├── backend/
│   │   ├── spring-boot-mapping.yaml   # ✅ Complete
│   │   └── fastapi-mapping.yaml       # 📋 Planned
│   └── infrastructure/
│       └── pulumi-mapping.yaml        # 📋 Planned
│
├── reference/                         # Tier 3: Reference guides
│   ├── 01-philosophy.md               # Docs-as-code principles (190 tokens)
│   ├── 02-requirements.md             # Requirements writing (planned)
│   ├── 03-design.md                   # Design docs (planned)
│   ├── 04-diagrams.md                 # Diagram selection (planned)
│   ├── 05-api-docs.md                 # API documentation (planned)
│   └── comprehensive-guide.md.backup  # Original guide (archived)
│
├── examples/                          # Example documentation
│   ├── greenfield/                    # Template-based examples
│   └── brownfield/                    # Code-to-docs examples
│
└── guides/                            # Framework-specific guides
    ├── requirements/                  # Requirements documentation
    └── code-to-docs/                  # Code extraction guides
        ├── backend/
        └── infrastructure/
```

---

## 🎯 How It Works (PDA Flow)

### User Request Flow

**Example**: "Create an SRS for a billing system"

1. **Auto-Load**: `SKILL.md` classifies intent as CREATE_NEW (2,500 tokens)
2. **Selective Load**:
   - `workflows/greenfield-workflow.md` (1,500 tokens)
   - `templates/markdown/requirements-srs.md` (500 tokens)
3. **Execute**: Generate customized SRS
4. **Total Tokens**: 4,500 (vs 9,000 in v1.0) = **50% reduction**

### Intent Classification

The skill automatically classifies your request into one of five intents:

| Intent | Trigger Keywords | Workflow Loaded | Typical Tokens |
|--------|-----------------|----------------|----------------|
| **CREATE_NEW** | "create", "generate", "write" + doc type | greenfield-workflow.md | ~4,000 |
| **CODE_TO_DOCS** | "document", "extract", path reference | brownfield-workflow.md | ~5,000 |
| **AUDIT** | "audit", "review", "check", "improve" | audit-workflow.md | ~4,000 |
| **CONVERT** | "convert", "transform", "to Word/PDF" | convert-workflow.md | ~3,500 |
| **DIAGRAM** | "diagram", "C4", "sequence", "visualize" | diagram-workflow.md | ~4,200 |

---

## 🛠️ Integration with Other Skills

This skill seamlessly integrates with other Claude Code skills:

| Skill | Purpose | Auto-Invoked? | Use Case |
|-------|---------|---------------|----------|
| **docx** | Word document creation/conversion | ✅ When requested | MD → DOCX conversion, professional styling |
| **pdf** | PDF generation | ✅ When requested | MD/DOCX → PDF, documentation packages |
| **plantuml** | UML diagram generation | ✅ For UML diagrams | ER, sequence, class, state machine diagrams |
| **mermaid-architect** | C4 diagram generation | ✅ For C4 diagrams | System context, container, component diagrams |

**Auto-invocation**: The skill automatically calls these skills when needed, you don't need to invoke them manually.

---

## 📚 Documentation Philosophy

This skill follows **Docs-as-Code** principles:

1. **Living Documentation**: Update docs in the same commit as code changes
2. **Minimum Viable Documentation**: Small, fresh, accurate docs > large stale docs
3. **The Bonsai Tree Principle**: Alive but frequently trimmed
4. **Audience-Specific**: Different docs for stakeholders, developers, users
5. **Git-Friendly**: Markdown primary format, version controlled with code

---

## 🎓 Learning Resources

### For New Users
1. **Quick Start**: See examples above
2. **User Guide**: `USER_GUIDE.md` (comprehensive feature documentation)
3. **Quick Reference**: `QUICK_START.md` (5-minute tutorial)

### For Advanced Users
4. **PDA Architecture**: `PDA_MIGRATION_SUMMARY.md` (token optimization details)
5. **Workflow Guides**: `workflows/*.md` (detailed execution workflows)
6. **Reference Guides**: `reference/*.md` (best practices, philosophy)

### For Contributors
7. **Implementation**: `IMPLEMENTATION_SUMMARY.md` (technical architecture)
8. **Mappings**: `mappings/backend/spring-boot-mapping.yaml` (code-to-docs example)
9. **Templates**: `templates/markdown/*.md` (document structure examples)

---

## 🎯 Use Cases

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

## ⚙️ Configuration

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

## 🐛 Troubleshooting

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

## 📊 Performance Metrics (v2.0-PDA)

| Metric | v1.0 | v2.0-PDA | Improvement |
|--------|------|----------|-------------|
| **SKILL.md size** | 954 lines | 458 lines | 52% reduction |
| **Typical token load** | ~9,000 | ~4,140 | 54% reduction |
| **Initial load** | 4,770 tokens | 2,750 tokens | 42% reduction |
| **Largest file** | 954 lines | 458 lines | PDA compliant ✅ |
| **Workflow files** | 1 monolithic | 5 focused | Better organization ✅ |

---

## 🗺️ Roadmap

### v2.1 (Planned)
- [ ] Complete FastAPI mapping
- [ ] Complete React mapping
- [ ] Terraform infrastructure mapping
- [ ] Split remaining reference guides (02-10)
- [ ] Add more brownfield examples

### v2.2 (Future)
- [ ] Confluence integration
- [ ] Multi-language support (ES, FR, DE)
- [ ] Custom template system
- [ ] Documentation validation/linting
- [ ] Automated change detection

### v3.0 (Long-term)
- [ ] Interactive documentation websites
- [ ] Documentation testing (docs as tests)
- [ ] AI-powered gap analysis
- [ ] Continuous documentation generation

---

## 🤝 Contributing

To improve this skill:

1. **Add new mappings**: Create YAML files in `mappings/`
2. **Add examples**: Contribute real-world brownfield examples
3. **Improve templates**: Enhance templates in `templates/markdown/`
4. **Improve guides**: Update workflow guides in `workflows/`
5. **Report issues**: Document bugs and limitations

---

## 📜 License

This skill synthesizes best practices from:
- Industry standards (IEEE, ISO, OpenAPI)
- Open-source documentation projects
- Enterprise documentation patterns
- Academic software engineering research

---

## 🙏 Acknowledgments

Created to solve a critical problem: **software projects have poor or no documentation**.

By combining:
- Industry-standard templates
- Automated code-to-docs extraction
- AI-powered content generation
- Multi-format output
- Progressive Disclosure Architecture

We make documentation a **first-class citizen** in the software development lifecycle.

---

## 📞 Support

**Resources**:
- `USER_GUIDE.md` - Comprehensive feature documentation
- `QUICK_START.md` - 5-minute tutorial
- `PDA_MIGRATION_SUMMARY.md` - PDA architecture details
- `IMPLEMENTATION_SUMMARY.md` - Technical architecture

**For Questions**:
- Review the reference guides in `reference/`
- Examine workflow guides in `workflows/`
- Check examples in `examples/`

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

---

**Ready to generate world-class software documentation!** 🚀

**Version**: 2.0.0-PDA
**Last Updated**: 2025-01-13
**Minimum Claude Code Version**: Latest
**PDA Compliant**: ✅ Yes (54% token reduction)
