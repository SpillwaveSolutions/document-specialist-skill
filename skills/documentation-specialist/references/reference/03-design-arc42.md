# Design: The arc42 Template

---
TOKEN_BUDGET: 280
TIER: 3
LOAD_TRIGGER: On-demand when creating architecture documentation
DEPENDENCIES: None
---

## 3.1 The arc42 Template

arc42 is a practical, modular template for documenting architecture. It provides a 12-section table of contents that answers the most important questions.

### The 12 Sections

1. **Introduction and Goals**: Key requirements, stakeholders, top quality goals
2. **Constraints**: Non-negotiable business, technical, or legal decisions
3. **Context and Scope**: System boundaries and external interfaces
4. **Solution Strategy**: High-level design choices and rationale
5. **Building Block View**: Static decomposition into modules/components
6. **Runtime View**: Dynamic behavior for key use cases
7. **Deployment View**: Physical/cloud infrastructure
8. **Crosscutting Concepts**: Logging, error handling, security patterns
9. **Architectural Decisions**: ADRs (what, why, alternatives, trade-offs)
10. **Quality Requirements**: Detailed quality scenarios
11. **Risks and Technical Debt**: Known issues and compromises
12. **Glossary**: Authoritative term definitions

### Default files

| Document | Template | Output |
|----------|----------|--------|
| Full SDD | [templates/markdown/DESIGN_DOC.md](../templates/markdown/DESIGN_DOC.md) | `DESIGN_DOC.md` |
| Short C4 architecture | [templates/markdown/architecture.md](../templates/markdown/architecture.md) | `docs/architecture.md` |
| Workflow | [workflows/design-workflow.md](../workflows/design-workflow.md) | Load with intent DESIGN |

UI screens use PlantUML Salt. See [examples/greenfield/ui-wireframes.md](../examples/greenfield/ui-wireframes.md).

### Integration with C4

arc42 sections map naturally to C4 diagrams:

| arc42 Section | C4 Diagram Level |
|---------------|------------------|
| Section 3: Context and Scope | C4 Level 1: System Context |
| Section 5: Building Block View | C4 Level 2: Container, Level 3: Component |
| Section 6: Runtime View | Sequence diagrams, Activity diagrams |
| Section 7: Deployment View | Deployment diagrams |

Use Mermaid `flowchart TD` for C4-style boxes on GitHub wiki. Fall back from experimental `C4Context` if the wiki fails to render it.

### When to Use arc42

**Use arc42 when:**
- Building complex systems requiring comprehensive architecture docs
- Working in regulated industries (finance, healthcare)
- Onboarding new architects or teams
- Conducting architecture reviews

**Skip full arc42 when:**
- Building simple CRUD applications
- Creating proof-of-concept or MVPs
- Working on small microservices (use the short architecture template instead)

---

**End of arc42 Template Guide**
