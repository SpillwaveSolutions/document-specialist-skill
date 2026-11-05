# Requirements Documentation Guides

This directory contains specialized guides for creating requirements documentation.

## Available Guides

### 1. srs-guide.md
**Software Requirements Specification (SRS)**
- Formal, comprehensive requirements documentation
- IEEE-standard compliant structure
- Best for: High-assurance, regulated, or enterprise projects
- Key sections: Introduction, Functional Requirements, Non-Functional Requirements, Use Cases

### 2. prd-guide.md
**Product Requirements Document (PRD)**
- Modern, agile requirements documentation
- Business-focused with clear success metrics
- Best for: Product development, startups, agile teams
- Key sections: Objective, Success Metrics, User Stories, Out of Scope

### 3. user-stories-guide.md
**User Stories**
- Atomic requirements from user perspective
- "As a [user], I want to [goal], so that [benefit]"
- Best for: Agile development, iterative projects
- Includes: Story format, acceptance criteria, story mapping

### 4. acceptance-criteria-guide.md
**Acceptance Criteria**
- Testable conditions for user story completion
- Given-When-Then (Gherkin) format
- BDD-style scenario writing
- Best for: Ensuring testability and clarity

### 5. requirements-best-practices.md
**General Best Practices**
- Clear, unambiguous language
- Testable requirements
- Requirements traceability
- MoSCoW prioritization
- Avoiding common pitfalls

### 6. context-diagrams-guide.md
**System Context Diagrams**
- C4 Level 1 context diagrams
- DFD Level 0 diagrams
- Defining system boundaries
- Identifying external actors and systems

## When to Use Which Guide

| Scenario | Recommended Guide |
|----------|-------------------|
| Enterprise system with formal approvals | srs-guide.md |
| Product feature for SaaS application | prd-guide.md |
| Agile sprint planning | user-stories-guide.md |
| Ensuring testability | acceptance-criteria-guide.md |
| System scoping | context-diagrams-guide.md |
| General requirements writing | requirements-best-practices.md |

## Common Patterns

### Pattern 1: Formal Project (Waterfall-ish)
1. Start with srs-guide.md
2. Add context-diagrams-guide.md for system boundary
3. Apply requirements-best-practices.md for quality

### Pattern 2: Agile Product Development
1. Start with prd-guide.md for product vision
2. Break down into user-stories-guide.md
3. Add acceptance-criteria-guide.md for testability

### Pattern 3: Hybrid (Risk-Based)
1. Use prd-guide.md for most features
2. Use srs-guide.md for high-risk modules (billing, security, compliance)
3. Always apply requirements-best-practices.md

## Integration with Other Documentation

Requirements documentation should link to:
- **Design Documentation**: Requirements Traceability Matrix maps requirements to design components
- **Test Documentation**: Each requirement should have associated test cases
- **User Documentation**: User-facing requirements inform user guide content

## Quality Checklist

Every requirements document should have:
- [ ] Unique identifiers for each requirement (FR-001, NFR-001)
- [ ] Clear, testable acceptance criteria
- [ ] Priority assigned (MoSCoW: Must/Should/Could/Won't)
- [ ] Traceability links (requirement → design → test)
- [ ] Stakeholder approval sign-off
- [ ] Version history

## Tools and Formats

- **Primary Format**: Markdown (for version control and docs-as-code)
- **Enterprise Format**: Word (DOCX) generated from markdown
- **Collaboration**: Confluence, Notion, or GitHub/GitLab wikis
- **Visual**: Mermaid or PlantUML for context diagrams

## Examples

See `examples/greenfield/` for complete requirements document examples:
- `project-atlas-prd.md` - Modern PRD example
- `project-atlas-srs.md` - Formal SRS example for billing module
