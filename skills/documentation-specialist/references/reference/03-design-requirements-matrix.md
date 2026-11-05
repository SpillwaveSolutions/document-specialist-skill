# Design: Requirements Matrix

---
TOKEN_BUDGET: 150
TIER: 3
LOAD_TRIGGER: On-demand when mapping requirements to design components
DEPENDENCIES: 02-requirements-traceability.md, 03-design-arc42.md
---

## 3.3 Requirements Matrix

Link every requirement to its implementation component.

### Design Requirements Matrix

| Requirement | Design Component | Rationale |
|-------------|------------------|-----------|
| FR-001: User login | UserController + AuthService | Implements OAuth2 flow |
| FR-042: Search < 500ms | SearchService with Redis cache | Caching ensures performance target |
| NFR-SEC-001: Encrypt data at rest | DatabaseConfig with TDE | Meets security requirements |
| NFR-SCALE-001: Handle 10K concurrent users | Kubernetes autoscaling | Auto-scales based on load |

### Purpose

**Verification**: Ensures every requirement has an implementation
**Communication**: Bridges requirements and design teams
**Impact Analysis**: Identifies affected components when requirements change

### How to Create

1. Extract all requirements from SRS/PRD
2. Identify the component that implements each requirement
3. Add rationale explaining the design choice
4. Review with both requirements and design teams
5. Update as requirements or design evolves

---

**End of Requirements Matrix Guide**
