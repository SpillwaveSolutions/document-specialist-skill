# Requirements: Traceability and Context

---
TOKEN_BUDGET: 200
TIER: 3
LOAD_TRIGGER: On-demand when creating traceability matrices or system context diagrams
DEPENDENCIES: 02-requirements-writing.md
---

## 2.3 Requirements Traceability

Every requirement should link to:
- **Source**: User need or business goal
- **Design**: Component that implements it
- **Test**: Test case that verifies it

### Requirements Traceability Matrix

| Req ID | Description | Design Component | Test Case | Priority | Status |
|--------|-------------|------------------|-----------|----------|--------|
| FR-001 | User login | AuthController | TC-001 | Must | ✅ Done |
| FR-002 | Create task | TaskService | TC-005 | Must | ⏳ In Progress |
| NFR-001 | Response < 500ms | Redis cache | TC-050 | Should | 📋 Planned |

## 2.4 System Context Diagrams

A **System Context Diagram** (C4 Level 1 or DFD Level 0) defines the system boundary:

```mermaid
C4Context
  title System Context: Task Management Platform

  Person(user, "Team Member", "Uses the platform to manage tasks")
  Person(admin, "Admin", "Configures the system")

  System(taskSystem, "Task Management System", "Organizes tasks, assignments, and deadlines")

  System_Ext(googleAuth, "Google OAuth", "Authenticates users")
  System_Ext(email, "Email Service", "Sends notifications")
  System_Ext(analytics, "Analytics Platform", "Tracks usage metrics")

  Rel(user, taskSystem, "Uses")
  Rel(admin, taskSystem, "Configures")
  Rel(taskSystem, googleAuth, "Authenticates with")
  Rel(taskSystem, email, "Sends emails via")
  Rel(taskSystem, analytics, "Sends events to")
```

**Purpose**: Shows what's inside vs. outside the system, clarifying scope and dependencies.

---

**End of Requirements Traceability Guide**
