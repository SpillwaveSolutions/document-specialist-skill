# Requirements: Writing Effective Requirements

---
TOKEN_BUDGET: 250
TIER: 3
LOAD_TRIGGER: On-demand when writing requirements (SRS or PRD)
DEPENDENCIES: 02-requirements-srs-vs-prd.md
---

## 2.2 Writing Effective Requirements

### Atomic Requirements

**Characteristics:**
- Each requirement has a unique ID (FR-001, NFR-001)
- One requirement per statement (no "and" clauses)
- Testable and verifiable
- Implementation-neutral (what, not how)

**Example:**
❌ Bad: "The system should be fast and easy to use"
✅ Good: "FR-042: The search API shall return results in under 500ms for 95% of queries"

### User Story Format

```
As a [user type],
I want to [goal],
so that [benefit].
```

**Example:**
```
As a project manager,
I want to assign tasks to team members,
so that work is distributed and tracked.
```

### Acceptance Criteria (Given-When-Then)

```
Given a user is logged in,
When they click "Create Task",
Then a new task form should appear with fields: title, description, due date.
```

### Requirements Quality Checklist

- [ ] **Unique ID**: FR-XXX-001 or NFR-XXX-001 format
- [ ] **Testable**: Can be verified through testing
- [ ] **Atomic**: One requirement, no "and" clauses
- [ ] **Clear**: No ambiguous terms like "fast", "easy", "scalable"
- [ ] **Necessary**: Directly supports a business goal
- [ ] **Traceable**: Linked to source need and test case

---

**End of Writing Effective Requirements Guide**
