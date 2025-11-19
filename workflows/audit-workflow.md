# Documentation Audit Workflow

---
TOKEN_BUDGET: 1000
TIER: 3
LOAD_TRIGGER: Intent = AUDIT (review existing documentation)
DEPENDENCIES: SKILL.md, reference/quality-checklist.md
---

## Overview

This workflow guides the audit and improvement of existing documentation. Use this when the user wants to review documentation for quality, completeness, and adherence to best practices.

**Audit Types:**
- Requirements documents (SRS, PRD)
- Design documents (SDD, arc42)
- API documentation (OpenAPI, REST, GraphQL)
- User documentation (guides, KB articles)
- Deployment documentation

**Token Budget**: This workflow consumes ~1,000 tokens. Load only when intent is AUDIT.

---

## Workflow Steps

### Step 1: Identify Document Type

Read the document and classify:

| Document Indicators | Type | Quality Checklist |
|---------------------|------|-------------------|
| "Requirements Specification", "FR-", "NFR-" | SRS | reference/quality-checklist.md (Requirements section) |
| "Product Requirements", "User Stories", "Success Metrics" | PRD | reference/quality-checklist.md (Requirements section) |
| "Software Design", "arc42", "Architecture" | SDD/arc42 | reference/quality-checklist.md (Design section) |
| "openapi:", "paths:", "components:" | OpenAPI | reference/quality-checklist.md (API section) |
| "Step-by-step", "How to", "User Guide" | User Docs | reference/quality-checklist.md (User Docs section) |

### Step 2: Run Quality Checklist

#### All Documents Checklist

- [ ] **Clear, descriptive title**: Does the document have a meaningful title?
- [ ] **Version number and date**: Is version/date present and current?
- [ ] **Author/owner identified**: Is ownership clear?
- [ ] **Table of contents**: (if > 3 pages) Is TOC present and accurate?
- [ ] **Introduction**: Does it explain purpose and scope?
- [ ] **Glossary of terms**: Are technical terms defined?
- [ ] **Consistent formatting**: Headings, bullets, tables consistent?
- [ ] **No spelling/grammar errors**: Run grammar check
- [ ] **All acronyms defined**: First use includes definition?

#### Requirements Documents (SRS/PRD) Checklist

- [ ] **Unique IDs**: All requirements have FR-XXX-001 format?
- [ ] **Testable**: Each requirement is measurable/verifiable?
- [ ] **Acceptance criteria**: Given-When-Then format provided?
- [ ] **Non-functional requirements**: Performance, security, scalability included?
- [ ] **Priorities assigned**: MoSCoW or P0/P1/P2/P3?
- [ ] **Requirements traceability matrix**: Cross-reference provided?
- [ ] **Realistic**: Requirements achievable with current technology?

#### Design Documents (SDD/arc42) Checklist

- [ ] **Architecture overview**: High-level design with rationale?
- [ ] **Component descriptions**: All components documented?
- [ ] **Data model**: ER diagram or schema provided?
- [ ] **Interface specifications**: APIs, protocols defined?
- [ ] **Deployment architecture**: Infrastructure documented?
- [ ] **Security considerations**: Auth, encryption, compliance?
- [ ] **ADR (Architecture Decision Records)**: Key decisions documented?

#### API Documentation (OpenAPI) Checklist

- [ ] **Base URL**: Production, staging URLs defined?
- [ ] **Versioning**: API version strategy documented?
- [ ] **Authentication**: Auth method specified?
- [ ] **All endpoints documented**: Every path has description?
- [ ] **Request/response schemas**: $ref or inline schemas?
- [ ] **Error responses**: 4xx, 5xx responses documented?
- [ ] **Rate limiting**: Policies specified?
- [ ] **Code examples**: Request/response examples provided?

#### User Documentation Checklist

- [ ] **Step-by-step instructions**: Clear workflow?
- [ ] **Screenshots or diagrams**: Visual aids provided?
- [ ] **Troubleshooting section**: Common issues addressed?
- [ ] **FAQ**: Frequently asked questions answered?
- [ ] **Contact information**: Support email/link provided?
- [ ] **Searchable format**: Organized for easy navigation?

### Step 3: Identify Gaps and Issues

**Gap Analysis:**

1. **Missing Sections**: Compare against template
   - Example: "SRS is missing Requirements Traceability Matrix (Section 6)"

2. **Incomplete Sections**: Check section depth
   - Example: "Non-functional requirements only covers performance, missing security and scalability"

3. **Outdated Content**: Check dates and version references
   - Example: "References Spring Boot 2.5, but project uses 3.1"

4. **Inconsistent Format**: Check consistency
   - Example: "Some requirements use Given-When-Then, others don't"

5. **Missing Diagrams**: Visual documentation gaps
   - Example: "No system context diagram for architecture overview"

**Issue Classification:**

| Severity | Description | Example |
|----------|-------------|---------|
| **Critical** | Missing mandatory section or incorrect information | "OpenAPI spec missing authentication, but API requires auth" |
| **High** | Incomplete coverage of important topic | "Security section only 2 sentences, should be 2 pages" |
| **Medium** | Formatting, consistency, or clarity issues | "Inconsistent heading levels, some requirements lack IDs" |
| **Low** | Minor improvements, recommendations | "Add code examples in Python in addition to JavaScript" |

### Step 4: Generate Audit Report

**Report Structure:**

```markdown
# Documentation Audit Report

**Document**: [Document name and path]
**Type**: [SRS|PRD|SDD|OpenAPI|User Guide]
**Audit Date**: [Current date]
**Audited By**: Claude Code - Documentation Specialist

---

## Executive Summary

**Overall Quality**: [Excellent|Good|Fair|Poor]
**Completeness**: [95%|80%|60%|40%]
**Recommendation**: [Approve|Minor Revisions|Major Revisions|Rewrite]

**Key Findings**:
- [Finding 1: Critical issue or major gap]
- [Finding 2: Significant improvement opportunity]
- [Finding 3: Strength or best practice observed]

---

## Checklist Results

### All Documents
✅ Title: Clear and descriptive
✅ Version: 1.0.0, dated 2025-01-10
❌ Author: Missing (add author/owner)
✅ Table of Contents: Present and accurate
❌ Introduction: Missing purpose statement
⚠️  Glossary: Partial (only 3 of 15 technical terms defined)
✅ Formatting: Consistent
✅ Grammar: No errors detected
❌ Acronyms: JWT, API, SLA not defined on first use

### [Document Type Specific]
[... specific checklist results ...]

---

## Detailed Findings

### Critical Issues (Must Fix)

**1. Missing Authentication Documentation**
- **Location**: OpenAPI spec
- **Issue**: No `securitySchemes` defined, but endpoints require auth
- **Impact**: Developers cannot integrate without auth details
- **Recommendation**: Add JWT Bearer authentication to `components.securitySchemes`

### High Priority Issues (Should Fix)

**2. Incomplete Non-Functional Requirements**
- **Location**: Section 4 (Non-Functional Requirements)
- **Issue**: Only covers performance, missing security, scalability, usability
- **Impact**: Critical requirements not specified
- **Recommendation**: Add NFR sections for:
  - Security (NFR-SEC-001 through NFR-SEC-005)
  - Scalability (NFR-SCALE-001 through NFR-SCALE-003)
  - Usability (NFR-USABILITY-001 through NFR-USABILITY-002)

### Medium Priority Issues (Could Fix)

**3. Inconsistent Requirements Format**
- **Location**: Section 3 (System Features)
- **Issue**: Requirements 3.1-3.5 use Given-When-Then, 3.6-3.10 don't
- **Impact**: Reduces readability and testability
- **Recommendation**: Apply Given-When-Then format to all requirements

### Low Priority Suggestions (Nice to Have)

**4. Add Code Examples**
- **Location**: API documentation
- **Issue**: No request/response examples
- **Impact**: Minor - developers can infer from schema
- **Recommendation**: Add curl and Python examples for each endpoint

---

## Improvement Recommendations

### Quick Wins (< 1 hour)
1. Add author name to front matter
2. Define all acronyms on first use
3. Complete glossary with missing terms
4. Fix broken internal links

### Short Term (1-4 hours)
1. Add missing NFR sections (security, scalability)
2. Standardize requirements format (all Given-When-Then)
3. Add system context diagram
4. Complete requirements traceability matrix

### Long Term (1-2 days)
1. Expand architecture section with component diagrams
2. Add sequence diagrams for key workflows
3. Create comprehensive API examples
4. Add user acceptance test scenarios

---

## Best Practices Observed

- ✅ Excellent use of unique requirement IDs (FR-XXX-001 format)
- ✅ Clear acceptance criteria for most requirements
- ✅ Professional formatting and structure
- ✅ Good use of tables for structured data

---

## Compliance Check

- [ ] IEEE 830-1998 (SRS): 80% compliant (missing traceability matrix)
- [ ] OpenAPI 3.0 Specification: 75% compliant (missing security schemes)
- [ ] WCAG 2.1 AA (User Docs): Not assessed (web-only guideline)

---

## Next Steps

1. **Immediate**: Fix critical issues (#1)
2. **This Week**: Address high priority issues (#2)
3. **This Month**: Resolve medium priority issues (#3)
4. **As Time Permits**: Implement low priority suggestions (#4)

**Estimated Effort**: 6-8 hours to address all critical and high priority issues

---

## Conclusion

The [document name] is [quality assessment]. With [number] critical and [number] high priority issues addressed, this document will meet [standard/requirement].

**Final Recommendation**: [Approve with minor revisions|Requires major revisions before approval|Defer approval until critical issues resolved]

---

**End of Audit Report**
```

### Step 5: Offer Improvement Actions

After generating the audit report, offer:

```
I've completed the audit of [document name]. The document is [quality assessment].

I found:
- [X] critical issues (must fix)
- [Y] high priority issues (should fix)
- [Z] medium priority issues (could fix)

Would you like me to:
1. Automatically fix all critical and high priority issues?
2. Generate a detailed improvement plan with code examples?
3. Create missing diagrams?
4. Update the document to the latest template version?
5. Generate a compliance checklist for [standard]?
```

### Step 6: Automatic Fixes (If User Approves)

If user approves automatic fixes:

**For Missing Sections:**
- Add skeleton sections with placeholders
- Use templates to populate structure

**For Formatting Issues:**
- Standardize heading levels
- Add missing IDs
- Fix bullet point consistency

**For Missing Diagrams:**
- Invoke mermaid-architect or plantuml
- Generate based on existing content

**For Glossary:**
- Extract all technical terms
- Generate definitions
- Add to glossary section

---

## Example: Audit OpenAPI Specification

**User Request:**
```
Audit my OpenAPI specification at docs/api/customer-api.yaml
```

**Workflow Execution:**

### Step 1: Identify Document Type
```
Read: docs/api/customer-api.yaml
Detected: openapi: 3.0.3
Type: OpenAPI Specification
```

### Step 2: Run Quality Checklist

**All Documents:**
- ✅ Title: "Customer Management API"
- ✅ Version: "1.2.0"
- ❌ Author: Missing
- N/A TOC (YAML format)
- ✅ Description: Present
- ⚠️ Glossary: Partial (in description)

**API Documentation:**
- ✅ Base URL: https://api.example.com/v1
- ✅ Versioning: /v1 in path
- ❌ Authentication: Missing securitySchemes
- ✅ Endpoints: All documented
- ⚠️ Schemas: Some inline, should use $ref
- ❌ Error responses: Only 200/400, missing 401/403/404
- ❌ Rate limiting: Not documented
- ⚠️ Examples: Only 2 of 10 endpoints have examples

### Step 3: Identify Gaps

**Critical:**
1. Missing `components.securitySchemes` (endpoints show they require auth)

**High:**
2. Missing error responses (401, 403, 404, 500)
3. No rate limiting documentation

**Medium:**
4. Inconsistent schema references (mix of $ref and inline)
5. Missing examples for 8 endpoints

**Low:**
6. No code examples (curl, Python, JavaScript)

### Step 4: Generate Audit Report

```markdown
# OpenAPI Specification Audit Report

**Document**: docs/api/customer-api.yaml
**Type**: OpenAPI 3.0.3
**Audit Date**: 2025-01-13
**Audited By**: Claude Code - Documentation Specialist

## Executive Summary

**Overall Quality**: Good
**Completeness**: 75%
**Recommendation**: Minor Revisions

**Key Findings**:
- Missing security schemes definition (critical)
- Incomplete error response coverage (high)
- Good endpoint documentation but inconsistent schema usage (medium)

[... full audit report ...]
```

### Step 5-6: Offer Improvements

```
I've completed the audit. The OpenAPI specification is GOOD quality but needs minor revisions.

Issues found:
- 1 critical issue (missing security schemes)
- 2 high priority issues (error responses, rate limiting)
- 2 medium priority issues (schema consistency, examples)

Would you like me to:
1. Add missing securitySchemes section for JWT authentication?
2. Add comprehensive error response definitions?
3. Standardize all schemas to use $ref?
4. Generate request/response examples for all endpoints?
5. Add rate limiting documentation?
```

---

## Quality Standards Reference

For detailed quality criteria, refer to:

- **Requirements Quality**: `reference/02-requirements.md`
- **Design Quality**: `reference/03-design.md`
- **API Quality**: `reference/05-api-docs.md`
- **User Docs Quality**: `reference/07-user-docs.md`
- **Complete Checklist**: `reference/quality-checklist.md`

**Do NOT load unless conducting complex audits requiring detailed guidance.**

---

**End of Audit Workflow Guide**
