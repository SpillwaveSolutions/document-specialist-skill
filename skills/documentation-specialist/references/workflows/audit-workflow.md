# Documentation Audit Workflow

---
TOKEN_BUDGET: 350
TIER: 2
LOAD_TRIGGER: Intent = AUDIT
DEPENDENCIES: SKILL.md
---

## Overview

Review existing documentation for quality, completeness, and best practices.

**Audit Types**: SRS, PRD, SDD, OpenAPI, User Documentation

## Workflow Steps

### Step 1: Identify Document Type

| Indicators | Type | Focus |
|------------|------|-------|
| "FR-", "NFR-", "Requirements Specification" | SRS | Formal requirements |
| "User Stories", "Success Metrics" | PRD | Agile requirements |
| "arc42", "Architecture" | SDD | Design documentation |
| "openapi:", "paths:" | OpenAPI | API specification |
| "How to", "Step-by-step" | User Docs | End-user guides |

### Step 2: Run Quality Checklist

**All Documents**:
- [ ] Clear title, version, date
- [ ] Author/owner identified
- [ ] Table of contents (if > 3 pages)
- [ ] Introduction with purpose/scope
- [ ] Glossary of terms
- [ ] Consistent formatting

**Requirements (SRS/PRD)**:
- [ ] Unique IDs (FR-XXX-001)
- [ ] Testable criteria (Given-When-Then)
- [ ] NFRs included (performance, security)
- [ ] Priorities assigned

**API (OpenAPI)**:
- [ ] Base URL defined
- [ ] Authentication documented
- [ ] All endpoints described
- [ ] Error responses (4xx, 5xx)
- [ ] Request/response examples

### Step 3: Classify Issues

| Severity | Description |
|----------|-------------|
| **Critical** | Missing mandatory section, incorrect information |
| **High** | Incomplete coverage of important topic |
| **Medium** | Formatting, consistency issues |
| **Low** | Minor improvements, recommendations |

### Step 4: Generate Audit Report

```markdown
# Documentation Audit Report

**Document**: [name and path]
**Type**: [SRS|PRD|SDD|OpenAPI]
**Audit Date**: [date]

## Executive Summary
- **Quality**: [Excellent|Good|Fair|Poor]
- **Completeness**: [percentage]
- **Recommendation**: [Approve|Minor Revisions|Major Revisions]

## Critical Issues
[List with location, issue, impact, recommendation]

## High Priority Issues
[List with details]

## Quick Wins (< 1 hour)
[List of easy fixes]

## Next Steps
1. Fix critical issues
2. Address high priority items
3. Implement improvements
```

### Step 5: Present Fix Options

Present summary and options to user:
```
Found [X] critical, [Y] high priority, [Z] medium priority issues.

Options:
1. Automatically fix critical and high priority issues
2. Generate missing diagrams
3. Complete the glossary
4. Standardize formatting
```

## Quality Standards

For detailed criteria: [10-quality-checklist.md](../reference/10-quality-checklist.md)
