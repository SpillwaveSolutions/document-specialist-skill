# Architecture document

**System:** `[System name]`  
**Version:** `[0.1.0]`  
**Status:** `[Proposed | Accepted]`  
**Audience:** `[Engineers joining the system]`  
**Voice:** `[STE100 | google-docs-style]`

Short C4-first document. Use this when the user wants context, containers, and a key sequence without the full arc42 SDD. For regulated reviews, write `DESIGN_DOC.md` instead.

---

## Purpose

`[Two or three sentences. What the system does. Who uses it.]`

---

## System context

**In scope:** `[list]`  
**Out of scope:** `[list]`

```mermaid
flowchart TB
  actor([Primary actor])
  sys[System name]
  ext[External system]
  actor --> sys
  sys --> ext
```

---

## Containers

| Container | Tech | Role |
|-----------|------|------|
| `[name]` | `[stack]` | `[role]` |

```mermaid
flowchart LR
  ui[UI] --> api[API]
  api --> db[(Store)]
```

---

## Components

```mermaid
flowchart TB
  subgraph api [API]
    a[Module A]
    b[Module B]
  end
  a --> b
```

---

## Key sequence

Five participants or fewer.

```mermaid
sequenceDiagram
  participant U as User
  participant A as API
  participant D as Store
  U->>A: Request
  A->>D: Query
  D-->>A: Row
  A-->>U: Response
```

---

## Deployment

```mermaid
flowchart LR
  lb[Load balancer] --> svc[Service]
  svc --> db[(Database)]
```

---

## UI wireframes

One Salt diagram per screen. Do not sketch UI in Mermaid.

```puml
@startuml
salt
{
  {+
    [Screen title]
    { Field | "value" }
    { [ Cancel ] | [ Save ] }
  }
}
@enduml
```

## Decisions to read next

- ADR-001: `[title]`

When a change crosses two containers, update this file in the same PR as the code.
