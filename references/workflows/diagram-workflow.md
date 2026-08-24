# Diagram Generation Workflow

---
TOKEN_BUDGET: 380
TIER: 2
LOAD_TRIGGER: Intent = DIAGRAM
DEPENDENCIES: SKILL.md
---

## Overview

Generate visual documentation with `design-doc-mermaid` and `plantuml`.
Do not invent a third diagram skill name.

## Workflow Steps

### Step 1: Identify Diagram Type

| Keywords | Diagram | Tool |
|----------|---------|------|
| "C4 context", "system overview" | C4 Context | design-doc-mermaid |
| "C4 container", "services" | C4 Container | design-doc-mermaid |
| "C4 component", "modules" | C4 Component | design-doc-mermaid |
| "flowchart" | Flowchart | design-doc-mermaid |
| "sequence", "flow" (GitHub wiki) | Sequence | design-doc-mermaid |
| "sequence" (UML depth / image export) | Sequence | plantuml |
| "ER", "database", "entities" | ER Diagram | plantuml |
| "state", "lifecycle" | State Machine | plantuml |
| "activity", "process" | Activity | plantuml or design-doc-mermaid |
| "class", "inheritance" | Class | plantuml |

GitHub Flavored Markdown and GitHub wiki render Mermaid. They do not render PlantUML source. When the target is `wiki_ticket_sdd` `docs/designs/`, put Mermaid in the Markdown. Add PlantUML only as a `.puml` file plus a PNG/SVG link.

### Step 2: Gather Content

**C4 Diagrams**: System name, actors, containers, relationships
**Sequence**: Participants, ordered steps from real call sites
**ER**: Entities, attributes, relationships
**State Machine**: Entity, states, transitions

Derive nodes from code and config. Cap node count. Write "+N more" instead of silent truncation.

### Step 3: Invoke Skill

**Mermaid (`design-doc-mermaid`)**:
```
Task: Generate [C4 level | flowchart | sequence] diagram
System: [name]
Elements: [list from repo]
Relationships: [list from repo]
Output: fenced mermaid block in the host Markdown
Also save: docs/diagrams/[filename].mmd
Validate: scripts/resilient_diagram.py or mmdc
```

**UML (`plantuml`)**:
```
Task: Generate [type] diagram
Elements: [entities/participants/states]
Relationships: [connections]
Output: docs/diagrams/[filename].puml
Also render: PNG or SVG and link it from the Markdown
```

### Step 4: Present Rendering Options

```
Generated [diagram type]: [path]

Options:
1. Keep Mermaid inline for GitHub / wiki
2. Render PlantUML to PNG/SVG
3. Generate related diagrams
4. Embed in the architecture doc or code walkthrough
```

## Quick Reference

| Show... | Use | Tool |
|---------|-----|------|
| External dependencies | C4 Context | design-doc-mermaid |
| Microservices/DBs | C4 Container | design-doc-mermaid |
| Internal modules | C4 Component | design-doc-mermaid |
| API call flow on GitHub | Sequence | design-doc-mermaid |
| API call flow as UML image | Sequence | plantuml |
| Database schema | ER Diagram | plantuml |
| Entity lifecycle | State Machine | plantuml |
| Business process | Activity | either, prefer mermaid on wiki |

## Selection Guide

**State Machine vs Activity**:
- **State Machine**: Entity states, transitions (Order: Pending to Shipped)
- **Activity**: Process steps, decisions (Registration flow)

For detailed guidance: [04-diagrams-selection.md](../reference/04-diagrams-selection.md)
