# Code-to-Docs: Extraction Workflow

---
TOKEN_BUDGET: 180
TIER: 3
LOAD_TRIGGER: On-demand when executing brownfield documentation generation
DEPENDENCIES: 09-code-to-docs-detection.md
---

## 9.3 Extraction Workflow

### 7-Step Process

**Step 1: Detect Framework**
- Scan for key files (Glob)
- Confirm framework patterns (Grep)
- Load framework mapping

**Step 2: Load Mapping**
- Use framework-specific extraction rules
- Example: `mappings/backend/spring-boot-mapping.yaml`

**Step 3: Scan Codebase**
- Use Glob and Grep to find components
- Example: Find all `@RestController` classes

**Step 4: Read Key Files**
- Extract relevant code elements
- Example: Read controller methods, entity classes

**Step 5: Map to Documentation**
- Apply mapping rules (code → doc sections)
- Example: `@GetMapping("/api/tasks")` → OpenAPI GET endpoint

**Step 6: Generate Artifacts**
- Create SDD, API docs, diagrams
- Example: Generate arc42 SDD, OpenAPI spec, C4 diagram

**Step 7: Post-Process**
- Offer conversions (MD → DOCX → PDF)
- Offer additional diagrams (ER, sequence)

---

### Mapping Rules Example

**Spring Boot Mapping:**
```yaml
architecture:
  entry_point:
    pattern: "@SpringBootApplication"
    extract: "Application class, port, profiles"

api:
  controller:
    pattern: "@RestController"
    extract: "Endpoints, methods, paths, parameters"

data:
  entity:
    pattern: "@Entity"
    extract: "Tables, columns, relationships"

business_logic:
  service:
    pattern: "@Service"
    extract: "Business operations"

security:
  config:
    pattern: "SecurityConfig"
    extract: "Auth methods, protected endpoints"
```

---

### Progressive Extraction

**Start Minimal**:
1. System context (what is this?)
2. Architecture overview (how is it structured?)
3. API surface (what are the endpoints?)

**Expand as Needed**:
4. Data model (database schema)
5. Business logic (service layer)
6. Security (authentication, authorization)
7. Deployment (infrastructure, config)

---

**End of Code-to-Docs Extraction Workflow Guide**
