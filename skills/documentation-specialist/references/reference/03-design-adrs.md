# Design: Architecture Decision Records (ADRs)

---
TOKEN_BUDGET: 300
TIER: 3
LOAD_TRIGGER: On-demand when documenting architectural decisions
DEPENDENCIES: 03-design-arc42.md
---

## 3.2 Architecture Decision Records (ADRs)

For every significant architectural decision, document:
- **Context**: What forces are at play?
- **Decision**: What did we decide?
- **Consequences**: What are the trade-offs?

### ADR Template

```markdown
# ADR-001: Choose Microservices over Monolith

## Status
Accepted

## Context
We need to scale different parts of the application independently.
The billing service has strict compliance requirements.
Our team is growing and needs to work on features in parallel.

## Decision
We will use a microservices architecture with separate services for:
- User management
- Task management
- Billing

## Consequences

**Positive:**
- Independent scaling and deployment
- Isolation of high-assurance billing service
- Team autonomy (each team owns a service)
- Technology diversity (use best tool for each service)

**Negative:**
- Increased operational complexity (more services to monitor)
- Network latency between services
- Distributed transactions are harder
- Need for API gateway and service discovery

## Alternatives Considered

**Alternative 1: Monolith**
- Simpler to deploy and monitor
- Rejected because: Cannot scale billing independently, team bottlenecks

**Alternative 2: Modular Monolith**
- Internal modules with clear boundaries
- Rejected because: Still single deployment, cannot isolate billing compliance
```

### Best Practices

1. **Number sequentially**: ADR-001, ADR-002, etc.
2. **Immutable**: Never edit an ADR, supersede with a new one
3. **Status states**: Proposed → Accepted → Deprecated → Superseded
4. **Store with code**: In `/docs/adr/` directory, version controlled
5. **Link to implementation**: Reference code PRs, commits

### When to Write an ADR

Write an ADR for decisions that:
- Are hard to reverse (database choice, cloud provider)
- Have significant cost or performance implications
- Affect multiple teams or services
- Set precedents for future decisions

**Don't write ADRs for**: Library choices, coding style (use linters), minor refactorings

---

**End of ADR Guide**
