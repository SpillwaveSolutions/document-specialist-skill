# UI wireframes (PlantUML Salt)

**System:** Document Specialist and example products  
**Tool:** PlantUML Salt  
**Voice:** Google developer documentation style

Mermaid cannot sketch screens. Use PlantUML Salt for every UI in an SDD or architecture document. Keep the `.puml` source, render PNG or SVG, and link the image. GitHub wiki does not render Salt fences.

This page is the few-shot set. Copy a wireframe, rename the window title, and swap labels for the product under design.

---

## Salt cheatsheet

| Mark | Control |
|------|---------|
| `"text"` | Text field |
| `[OK]` | Button |
| `[]` | Checkbox |
| `()` | Radio |
| `^` | Drop-down |
| `{* File \| Edit }` | Menu bar |
| `{/ Tab1 \| Tab2 }` | Tabs |
| `{+ ... }` | Window |
| `{T + item ++ child}` | Tree |
| `==` `--` `..` | Separators |
| `\|` | Table cell |

Prefix the diagram with `salt` inside `@startuml`. Do not use Mermaid `block-beta` for screens.

---

## Folio library

Landing view of the Document Specialist studio. Menu, tabs, and a two-up card grid.

```puml
@startuml
salt
{
  {* File | Edit | View | Plugins }
  {+
    {/ <b>Library | DESIGN_DOC | Diagrams | Plugins }
    .
    { Folio  |  Document Specialist  |  [ Download plugin ] }
    .
    SpillwaveSolutions / document-specialist-skill
    <b>Design documents the skill was missing
    .
    {^
      {
        <b>DESIGN_DOC.md
        Architects and skill authors
        arc42 SDD of Document Specialist
        [ Open ]
      } |
      {
        <b>Northstar commerce SDD
        Greenfield few-shot
        Checkout, catalog, payments
        [ Open ]
      }
    }
    {
      {
        <b>Architecture document
        C4-first short form
        [ Open ]
      } |
      {
        <b>UI wireframes
        PlantUML Salt
        [ Open ]
      }
    }
  }
}
@enduml
```

---

## Folio document paper

Reading an SDD. Outline on the left, paper in the center, copy and plugin actions on the toolbar.

```puml
@startuml
salt
{
  {* File | Edit | View }
  {+
    {/ Library | <b>DESIGN_DOC | Diagrams | Plugins }
    .
    {
      {
        Outline
        {T
         + DESIGN_DOC.md
         ++ 1. Introduction and goals
         ++ 3. Context and scope
         ++ 5. Building block view
         ++ 6. Runtime view
         ++ 8. UI wireframes
        }
      } |
      {
        DESIGN_DOC.md
        Architects and skill authors
        { [ Copy Markdown ] | [ Plugin ] }
        ..
        <b>Document Specialist design document
        .
        System  | Document Specialist skill
        Status  | Accepted
        Voice   | Google developer documentation style
        .
        == 1. Introduction and goals
        Document Specialist turns an agent
        into a documentation specialist.
        .
        [ Context diagram rendered here ]
      }
    }
  }
}
@enduml
```

---

## Northstar catalog

Shopper browse. Filters, product grid, cart count.

```puml
@startuml
salt
{
  {* Northstar | Catalog | Account | Help }
  {+
    {/ <b>Shop | Cart (2) | Orders }
    .
    { Search  | "linen shirt"  | [ Search ] }
    .
    {
      {
        Filters
        [] In stock
        [] On sale
        Size
        () XS
        () S
        () M
        () L
        Color  | ^White^
      } |
      {^
        {
          SKU-104
          <b>Oxford shirt
          $64
          [ Add to cart ]
        } |
        {
          SKU-221
          <b>Linen shirt
          $72
          [ Add to cart ]
        }
      }
    }
  }
}
@enduml
```

---

## Northstar checkout

Single-page checkout. Shipping, payment token, place order. Card number never appears. That is a PCI constraint.

```puml
@startuml
salt
{
  {+
    Northstar / Checkout
    {/ Cart | <b>Shipping | Payment | Review }
    .
    Ship to
    { Name     | "Alex Rivera" }
    { Address  | "1200 Congress Ave" }
    { City     | "Austin" } | { ZIP | "78701" }
    [] Billing address is the same
    .
    Payment
    PSP host field  | "•••• 4242"
    Expiry          | "09 / 28"
    .
    { [ Back to cart ] | [ Place order ] }
  }
}
@enduml
```

---

## Pet Clinic: owners

Brownfield staff UI recovered from Spring MVC templates. Search by last name, then open an owner.

```puml
@startuml
salt
{
  {* Pet Clinic | Owners | Vets | Help }
  {+
    {/ <b>Find owners | Veterinarians | Error }
    .
    Find owner
    { Last name | "Davis" | [ Find Owner ] }
    [ Add Owner ]
    .
    {#
      Last name | First name | City | Pets
      Davis     | Betty      | Madison | Basil
      Davis     | Harold     | McFarland | Iggy, Lucky
    }
  }
}
@enduml
```

---

## Pet Clinic: record a visit

```puml
@startuml
salt
{
  {+
    New visit for Iggy
    .
    { Owner | Harold Davis }
    { Pet   | Iggy  (dog) }
    { Date  | "2026-09-04" }
    { Description | "Annual vaccines" }
    .
    { [ Cancel ] | [ Add Visit ] }
  }
}
@enduml
```

---

## Document Specialist plugin hosts

Settings-style screen for the four manifests.

```puml
@startuml
salt
{
  {+
    Install Document Specialist
    {/ <b>Universal | Claude Code | Grok | Codex }
    .
    Agent Plugins 1.0
    plugin.json at the repo root
    skills/documentation-specialist/SKILL.md
    .
    [] Also pin .claude-plugin
    [] Also pin .grok-plugin
    [] Also pin .codex-plugin
    .
    Default prompt
    "Write DESIGN_DOC.md using arc42.
     Include Salt wireframes for every UI."
    .
    [ Copy install command ] | [ Download zip ]
  }
}
@enduml
```

---

## How agents should file these

1. Write Salt source under `docs/diagrams/[screen].puml`.
2. Render PNG or SVG. PlantUML server, `plantuml` CLI, or this studio.
3. Link the image from `DESIGN_DOC.md`. Keep the fence so reviewers can edit.
4. One screen per diagram. Do not nest an entire product in one Salt block.

When the user names a UI, a screen, a mock, or a wireframe, load this page and `design-workflow.md`, then emit Salt. Do not substitute a Mermaid flowchart for a screen.
