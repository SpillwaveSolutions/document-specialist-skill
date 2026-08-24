# Diagrams: Choosing the Right Diagram

---
TOKEN_BUDGET: 280
TIER: 3
LOAD_TRIGGER: On-demand when selecting diagram type for documentation
DEPENDENCIES: None
---

## 4.1 Choosing the Right Diagram

Default is Mermaid. GitHub wiki renders it. Use PlantUML only for types
Mermaid does not do well, plus every wireframe.

### Decision matrix

| Need | Diagram | Tool |
|------|---------|------|
| System boundary and external actors | C4 Context | Mermaid |
| Deployable containers | C4 Container | Mermaid |
| Internal modules | C4 Component or flowchart | Mermaid |
| Interactions over time | Sequence | Mermaid |
| Object lifecycle | State (`stateDiagram-v2`) | Mermaid |
| Workflow or business process | Flowchart | Mermaid |
| Database schema | ER (`erDiagram`) | Mermaid |
| Class relationships | Class (`classDiagram`) | Mermaid |
| Infra as boxes and arrows | Flowchart | Mermaid |
| UI wireframe or screen mock | Salt wireframe | PlantUML |
| Actors and goals | Use case | PlantUML |
| Clock or waveform | Timing | PlantUML |
| Enterprise layers | ArchiMate | PlantUML |

### Publish

- GitHub wiki: Mermaid stays in a fenced block. PlantUML is a PNG or SVG
  that you commit and upload with the wiki page.
- Confluence: render Mermaid and PlantUML to images and upload both.

### Common scenarios

**New microservices architecture**
1. C4 Context
2. C4 Container
3. C4 Component or flowchart for a complex service
4. Sequence for key workflows

**REST API**
1. OpenAPI as the primary spec
2. Sequence for auth
3. State for resource lifecycle

**Database**
1. Mermaid `erDiagram`

**Onboarding**
1. C4 Context
2. Flowchart or C4 Component
3. Mermaid class diagram for a dense OOP cluster
4. Sequence for critical flows

**UI**
1. PlantUML Salt wireframe, rendered to PNG, linked and uploaded

---

**End of Diagram Selection Guide**
