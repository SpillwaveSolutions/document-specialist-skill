# Diagrams: C4 Model Hierarchy

---
TOKEN_BUDGET: 200
TIER: 3
LOAD_TRIGGER: On-demand when creating C4 diagrams
DEPENDENCIES: 04-diagrams-selection.md
---

## 4.3 C4 Model Hierarchy

The C4 model provides a hierarchical way to document software architecture by "zooming in" through four levels.

### Level 1: System Context

**Shows**: The system as a single box
**Includes**: External users and systems
**Purpose**: High-level interactions and system boundary

**Audience**: Non-technical stakeholders, executives

**Example**: Task Management System with external OAuth, Email, Analytics

---

### Level 2: Container

**Shows**: "Zooms in" to show deployable units
**Includes**: Web apps, APIs, databases, message queues

**Purpose**: Show the major technology choices and how they communicate

**Audience**: Technical leads, architects

**Example**: Web App (React) → API (Spring Boot) → Database (PostgreSQL)

---

### Level 3: Component

**Shows**: "Zooms in" on a single container
**Includes**: Internal components (controllers, services, repositories)

**Purpose**: Show the internal structure and responsibilities

**Audience**: Developers working on that container

**Example**: Inside API container: TaskController, TaskService, TaskRepository

---

### Level 4: Code (Optional)

**Shows**: "Zooms in" on a component
**Includes**: Class diagrams or UML

**Purpose**: Detailed implementation structure

**Audience**: Developers implementing that component

**Note**: Often auto-generated from code, not manually maintained

---

### When to Create Each Level

| Level | When to Create |
|-------|----------------|
| Level 1: Context | Always (defines system boundary) |
| Level 2: Container | For all systems (shows architecture) |
| Level 3: Component | For complex containers |
| Level 4: Code | Rarely (auto-generate or skip) |

### Integration with arc42

- C4 Level 1 → arc42 Section 3 (Context and Scope)
- C4 Level 2-3 → arc42 Section 5 (Building Block View)

---

**End of C4 Model Hierarchy Guide**
