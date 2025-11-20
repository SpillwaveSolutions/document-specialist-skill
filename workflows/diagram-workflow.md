# Diagram Generation Workflow

---
TOKEN_BUDGET: 1000
TIER: 3
LOAD_TRIGGER: Intent = DIAGRAM (generate visual documentation)
DEPENDENCIES: SKILL.md, reference/04-diagrams.md
---

## Overview

This workflow guides diagram generation for software documentation. Use this when the user wants to create visual representations of systems, architectures, data models, or workflows.

**Supported Diagram Types:**
- **C4 Model**: Context, Container, Component, Code (via mermaid-architect)
- **UML**: Class, Sequence, Activity, State Machine, ER (via plantuml)
- **Flowcharts**: Process flows, decision trees (via mermaid-architect)
- **Other**: Network diagrams, deployment diagrams (via plantuml)

**Token Budget**: This workflow consumes ~1,000 tokens. Load only when intent is DIAGRAM.

---

## Workflow Steps

### Step 1: Identify Diagram Type

**Parse user request:**

| Keywords | Diagram Type | Tool | Use Case |
|----------|--------------|------|----------|
| "system context", "C4 context", "external systems" | C4 Context | mermaid-architect | High-level system overview with external dependencies |
| "container", "C4 container", "services" | C4 Container | mermaid-architect | Applications, data stores, microservices |
| "component", "C4 component", "modules" | C4 Component | mermaid-architect | Internal structure of a container |
| "class diagram", "classes", "inheritance" | Class Diagram | plantuml | Object-oriented design, class relationships |
| "sequence", "interaction", "message flow" | Sequence Diagram | plantuml | Time-ordered interactions between objects |
| "activity", "workflow", "process" | Activity Diagram | plantuml | Business process, algorithm flow |
| "state machine", "states", "transitions" | State Machine | plantuml | Stateful entity lifecycle |
| "ER diagram", "database", "entities" | ER Diagram | plantuml | Database schema, table relationships |
| "flowchart", "decision tree", "flow" | Flowchart | mermaid-architect | Simple process flows, decision points |
| "deployment", "infrastructure", "servers" | Deployment Diagram | plantuml | Physical deployment topology |

### Step 2: Determine Diagram Complexity

**Simple diagrams** (3-5 elements):
- Use Mermaid for quick generation
- Faster rendering
- Good for presentations

**Complex diagrams** (6+ elements, detailed relationships):
- Use PlantUML for advanced features
- Better for technical documentation
- More customization options

### Step 3: Gather Diagram Content

**For C4 Diagrams:**

Ask user or extract from context:
1. **System name**: What system are we documenting?
2. **External actors**: Users, external systems
3. **Containers**: Applications, databases, APIs
4. **Relationships**: How do they interact?

**For Sequence Diagrams:**

Ask user or extract from code:
1. **Scenario**: What workflow to diagram? (e.g., "Create Order")
2. **Actors**: Objects/services involved (e.g., Controller, Service, Repository)
3. **Steps**: Ordered sequence of method calls

**For ER Diagrams:**

Extract from code or ask user:
1. **Entities**: Tables or domain objects
2. **Attributes**: Key fields
3. **Relationships**: One-to-One, One-to-Many, Many-to-Many

**For State Machine Diagrams:**

Ask user:
1. **Entity**: What has states? (e.g., Order, Task, User)
2. **States**: List all states (e.g., Pending, Approved, Shipped)
3. **Transitions**: Events that change state

**For Activity Diagrams:**

Ask user:
1. **Process name**: What process to model?
2. **Steps**: List sequential actions
3. **Decision points**: Conditions and branches
4. **Parallel activities**: Concurrent actions

### Step 4: Invoke Appropriate Skill

#### For C4 Diagrams (mermaid-architect skill)

**C4 Context Example:**

```
Skill: mermaid-architect
Task: Generate C4 Context diagram
System: E-Commerce Platform
Elements:
  - Customer (Person, uses web browser)
  - E-Commerce System (Software System, main application)
  - Payment Gateway (External System, Stripe)
  - Email Service (External System, SendGrid)
  - Inventory System (External System, legacy ERP)
Relationships:
  - Customer → E-Commerce System: Browses products, places orders
  - E-Commerce System → Payment Gateway: Processes payments
  - E-Commerce System → Email Service: Sends order confirmations
  - E-Commerce System → Inventory System: Checks stock levels
Output: docs/diagrams/c4-context.md
```

**C4 Container Example:**

```
Skill: mermaid-architect
Task: Generate C4 Container diagram
System: E-Commerce System
Containers:
  - Web Application (React, port 3000)
  - API Service (Spring Boot, port 8080)
  - Database (PostgreSQL)
  - Cache (Redis)
  - Message Queue (RabbitMQ)
Relationships:
  - Web Application → API Service: Makes API calls (HTTPS)
  - API Service → Database: Reads/writes data (JDBC)
  - API Service → Cache: Stores sessions (Redis protocol)
  - API Service → Message Queue: Publishes events (AMQP)
Output: docs/diagrams/c4-container.md
```

#### For UML Diagrams (plantuml skill)

**Sequence Diagram Example:**

```
Skill: plantuml
Task: Generate sequence diagram for "Create Order" workflow
Participants:
  - OrderController
  - OrderService
  - InventoryService
  - PaymentService
  - OrderRepository
  - EmailService
Sequence:
  1. Client → OrderController: POST /api/v1/orders
  2. OrderController → OrderService: createOrder(orderDTO)
  3. OrderService → InventoryService: checkStock(productId)
  4. InventoryService → OrderService: stockAvailable(true)
  5. OrderService → PaymentService: processPayment(amount)
  6. PaymentService → OrderService: paymentSuccess(transactionId)
  7. OrderService → OrderRepository: save(order)
  8. OrderRepository → OrderService: savedOrder
  9. OrderService → EmailService: sendOrderConfirmation(order)
  10. OrderService → OrderController: return orderId
  11. OrderController → Client: 201 Created
Output: docs/diagrams/sequence-create-order.puml
```

**ER Diagram Example:**

```
Skill: plantuml
Task: Generate ER diagram from JPA entities
Tables:
  - users (id PK, email, name, created_at)
  - products (id PK, name, price, stock)
  - orders (id PK, user_id FK, status, total_amount, created_at)
  - order_items (id PK, order_id FK, product_id FK, quantity, price)
Relationships:
  - users (1) -- (N) orders: One user can have many orders
  - orders (1) -- (N) order_items: One order has many items
  - products (1) -- (N) order_items: One product appears in many order items
Output: docs/diagrams/er-diagram.puml
```

**State Machine Diagram Example:**

```
Skill: plantuml
Task: Generate state machine diagram for Order lifecycle
Entity: Order
States:
  - [*] → Pending: Order created
  - Pending → Confirmed: Payment received
  - Confirmed → Processing: Warehouse picked items
  - Processing → Shipped: Carrier picked up
  - Shipped → Delivered: Customer received
  - Delivered → [*]: Order complete
  - Pending → Cancelled: Customer cancelled (within 1 hour)
  - Confirmed → Cancelled: Out of stock
  - Any → Refunded: Customer requested refund
Output: docs/diagrams/state-order.puml
```

**Activity Diagram Example:**

```
Skill: plantuml
Task: Generate activity diagram for user registration process
Process: User Registration
Steps:
  1. Start
  2. User fills registration form
  3. Validate email format
  4. Decision: Valid email?
     - No → Show error, return to form
     - Yes → Continue
  5. Check if email already exists
  6. Decision: Email exists?
     - Yes → Show "Email already registered", return to form
     - No → Continue
  7. Hash password (bcrypt)
  8. Save user to database
  9. Send verification email
  10. Show "Check your email" message
  11. End
Output: docs/diagrams/activity-user-registration.puml
```

### Step 5: Offer Diagram Rendering

After generating diagram code:

```
I've generated the [diagram type] in [tool format]:
→ docs/diagrams/[filename]

Would you like me to:
1. Render this diagram to PNG/SVG? (invoke plantuml skill for rendering)
2. Generate additional related diagrams?
3. Embed this diagram in your documentation?
4. Create a diagram index/gallery?
```

---

## Diagram Selection Guide

### When to Use C4 Model (Mermaid)

**C4 Context**: High-level overview
- **Use when**: Need to show system boundaries, external dependencies
- **Audience**: Executives, product managers, non-technical stakeholders
- **Example**: "How does our system interact with third-party services?"

**C4 Container**: Application-level architecture
- **Use when**: Showing major applications, data stores, microservices
- **Audience**: Architects, senior developers, DevOps
- **Example**: "What are the main components of our platform?"

**C4 Component**: Internal structure
- **Use when**: Documenting internal modules of a single application
- **Audience**: Developers working on that application
- **Example**: "How is our Spring Boot API organized internally?"

### When to Use UML Diagrams (PlantUML)

**Class Diagram**:
- **Use when**: Documenting object-oriented design, domain model
- **Audience**: Developers, architects
- **Example**: "What are the main domain objects and their relationships?"

**Sequence Diagram**:
- **Use when**: Explaining time-ordered interactions, API flows
- **Audience**: Developers, QA engineers
- **Example**: "How does the payment processing workflow work?"

**Activity Diagram**:
- **Use when**: Documenting business processes, algorithms, workflows
- **Audience**: Business analysts, developers, QA
- **Example**: "What is the user registration flow?"

**State Machine Diagram**:
- **Use when**: Modeling stateful entities with complex lifecycles
- **Audience**: Developers, business analysts
- **Example**: "What are all the states an order can be in?"

**ER Diagram**:
- **Use when**: Database design, data modeling
- **Audience**: Database administrators, backend developers
- **Example**: "What tables exist and how are they related?"

### State Machine vs Activity Diagram

**Use State Machine when**:
- Modeling an entity that has distinct states (Order: Pending, Confirmed, Shipped)
- Focus is on state transitions and events
- Need to show which states can transition to which other states

**Use Activity Diagram when**:
- Modeling a process or workflow with sequential steps
- Focus is on actions, not states
- Need to show decision points, parallel activities, swim lanes

---

## Examples

### Example 1: Generate C4 Container Diagram

**User Request:**
```
Create a C4 container diagram for my e-commerce microservices platform
```

**Workflow:**

1. **Identify Type**: C4 Container Diagram
2. **Gather Content**:
   - Containers: Web App, Product API, Order API, User API, PostgreSQL, Redis, RabbitMQ, Payment Gateway (external)
   - Relationships: Web App calls all APIs, APIs use PostgreSQL and Redis, Order API calls Payment Gateway

3. **Invoke mermaid-architect**:
```
Skill: mermaid-architect
Generate C4 Container diagram with containers and relationships
Output: docs/diagrams/c4-ecommerce-containers.md
```

4. **Offer**: "Render to PNG?" "Generate Component diagram for Order API?"

### Example 2: Generate Sequence Diagram for API Call

**User Request:**
```
Create a sequence diagram showing how the "Get User Profile" API endpoint works
```

**Workflow:**

1. **Identify Type**: Sequence Diagram
2. **Gather Content**:
   - Participants: Client, UserController, AuthService, UserService, UserRepository, Database
   - Flow: Authentication check → Service call → Database query → Response

3. **Invoke plantuml**:
```
Skill: plantuml
Generate sequence diagram for GET /api/v1/users/{userId}
Output: docs/diagrams/sequence-get-user-profile.puml
```

4. **Offer**: "Render to PNG?" "Create similar diagrams for other endpoints?"

---

## Best Practices

1. **Keep diagrams focused**: One concern per diagram
2. **Use appropriate abstraction level**: C4 Context for executives, Component for developers
3. **Add legends**: Explain symbols, colors, line styles
4. **Update diagrams with code changes**: Keep diagrams in sync
5. **Provide context**: Add description above/below diagram explaining what it shows
6. **Use consistent naming**: Same names as in code or documentation
7. **Optimize for target medium**: Simple for presentations, detailed for technical docs

---

## Quick Reference

| Need to show... | Use this diagram | Tool |
|-----------------|------------------|------|
| System boundaries, external dependencies | C4 Context | mermaid-architect |
| Microservices, databases, applications | C4 Container | mermaid-architect |
| Internal modules of an application | C4 Component | mermaid-architect |
| Object-oriented class structure | Class Diagram | plantuml |
| Time-ordered API/method calls | Sequence Diagram | plantuml |
| Business process with decisions | Activity Diagram | plantuml |
| Entity lifecycle with states | State Machine | plantuml |
| Database tables and relationships | ER Diagram | plantuml |
| Simple process flow | Flowchart | mermaid-architect |
| Physical servers and deployment | Deployment Diagram | plantuml |

---

## References

For detailed diagram selection guidance:
- **Diagrams Overview**: `reference/04-diagrams.md`

**Do NOT load unless user needs deep dive into diagram types.**

---

**End of Diagram Workflow Guide**
