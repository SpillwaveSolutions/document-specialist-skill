# Architecture document

**System:** Northstar Commerce  
**Version:** 1.2.0  
**Status:** Accepted  
**Audience:** Engineers joining the platform  
**Voice:** Google developer documentation style

This is the short C4-first cousin of `DESIGN_DOC.md`. Use it when the user wants system context, containers, and key sequences without the full arc42 ceremony. For regulated reviews, write the SDD instead.

---

## Purpose

Northstar lets a retailer publish a catalog, take payment, and hand a parcel to a carrier. This note shows where those responsibilities live and how a checkout call travels.

---

## System context

Shoppers and merchandizers are people. The PSP, the carrier, and email are external systems. Northstar is the single system of record for orders.

```mermaid
flowchart TB
  shopper([Shopper])
  merch([Merchandizer])
  ns[Northstar Commerce]
  psp[PSP]
  carrier[Carrier]
  email[Email]
  shopper -->|HTTPS| ns
  merch -->|HTTPS| ns
  ns -->|capture and refund| psp
  ns -->|label and track| carrier
  ns -->|receipt| email
```

---

## Containers

| Container | Tech | Role |
|-----------|------|------|
| Storefront | SSR web app | Shopper UI |
| Admin console | SPA | Merchandizing |
| API | Java 21 | Catalog, checkout, fulfillment |
| Postgres | Cloud SQL | Orders and catalog |
| Redis | Memorystore | Carts |
| Worker | Java 21 | Outbox drain |

```mermaid
flowchart LR
  shopper([Shopper]) --> web[Storefront]
  merch([Merchandizer]) --> admin[Admin]
  web --> api[API]
  admin --> api
  api --> pg[(Postgres)]
  api --> redis[(Redis)]
  api --> worker[Worker]
  worker --> pg
  worker --> psp[PSP]
  worker --> carrier[Carrier]
```

---

## Components inside the API

```mermaid
flowchart TB
  subgraph api [API]
    cat[Catalog]
    chk[Checkout]
    pay[Payments adapter]
    ful[Fulfillment]
  end
  cat --> chk
  chk --> pay
  chk --> ful
```

Catalog owns products and prices. Checkout owns orders. Payments never stores PAN. Fulfillment drains the outbox.

---

## Key sequence: checkout

Keep this to five participants.

```mermaid
sequenceDiagram
  participant W as Storefront
  participant A as API
  participant P as Payments
  participant D as Postgres
  participant Q as Worker

  W->>A: POST /orders
  A->>D: pending order
  A->>P: capture
  P-->>A: capture id
  A->>D: captured plus outbox
  A-->>W: 201
  Q->>D: read outbox
  Q->>Q: notify carrier
```

---

## Deployment

```mermaid
flowchart LR
  dns[HTTPS LB] --> web[Storefront pods]
  dns --> api[API pods]
  api --> pg[(Cloud SQL)]
  api --> redis[(Redis)]
  worker[Worker pods] --> pg
```

Staging mirrors production with a smaller replica. Promotes with a tagged image.

---

## Decisions to read next

- ADR-001 Modular monolith
- ADR-002 Transactional outbox

When a change crosses two containers or a quality goal, update this file and `DESIGN_DOC.md` in the same PR.

---

## UI wireframes

PlantUML Salt for the shopper checkout. Full catalog and admin screens are in the UI wireframes example.

```puml
@startuml
salt
{
  {+
    Northstar / Checkout
    {/ Cart | <b>Shipping | Payment | Review }
    Ship to
    { Address | "1200 Congress Ave" }
    { City    | "Austin" } | { ZIP | "78701" }
    Payment | PSP host field "•••• 4242"
    { [ Back ] | [ Place order ] }
  }
}
@enduml
```

---

## Use cases (PlantUML leftover)

GitHub wiki does not render the following source. Render PNG or SVG, commit it under `docs/diagrams/`, and upload the image with the wiki page.

```puml
@startuml
left to right direction
actor Shopper
actor Merchandizer
rectangle Northstar {
  usecase "Browse catalog" as UC1
  usecase "Place order" as UC2
  usecase "Refund order" as UC3
  usecase "Publish price" as UC4
}
Shopper --> UC1
Shopper --> UC2
Merchandizer --> UC3
Merchandizer --> UC4
@enduml
```
