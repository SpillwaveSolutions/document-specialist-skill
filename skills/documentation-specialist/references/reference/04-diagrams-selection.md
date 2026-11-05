# Diagram playbook

Use this with `references/workflows/diagram-workflow.md`. Default tool is Mermaid. PlantUML is leftover types and images.

Cap a figure at about 16 nodes. Prefer several small diagrams over one dense one.

---

## Chooser

| You need to show | Diagram | Tool |
|------------------|---------|------|
| Who talks to the system | Context flowchart | Mermaid |
| Deployable pieces | Container flowchart | Mermaid |
| Modules inside a container | Component flowchart or class | Mermaid |
| Time-ordered calls | Sequence | Mermaid |
| Branching process | Flowchart | Mermaid |
| Lifecycle | State | Mermaid |
| Tables and keys | ER | Mermaid |
| Types and inheritance | Class | Mermaid |
| Nested ideas | Mind map | Mermaid |
| Schedule | Gantt | Mermaid |
| Shall-statements | Requirement | Mermaid |
| User feeling over time | Journey | Mermaid |
| Wire format | Packet | Mermaid |
| Actors and goals | Use case | PlantUML |
| UI sketch | Salt wireframe | PlantUML |
| Clock / waveform | Timing | PlantUML |
| Enterprise layers | ArchiMate | PlantUML |
| Rack / network | nwdiag | PlantUML |
| Breakdown structure | WBS | PlantUML |

If GitHub fails to render C4, `architecture-beta`, or `block-beta`, rewrite as `flowchart TD`. Do not switch to PlantUML for that reason on wiki.

---

## Flowchart

Process, decisions, or C4-style boxes.

```mermaid
flowchart TD
  start([Start]) --> ingest[Read request]
  ingest --> ok{Valid?}
  ok -->|yes| save[Write DESIGN_DOC.md]
  ok -->|no| ask[Ask one clarifying question]
  save --> done([Done])
  ask --> done
```

Direction: `TD` for documents, `LR` for deployment. Multi-line labels use `<br>`.

---

## Sequence

Keep five participants or fewer. Use subsystems, not every class.

```mermaid
sequenceDiagram
  participant A as Architect
  participant H as Host
  participant S as Skill
  A->>H: Write SDD
  H->>S: Load design-workflow
  S-->>H: DESIGN_DOC.md
  H-->>A: Path
```

---

## State

```mermaid
stateDiagram-v2
  [*] --> Draft
  Draft --> InReview: PR opened
  InReview --> Accepted: LGTM
  InReview --> Draft: changes requested
  Accepted --> [*]
```

---

## Class

```mermaid
classDiagram
  class DocumentSpecialist {
    +classifyIntent()
    +loadWorkflow()
    +writeDesignDoc()
  }
  class Workflow {
    +steps
  }
  class Template {
    +placeholders
  }
  DocumentSpecialist --> Workflow
  DocumentSpecialist --> Template
```

---

## ER

```mermaid
erDiagram
  PROJECT ||--o{ DOCUMENT : has
  DOCUMENT ||--o{ FIGURE : includes
  DOCUMENT {
    string path PK
    string kind
  }
  FIGURE {
    string id PK
    string tool
  }
```

---

## User journey

```mermaid
journey
  title Architect requests an SDD
  section Ask
    Name the system: 4: Architect
    Point at the repo: 5: Architect
  section Generate
    Classify intent: 4: Skill
    Draw figures: 3: Skill
  section Review
    Read DESIGN_DOC.md: 5: Architect
    Request edits: 3: Architect
```

---

## Mind map

```mermaid
mindmap
  root((Figures))
    Behavior
      Sequence
      State
      Flowchart
    Structure
      Class
      ER
      Context
    Leftover
      Use case
      Salt
      Timing
```

---

## Gantt

```mermaid
gantt
  title SDD first cut
  dateFormat YYYY-MM-DD
  section Draft
  Context and goals     :a1, 2026-09-01, 2d
  Building blocks       :a2, after a1, 2d
  section Figures
  Sequence and ER       :a3, after a2, 2d
  Review                :a4, after a3, 1d
```

---

## Requirement

```mermaid
requirementDiagram
  requirement design_doc {
    id: "FR-SDD-001"
    text: "The skill shall emit DESIGN_DOC.md"
    risk: High
    verifymethod: Inspection
  }
  element template {
    type: Document
  }
  template - satisfies -> design_doc
```

---

## Packet

```mermaid
packet-beta
0-15: "Skill id"
16-31: "Intent"
32-63: "Workflow"
64-95: "Template"
96-127: "Voice pack"
```

---

## Salt wireframe

Use PlantUML Salt for every UI, mock, or screen. Mermaid has no wireframe type. One screen per diagram.

```puml
@startuml
salt
{
  {* File | Edit | View }
  {+
    {/ <b>Library | DESIGN_DOC | Wireframes }
    .
    Find owner
    { Last name | "Davis" | [ Find Owner ] }
    [ Add Owner ]
    .
    {#
      Last name | First name | Pets
      Davis     | Betty      | Basil
      Davis     | Harold     | Iggy
    }
  }
}
@enduml
```

Copy labels from the real product. Full Folio, Northstar, and Pet Clinic screens are in the UI wireframes example.

---

## PlantUML leftover: use case

Render this to PNG or SVG. Do not leave it as the only view on GitHub wiki.

```puml
@startuml
left to right direction
actor Architect
rectangle "Document Specialist" {
  usecase "Write SDD" as UC1
  usecase "Write architecture" as UC2
  usecase "Extract from code" as UC3
}
Architect --> UC1
Architect --> UC2
Architect --> UC3
@enduml
```

---

## Formatting notes

- Set direction explicitly (`TD`, `LR`).
- Quote labels that contain punctuation.
- Style with `classDef` when you need contrast. Prefer theme variables over one-off hex in every node.
- Break a crowded figure into two linked diagrams rather than shrinking fonts.
- For wiki: keep the `mermaid` fence. For Confluence, Notion, Word, or PDF: render PNG or SVG and upload the image.
