# Requirements: SRS vs. PRD

---
TOKEN_BUDGET: 200
TIER: 3
LOAD_TRIGGER: On-demand when creating requirements documentation
DEPENDENCIES: None
---

## 2.1 From Formal to Agile: SRS vs. PRD

### Software Requirements Specification (SRS)

**Characteristics:**
- Formal, comprehensive "playbook"
- IEEE-standard based
- Best for: High-assurance environments (medical, finance, government)
- Structure: Introduction → Functional Requirements → Non-Functional Requirements → Use Cases → Traceability Matrix

### Product Requirements Document (PRD)

**Characteristics:**
- Modern, collaborative, living document
- Agile-friendly
- Best for: Product development, startups, SaaS
- Structure: Objective → Success Metrics → User Stories → Out of Scope

### Risk-Based Approach

Use PRDs for most features, but escalate to formal SRS for high-risk modules (billing, security, compliance).

**Decision Matrix:**

| Risk Level | Criticality | Document Type |
|------------|-------------|---------------|
| Low | Feature enhancement | PRD |
| Medium | New feature | PRD |
| High | Billing, security | SRS |
| Critical | Medical, financial | SRS + Compliance Docs |

---

**End of SRS vs. PRD Guide**
