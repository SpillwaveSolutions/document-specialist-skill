# Code-to-Docs: When to Use Brownfield Documentation

---
TOKEN_BUDGET: 150
TIER: 3
LOAD_TRIGGER: On-demand when reverse-engineering documentation from code
DEPENDENCIES: None
---

## 9.1 When to Use Brownfield Documentation

### Use Cases

**1. Inherited Legacy Codebase**
- No documentation exists
- Original developers have left
- Need to understand before making changes

**2. Open-Source Project Adoption**
- Evaluating whether to use a library
- Contributing to a project
- Onboarding team to new dependency

**3. Onboarding New Team Members**
- Reduce ramp-up time from weeks to days
- Provide high-level architecture overview
- Document undocumented tribal knowledge

**4. Compliance Audit Requirements**
- SOC 2, HIPAA, PCI-DSS audits
- Need formal documentation of existing systems
- Demonstrate security controls

**5. Architecture Review**
- Planning a major refactoring
- Identifying technical debt
- Evaluating scalability

**6. M&A Due Diligence**
- Acquiring a company or product
- Need to understand what you're buying
- Assess code quality and maintainability

---

### When NOT to Use

**Don't use brownfield documentation when:**
- Code is already well-documented
- Building a greenfield project (use templates instead)
- Code is being rewritten (document the new design)
- Time is better spent refactoring than documenting

---

### ROI Calculation

**Investment**: 2-4 hours to generate brownfield documentation

**Return**:
- Onboarding time reduced by 50% (weeks → days)
- Fewer incidents due to better understanding
- Faster feature development (less time spelunking code)
- Reduced bus factor (knowledge not trapped in one person's head)

---

**End of When to Use Brownfield Documentation Guide**
