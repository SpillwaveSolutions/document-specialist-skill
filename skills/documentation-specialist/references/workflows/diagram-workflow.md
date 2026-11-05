# Diagram Generation Workflow

---
TOKEN_BUDGET: 520
TIER: 2
LOAD_TRIGGER: Intent = DIAGRAM
DEPENDENCIES: SKILL.md
---

## Overview

Default tool is `design-doc-mermaid`. GitHub Flavored Markdown and GitHub
wiki render fenced `mermaid` blocks. They do not render PlantUML source.

Use `plantuml` only when Mermaid cannot do the job easily, or when the
publish target needs a raster image that PlantUML already owns.

## Publish targets

| Target | Mermaid | PlantUML |
|--------|---------|----------|
| GitHub wiki / GFM | Keep the fenced `mermaid` block. It renders. | Never leave a raw `puml` fence as the only view. Render PNG or SVG, commit it under `docs/diagrams/`, link the image, and upload the image with the wiki page. |
| Confluence / Notion / Word / PDF | Render PNG or SVG with `mmdc` or `scripts/resilient_diagram.py`. Upload the image. Do not rely on Confluence to render Mermaid. | Render PNG or SVG. Upload the image. |

## Step 1: Identify diagram type

| Keywords | Diagram | Tool |
|----------|---------|------|
| C4 context, system overview | C4 Context | design-doc-mermaid |
| C4 container, services | C4 Container | design-doc-mermaid |
| C4 component, modules | C4 Component or flowchart | design-doc-mermaid |
| flowchart, process | Flowchart | design-doc-mermaid |
| sequence, call flow | Sequence | design-doc-mermaid |
| class, inheritance | Class (`classDiagram`) | design-doc-mermaid |
| ER, database, entities | ER (`erDiagram`) | design-doc-mermaid |
| state, lifecycle | State (`stateDiagram-v2`) | design-doc-mermaid |
| activity, workflow | Flowchart | design-doc-mermaid |
| component boxes, module graph | Flowchart | design-doc-mermaid |
| deployment, topology (boxes and arrows) | Flowchart | design-doc-mermaid |
| wireframe, mock, UI sketch | Salt wireframe | plantuml |
| use case, actors and goals | Use case | plantuml |
| timing, clock, waveform | Timing | plantuml |
| ArchiMate, enterprise layer | ArchiMate | plantuml |
| network rack, nwdiag | Network | plantuml |
| WBS | WBS | plantuml |
| JSON or YAML tree | JSON/YAML viz | plantuml |

If GitHub fails to render an experimental Mermaid type (C4, `architecture-beta`,
`block-beta`), fall back to `flowchart TD`. Do not switch to PlantUML for that
reason on wiki.

## Step 2: Gather content

Derive nodes from code and config. Cap node count at about 16. Write "+N more"
instead of silent truncation.

**Wireframes**: real screens, labels, and controls. Use PlantUML Salt. Render
an image. Link it. Keep the `.puml` source.

## Step 3: Invoke skill

**Mermaid (`design-doc-mermaid`)**

```
Task: Generate [type] diagram
System: [name]
Elements: [list from repo]
Output: fenced mermaid block in the host Markdown
Also save: docs/diagrams/[filename].mmd
Validate: scripts/resilient_diagram.py or mmdc
Confluence: also render PNG/SVG and upload
```

**PlantUML (`plantuml`) — leftover types and images only**

```
Task: Generate [wireframe | use case | timing | ArchiMate | network | WBS]
Output: docs/diagrams/[filename].puml
Always render: PNG or SVG
Always link the image from the Markdown
Wiki: upload the image with the page
Confluence: upload the image
```

## Step 4: Present options

```
Generated [diagram type]: [path]

Wiki: Mermaid stays inline. PlantUML is an image link plus uploaded file.
Confluence: both are images.
```

## Quick reference

| Show | Tool | Wiki | Confluence |
|------|------|------|------------|
| Context, containers, sequence, class, ER, state, activity | design-doc-mermaid | fenced mermaid | PNG/SVG upload |
| Wireframe, use case, timing, ArchiMate, nwdiag, WBS | plantuml | PNG/SVG upload | PNG/SVG upload |

For detailed guidance: [04-diagrams-selection.md](../reference/04-diagrams-selection.md)
