# Brownfield Code-to-Docs Workflow

---
TOKEN_BUDGET: 1500
TIER: 3
LOAD_TRIGGER: Intent = CODE_TO_DOCS (reverse-engineer documentation from existing code)
DEPENDENCIES: SKILL.md, mappings/*, reference/09-code-to-docs.md
---

## Overview

This workflow guides the reverse-engineering of professional documentation from existing codebases (brownfield). Use this when the user wants to generate documentation from source code without manual specification.

**Supported Frameworks:**
- **Backend**: Spring Boot, FastAPI, Express.js, Django, Flask
- **Infrastructure**: Pulumi, Terraform, AWS CDK, CloudFormation
- **Frontend**: React, Next.js, Vue.js, Angular
- **Data**: Python ETL, Apache Airflow, Spark, dbt
- **CLI**: Python CLI, Node CLI, Java CLI

**Token Budget**: This workflow consumes ~1,500 tokens. Load only when intent is CODE_TO_DOCS.

---

## Workflow Steps

### Step 1: Framework Detection

**Objective**: Automatically identify the technology stack by scanning the codebase.

**Detection Patterns:**

| Framework | Detection Files | Detection Patterns |
|-----------|----------------|-------------------|
| **Spring Boot** | `pom.xml`, `build.gradle` | `@SpringBootApplication`, `spring-boot-starter` |
| **FastAPI** | `requirements.txt`, `main.py` | `from fastapi import`, `app = FastAPI()` |
| **Express.js** | `package.json`, `server.js` | `const express =`, `app.listen` |
| **Django** | `manage.py`, `settings.py` | `django.setup()`, `INSTALLED_APPS` |
| **Pulumi** | `Pulumi.yaml`, `__main__.py` | `import pulumi`, `pulumi.aws.*` |
| **Terraform** | `*.tf`, `terraform.tfvars` | `resource "aws_`, `provider "` |
| **React** | `package.json`, `src/App.jsx` | `"react":`, `import React` |
| **Next.js** | `next.config.js`, `pages/` | `next/router`, `export default function` |

**Detection Process:**

```markdown
1. Use Glob to find detection files:
   Glob: "pom.xml" → Spring Boot Maven project
   Glob: "build.gradle" → Spring Boot Gradle project
   Glob: "Pulumi.yaml" → Pulumi infrastructure
   Glob: "main.tf" → Terraform infrastructure
   Glob: "package.json" + "src/App.jsx" → React frontend

2. Use Grep to confirm framework patterns:
   Grep: "@SpringBootApplication" → Confirmed Spring Boot
   Grep: "from fastapi import" → Confirmed FastAPI
   Grep: "import pulumi" → Confirmed Pulumi

3. Identify framework version (if possible):
   For Spring Boot: Read pom.xml or build.gradle for spring-boot-starter version
   For React: Read package.json for "react" version
```

**If framework is detected:**
→ Load framework-specific mapping file: `mappings/{category}/{framework}-mapping.yaml`
→ Load framework-specific guide: `guides/code-to-docs/{category}/{framework}-to-docs.md`

**If framework is NOT detected:**
→ Ask user: "I couldn't detect the framework. Is this a [list common frameworks]?"
→ Fallback to generic code analysis

### Step 2: Load Framework Mapping

**For Spring Boot:**
```
Read: mappings/backend/spring-boot-mapping.yaml
Read: guides/code-to-docs/backend/spring-boot-to-docs.md (if needed)
```

**For Pulumi:**
```
Read: mappings/infrastructure/pulumi-mapping.yaml
Read: guides/code-to-docs/infrastructure/pulumi-to-docs.md (if needed)
```

**For FastAPI (when available):**
```
Read: mappings/backend/fastapi-mapping.yaml
Read: guides/code-to-docs/backend/fastapi-to-docs.md (if needed)
```

**IMPORTANT**: Load ONLY the mapping file for the detected framework. Do NOT load all mappings.

### Step 3: Code Analysis (6-Step Extraction)

#### Step 3.1: Architecture Extraction

**Objective**: Identify high-level system architecture.

**For Spring Boot:**
```
Grep: "@SpringBootApplication" → Main application class
Grep: "@Configuration" → Configuration classes
Read: application.yml or application.properties → External systems, database config
```

**Extract**:
- Application entry point
- External dependencies (database URL, external APIs from config files)
- Profiles (dev, staging, production)
- Port numbers

**For Pulumi:**
```
Read: __main__.py → Pulumi resources
Grep: "pulumi.aws.ec2.Vpc" → VPC configuration
Grep: "pulumi.aws.ecs.Cluster" → ECS clusters
Grep: "pulumi.aws.rds.Instance" → Databases
```

**Extract**:
- Cloud provider (AWS, Azure, GCP)
- Network architecture (VPC, subnets)
- Compute resources (EC2, ECS, Lambda)
- Data stores (RDS, DynamoDB, S3)

#### Step 3.2: API Extraction (Backend Only)

**For Spring Boot:**
```
Grep: "@RestController" → Find all REST controllers
For each controller:
  Grep: "@GetMapping" → GET endpoints
  Grep: "@PostMapping" → POST endpoints
  Grep: "@PutMapping" → PUT endpoints
  Grep: "@DeleteMapping" → DELETE endpoints
  Grep: "@RequestMapping" → Base path
  Read controller file → Extract method signatures, parameters, return types
```

**Extract**:
- HTTP methods (GET, POST, PUT, DELETE)
- Paths (`/api/v1/products`, `/api/v1/orders/{id}`)
- Request parameters (@PathVariable, @RequestParam, @RequestBody)
- Response types (DTOs)
- Security annotations (@PreAuthorize, @Secured)

**For FastAPI (when available):**
```
Grep: "@app.get(" → GET endpoints
Grep: "@app.post(" → POST endpoints
Read route functions → Extract path parameters, query parameters, request bodies
```

**Output**: Generate OpenAPI 3.0 specification

#### Step 3.3: Data Model Extraction

**For Spring Boot:**
```
Grep: "@Entity" → Find all JPA entities
For each entity:
  Grep: "@Table" → Table name
  Grep: "@Column" → Column definitions
  Grep: "@Id" → Primary key
  Grep: "@ManyToOne|@OneToMany|@ManyToMany" → Relationships
  Read entity file → Extract field types, constraints
```

**Extract**:
- Entity names (User, Product, Order)
- Table names (users, products, orders)
- Fields and data types (String, Integer, LocalDateTime)
- Relationships (Order → User is ManyToOne)
- Constraints (nullable, unique, length)

**Output**: Generate ER diagram with PlantUML

#### Step 3.4: Business Logic Extraction

**For Spring Boot:**
```
Grep: "@Service" → Find all service classes
Grep: "@Component" → Find all component classes
Read service files → Extract public method signatures, workflows
```

**Extract**:
- Service layer architecture
- Key business workflows (e.g., createOrder, processPayment)
- Transaction boundaries (@Transactional)

**Output**: Document in SDD Section 5 (Building Block View)

#### Step 3.5: Security Extraction

**For Spring Boot:**
```
Grep: "@Configuration.*Security" → Security configuration
Grep: "WebSecurityConfigurerAdapter|SecurityFilterChain" → Security setup
Read security config → Extract authentication, authorization rules
```

**Extract**:
- Authentication method (JWT, OAuth2, Basic)
- Authorization rules (URL patterns, roles)
- CORS configuration
- CSRF protection

**Output**: Document in SDD Section 8 (Crosscutting Concepts - Security)

#### Step 3.6: Deployment Configuration Extraction

**For Spring Boot:**
```
Read: application.yml or application.properties
Read: Dockerfile (if exists)
Read: docker-compose.yml (if exists)
Read: kubernetes/*.yaml (if exists)
```

**For Pulumi:**
```
Read: Pulumi.yaml → Project configuration
Read: __main__.py → All infrastructure resources
Extract: VPC, ECS, RDS, S3, CloudFront, security groups, IAM roles
```

**Extract**:
- Database connection (host, port, database name)
- Port numbers
- Environment variables
- Docker images
- Kubernetes deployments

**Output**: Document in SDD Section 7 (Deployment View)

### Step 4: Generate Documentation Artifacts

Based on framework type, generate appropriate documentation:

#### For Backend Applications (Spring Boot, FastAPI, etc.)

**Generate:**

1. **Software Design Document (SDD) - arc42 format**
   - Section 3: System Context (external systems from config)
   - Section 5: Building Block View (controllers, services, repositories)
   - Section 6: Data Design (entities, relationships, ER diagram)
   - Section 7: Deployment View (application.yml, Docker, Kubernetes)
   - Section 8: Crosscutting Concepts (security, logging, error handling)

2. **OpenAPI 3.0 Specification**
   - `info`: API title, version (from pom.xml or package.json)
   - `servers`: URLs from application config
   - `paths`: All endpoints extracted from @RestController methods
   - `components.schemas`: DTOs from request/response classes
   - `components.securitySchemes`: Security config
   - `security`: Applied security globally

3. **Diagrams**
   - C4 Container Diagram (Mermaid - via mermaid-architect)
   - Component Diagram (PlantUML - via plantuml)
   - ER Diagram (PlantUML - via plantuml)
   - Sequence Diagrams for key flows (PlantUML - via plantuml)

**Save to:**
```
docs/
├── design/
│   └── {project-name}-sdd.md
├── api/
│   └── {project-name}-openapi.yaml
└── diagrams/
    ├── c4-container.md
    ├── component-diagram.puml
    ├── er-diagram.puml
    └── sequence-*.puml
```

#### For Infrastructure (Pulumi, Terraform)

**Generate:**

1. **Deployment Architecture Document**
   - Network Architecture (VPC, subnets, NAT, Internet Gateway)
   - Compute Resources (ECS, EC2, Lambda)
   - Data Layer (RDS, DynamoDB, S3)
   - CDN (CloudFront)
   - Security (Security Groups, IAM Roles)
   - Cost Estimation (optional)

2. **Diagrams**
   - C4 Level 2: Infrastructure containers (Mermaid - via mermaid-architect)
   - Deployment Diagram (PlantUML - via plantuml)

**Save to:**
```
docs/
├── deployment/
│   └── {project-name}-infrastructure.md
└── diagrams/
    ├── infrastructure-c4.md
    └── deployment-topology.puml
```

#### For Frontend (React, Next.js)

**Generate:**

1. **Component Architecture Document**
   - Component hierarchy
   - State management (Redux, Context API)
   - Routing structure
   - API integration points

2. **Diagrams**
   - Component hierarchy diagram
   - State flow diagram

**Save to:**
```
docs/
├── design/
│   └── {project-name}-frontend-design.md
└── diagrams/
    └── component-hierarchy.puml
```

### Step 5: Invoke Diagram Skills

After generating documentation, invoke diagram skills:

**For C4 Diagrams (System Context, Container, Component):**
```
Invoke: mermaid-architect skill
Pass: System components extracted from code
Request: C4 container diagram showing:
  - Frontend (React app)
  - Backend (Spring Boot API)
  - Database (PostgreSQL)
  - External systems (Stripe, SendGrid)
```

**For UML Diagrams (ER, Component, Sequence):**
```
Invoke: plantuml skill
Pass: Entity relationships or component structure
Request:
  - ER diagram from @Entity classes
  - Component diagram showing layers
  - Sequence diagram for "Create Order" flow
```

### Step 6: Professional Formatting

Ensure all generated documentation includes:

- ✅ **Front Matter**
  - Title: "[Project Name] Software Design Document"
  - Version: Extract from pom.xml, package.json, or default to "1.0"
  - Date: Current date
  - Generated by: "Claude Code - Documentation Specialist Skill"

- ✅ **Table of Contents**
  - Auto-generate for docs > 3 pages

- ✅ **Code References**
  - Link to specific files and line numbers when mentioning code elements
  - Example: "The OrderController (src/controllers/OrderController.java:45) handles order creation"

- ✅ **Glossary**
  - Define all technical terms
  - Define all framework-specific annotations (@Entity, @RestController)

- ✅ **Traceability**
  - Map code elements to documentation sections
  - Example: "FR-ORDER-001 is implemented in OrderService.createOrder()"

### Step 7: Post-Processing Offers

After generating all artifacts, offer:

```
I've analyzed your [framework] application and generated:
- Software Design Document (arc42): docs/design/{project}-sdd.md
- OpenAPI Specification: docs/api/{project}-openapi.yaml
- C4 Container Diagram: docs/diagrams/c4-container.md
- Component Diagram: docs/diagrams/component-diagram.puml
- ER Diagram: docs/diagrams/er-diagram.puml

Would you like me to:
1. Convert the SDD to Word format (DOCX)?
2. Generate a PDF documentation package?
3. Render PlantUML diagrams to PNG images?
4. Create sequence diagrams for specific workflows?
5. Generate deployment runbook documentation?
6. Create additional diagrams (state machine, activity)?
```

---

## Example 1: Spring Boot E-Commerce API

**User Request:**
```
Document my Spring Boot application at ~/projects/ecommerce-api
```

**Workflow Execution:**

### Step 1: Framework Detection
```
Glob: "pom.xml" → Found
Grep: "@SpringBootApplication" → Found at src/main/java/com/example/EcommerceApplication.java
Detection: Spring Boot 3.1 (from pom.xml)
```

### Step 2: Load Framework Mapping
```
Read: mappings/backend/spring-boot-mapping.yaml
```

### Step 3: Code Analysis

**3.1 Architecture:**
```
Read: src/main/resources/application.yml
Extracted:
  - Server port: 8080
  - Database: jdbc:postgresql://localhost:5432/ecommerce
  - External API: https://api.stripe.com (payment gateway)
```

**3.2 API Extraction:**
```
Grep: "@RestController" → Found 8 controllers
  - OrderController.java
  - ProductController.java
  - UserController.java
  - CartController.java
  - PaymentController.java
  - CategoryController.java
  - ReviewController.java
  - ShippingController.java

For OrderController:
  @GetMapping("/api/v1/orders") → List all orders
  @PostMapping("/api/v1/orders") → Create order
  @GetMapping("/api/v1/orders/{orderId}") → Get order by ID
  @PutMapping("/api/v1/orders/{orderId}") → Update order
  @DeleteMapping("/api/v1/orders/{orderId}") → Delete order
```

**3.3 Data Model:**
```
Grep: "@Entity" → Found 12 entities
  - Order.java
  - Product.java
  - User.java
  - CartItem.java
  - OrderItem.java
  - Category.java
  - Review.java
  - Address.java
  - Payment.java
  - Shipping.java
  - Inventory.java
  - Discount.java

For Order entity:
  @Table(name = "orders")
  Fields: id (Long), user (User @ManyToOne), orderItems (List<OrderItem> @OneToMany),
          status (OrderStatus enum), totalAmount (BigDecimal),
          createdAt (LocalDateTime), updatedAt (LocalDateTime)
```

**3.4 Business Logic:**
```
Grep: "@Service" → Found 10 services
  - OrderService.java
  - ProductService.java
  - UserService.java
  - CartService.java
  - PaymentService.java
  - EmailService.java
  - InventoryService.java
  - ShippingService.java
  - DiscountService.java
  - ReviewService.java
```

**3.5 Security:**
```
Read: src/main/java/com/example/config/SecurityConfig.java
Extracted:
  - Authentication: JWT (Bearer token)
  - Public endpoints: /api/v1/auth/**, /api/v1/products (GET)
  - Protected endpoints: /api/v1/orders/**, /api/v1/users/**
  - Roles: USER, ADMIN
```

**3.6 Deployment:**
```
Read: application.yml
Read: Dockerfile
Extracted:
  - Java 17, Spring Boot 3.1
  - PostgreSQL database
  - Redis for caching
  - Nginx reverse proxy
  - Docker Compose setup
```

### Step 4: Generate Documentation

**Generated:**

1. **docs/design/ecommerce-api-sdd.md** (arc42 format, 25 pages)
2. **docs/api/ecommerce-openapi.yaml** (OpenAPI 3.0, 800 lines, 40 endpoints)
3. **docs/diagrams/c4-container.md** (Mermaid C4 showing: Web App, API, PostgreSQL, Redis, Stripe)
4. **docs/diagrams/component-diagram.puml** (PlantUML showing: Controller, Service, Repository layers)
5. **docs/diagrams/er-diagram.puml** (PlantUML showing: 12 tables with relationships)
6. **docs/diagrams/sequence-create-order.puml** (PlantUML showing: Order creation flow)

### Step 5: Invoke Diagram Skills

```
Skill: mermaid-architect
Task: Generate C4 container diagram
Output: docs/diagrams/c4-container.md

Skill: plantuml
Task: Generate ER diagram from @Entity classes
Output: docs/diagrams/er-diagram.puml
```

### Step 6-7: Format and Offer Post-Processing

```
I've analyzed your Spring Boot e-commerce API and generated:
✅ Software Design Document: docs/design/ecommerce-api-sdd.md
✅ OpenAPI Specification: docs/api/ecommerce-openapi.yaml
✅ C4 Container Diagram: docs/diagrams/c4-container.md
✅ Component Diagram: docs/diagrams/component-diagram.puml
✅ ER Diagram: docs/diagrams/er-diagram.puml
✅ Sequence Diagram (Create Order): docs/diagrams/sequence-create-order.puml

Would you like me to:
1. Convert the SDD to Word format?
2. Generate a PDF package?
3. Render PlantUML diagrams to PNG?
```

---

## Example 2: Pulumi AWS Infrastructure

**User Request:**
```
Generate deployment documentation from my Pulumi AWS infrastructure at ~/projects/aws-infra
```

**Workflow Execution:**

### Step 1: Framework Detection
```
Glob: "Pulumi.yaml" → Found
Grep: "import pulumi" → Found in __main__.py
Detection: Pulumi (Python, AWS provider)
```

### Step 2: Load Framework Mapping
```
Read: mappings/infrastructure/pulumi-mapping.yaml
```

### Step 3: Code Analysis

**Read: __main__.py**
```python
Extracted resources:
- pulumi.aws.ec2.Vpc("main-vpc", cidr_block="10.0.0.0/16")
- pulumi.aws.ec2.Subnet("public-subnet-1", vpc_id=vpc.id, cidr_block="10.0.1.0/24")
- pulumi.aws.ecs.Cluster("app-cluster")
- pulumi.aws.ecs.Service("web-service", cluster=cluster.arn)
- pulumi.aws.rds.Instance("postgres-db", engine="postgres", instance_class="db.t3.medium")
- pulumi.aws.s3.Bucket("app-assets")
- pulumi.aws.cloudfront.Distribution("cdn", origins=[...])
```

### Step 4: Generate Documentation

**Generated:**

1. **docs/deployment/aws-infrastructure.md** (15 pages covering)
   - Network Architecture (VPC, subnets, NAT Gateway, Internet Gateway)
   - Compute Resources (ECS cluster, services, task definitions)
   - Data Layer (RDS PostgreSQL, S3)
   - CDN (CloudFront)
   - Security (Security Groups, IAM Roles)

2. **docs/diagrams/infrastructure-c4.md** (Mermaid C4 Level 2)
3. **docs/diagrams/deployment-topology.puml** (PlantUML deployment diagram)

### Step 5-7: Invoke Skills and Offer Post-Processing

```
I've analyzed your Pulumi AWS infrastructure and generated:
✅ Deployment Architecture Document: docs/deployment/aws-infrastructure.md
✅ C4 Infrastructure Diagram: docs/diagrams/infrastructure-c4.md
✅ Deployment Topology Diagram: docs/diagrams/deployment-topology.puml

Would you like me to:
1. Generate a deployment runbook with step-by-step procedures?
2. Create a cost estimation document?
3. Generate disaster recovery documentation?
```

---

## Framework-Specific Notes

### Spring Boot Best Practices
- Always extract @RestController methods for OpenAPI spec
- Generate ER diagram from @Entity classes
- Document security configuration (@Configuration + SecurityFilterChain)
- Extract database config from application.yml

### Pulumi Best Practices
- Extract all pulumi.aws.* resources
- Group by category (Network, Compute, Data, Security)
- Document VPC structure with CIDR blocks
- Include security groups and IAM roles

### FastAPI Best Practices (when available)
- Extract @app.get/@app.post decorators for OpenAPI
- Use Pydantic models for schema generation
- Document authentication (OAuth2, API Key)

---

## Quality Checklist

Before finalizing brownfield documentation, verify:

- [ ] **Framework Detected**: Confirmed via Glob and Grep
- [ ] **Mapping Loaded**: Framework-specific mapping file read
- [ ] **Code Analyzed**: All 6 extraction steps completed
- [ ] **SDD Generated**: arc42 format with all relevant sections
- [ ] **API Spec Generated**: OpenAPI 3.0 with all endpoints (backend only)
- [ ] **Diagrams Generated**: C4, Component, ER, Sequence (as appropriate)
- [ ] **File References**: Code references include file paths and line numbers
- [ ] **Accurate Extraction**: All extracted data matches actual code
- [ ] **Glossary Added**: Framework-specific terms defined
- [ ] **Professional Formatting**: Proper headings, tables, code blocks
- [ ] **Diagrams Invoked**: mermaid-architect and plantuml skills called
- [ ] **Post-Processing Offered**: User offered format conversion

---

## References

For more detailed framework-specific guidance:

- **Spring Boot**: `guides/code-to-docs/backend/spring-boot-to-docs.md`
- **Pulumi**: `guides/code-to-docs/infrastructure/pulumi-to-docs.md`
- **Code-to-Docs Philosophy**: `reference/09-code-to-docs.md`
- **Diagram Selection**: `reference/04-diagrams.md`

**Do NOT load these unless explicitly needed for complex scenarios.**

---

**End of Brownfield Workflow Guide**
