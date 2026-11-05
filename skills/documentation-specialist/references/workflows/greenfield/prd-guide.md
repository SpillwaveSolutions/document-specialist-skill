# PRD Generation Guide

---
TOKEN_BUDGET: 250
TIER: 3
LOAD_TRIGGER: CREATE_NEW + PRD document type
DEPENDENCIES: greenfield-workflow.md
---

## PRD Structure (Agile-friendly)

### 1. Objective (0.5 pages)
- Problem statement (2-3 sentences)
- Proposed solution (2-3 sentences)
- Why now? (business driver)

### 2. Success Metrics (1 page)
- **Primary metrics**: 3-5 measurable targets
- **Secondary metrics**: Nice-to-have indicators
- **Counter-metrics**: Watch for negative impact

### 3. User Personas & Use Cases (2-3 pages)
For each persona:
- Who they are
- Goals and pain points
- How this feature helps them

3-5 key use cases with scenarios.

### 4. User Stories & Acceptance Criteria (3-5 pages)
**Epic breakdown** with user stories:

```markdown
**US-001**: As a [role], I want [goal], so that [benefit]

**Acceptance Criteria**:
- **Given** [context]
- **When** [action]
- **Then** [outcome]
```

**MoSCoW prioritization**: Must Have, Should Have, Could Have, Won't Have

### 5. Out of Scope (0.5 pages)
Explicitly state what's NOT included in this release.

### 6. Technical Considerations (1-2 pages)
- Architecture impact
- API changes
- Database changes
- Third-party integrations
- Performance / Security considerations

### 7. Timeline & Milestones (0.5 pages)
Key dates: Kickoff, Design Complete, Alpha, Beta, GA

### 8. Risks & Mitigations (1 page)

| Risk | Impact | Likelihood | Mitigation | Owner |
|------|--------|------------|------------|-------|
| [risk] | High/Med/Low | High/Med/Low | [action] | [name] |

## PRD vs SRS Decision

| Factor | Choose PRD | Choose SRS |
|--------|-----------|------------|
| Methodology | Agile/Scrum | Waterfall/Formal |
| Audience | Product team | Stakeholders, auditors |
| Compliance | Low risk | High risk (regulated) |
| Detail level | User stories | Formal requirements |

## Reference

For agile documentation: [08-agile-process.md](../../reference/08-agile-process.md)

For complete PRD example: [collaboration-prd.md](../../examples/greenfield/collaboration-prd.md)
