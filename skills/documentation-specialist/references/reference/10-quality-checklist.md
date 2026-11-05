# Quality: Documentation Quality Checklist

---
TOKEN_BUDGET: 220
TIER: 3
LOAD_TRIGGER: On-demand when auditing documentation quality
DEPENDENCIES: None
---

## 10.1 Documentation Quality Checklist

### All Documents

- [ ] **Clear, descriptive title**
  - Tells reader what the doc is about
  - Specific, not generic

- [ ] **Version number and date**
  - Semantic versioning (v1.0.0, v1.1.0)
  - Last updated date (YYYY-MM-DD format)

- [ ] **Author/owner identified**
  - Who wrote this?
  - Who maintains it?
  - Contact for questions

- [ ] **Table of contents** (if > 3 pages)
  - Hyperlinked headings
  - Helps navigation

- [ ] **Introduction** (purpose, scope, audience)
  - What is this document?
  - Who is it for?
  - What's in scope / out of scope?

- [ ] **Glossary of terms**
  - Define acronyms and jargon
  - Consistent terminology

- [ ] **Consistent formatting**
  - Same heading styles
  - Same code block styles
  - Same list formatting

- [ ] **No spelling or grammar errors**
  - Use spell checker
  - Proofread before publishing

- [ ] **All acronyms defined on first use**
  - Example: "API (Application Programming Interface)"

---

### Technical Documents (SDD, API Docs, Deployment)

- [ ] **Code examples are tested**
  - Examples actually work
  - Not pseudo-code

- [ ] **Diagrams are up-to-date**
  - Match current architecture
  - Source files available for editing

- [ ] **Links are not broken**
  - Test all hyperlinks
  - Use relative paths for internal links

- [ ] **Version-specific** (not "latest")
  - Document version 2.1.0, not "the current version"
  - Warn if documentation is for older version

---

### Requirements Documents (SRS, PRD)

- [ ] **Unique IDs**: All requirements have FR-XXX-001 format
- [ ] **Testable**: Each requirement is measurable/verifiable
- [ ] **Atomic**: One requirement per ID
- [ ] **Acceptance criteria**: Given-When-Then format provided
- [ ] **Priority**: Must-have, Should-have, Nice-to-have
- [ ] **Traceability**: Linked to design and tests

---

### API Documentation (OpenAPI)

- [ ] **Base URL**: Production, staging URLs defined
- [ ] **Authentication**: Auth method specified
- [ ] **All endpoints documented**
- [ ] **Request/response examples**
- [ ] **Error codes**: All status codes explained
- [ ] **Rate limits**: Documented

---

### User Documentation (KB Articles)

- [ ] **Title is goal-oriented**: "How to..." or "What is..."
- [ ] **Screenshots**: Annotated, current UI
- [ ] **Step-by-step**: Numbered instructions
- [ ] **Expected outcome**: What happens after following steps
- [ ] **Troubleshooting**: Common issues addressed

---

**End of Documentation Quality Checklist**
