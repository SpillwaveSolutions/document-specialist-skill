# Spring Boot Code-to-Docs Guide

---
TOKEN_BUDGET: 300
TIER: 3
LOAD_TRIGGER: CODE_TO_DOCS + Spring Boot detected
DEPENDENCIES: brownfield-workflow.md
---

## Detection

```
Glob: "pom.xml" or "build.gradle"
Grep: "@SpringBootApplication"
```

## Extraction Commands

### Architecture (Step 3.1)
```
Grep: "@SpringBootApplication" → Main class
Read: application.yml → Database, external APIs, ports
Grep: "@Configuration" → Config classes
```

### API (Step 3.2)
```
Grep: "@RestController" → All controllers
For each controller:
  Grep: "@GetMapping|@PostMapping|@PutMapping|@DeleteMapping"
  Grep: "@RequestMapping" → Base path
  Extract: Method signatures, @PathVariable, @RequestParam, @RequestBody
```

### Data Model (Step 3.3)
```
Grep: "@Entity" → All JPA entities
For each entity:
  Grep: "@Table" → Table name
  Grep: "@Column" → Fields
  Grep: "@ManyToOne|@OneToMany|@ManyToMany" → Relationships
```

### Business Logic (Step 3.4)
```
Grep: "@Service" → Service classes
Grep: "@Transactional" → Transaction boundaries
Extract: Public method signatures
```

### Security (Step 3.5)
```
Grep: "SecurityFilterChain|WebSecurityConfigurerAdapter"
Read: Security config class
Extract: Auth method (JWT, OAuth2), URL patterns, roles
```

### Deployment (Step 3.6)
```
Read: application.yml → Database URL, ports
Read: Dockerfile (if exists)
Read: docker-compose.yml (if exists)
Read: kubernetes/*.yaml (if exists)
```

## Output Files

| Artifact | Location | Content |
|----------|----------|---------|
| SDD | `docs/design/{project}-sdd.md` | arc42 format |
| OpenAPI | `docs/api/{project}-openapi.yaml` | All REST endpoints |
| C4 Diagram | `docs/diagrams/c4-container.md` | System overview |
| ER Diagram | `docs/diagrams/er-diagram.puml` | Entity relationships |
| Component | `docs/diagrams/component.puml` | Layer architecture |

## Key Annotations Reference

| Annotation | Meaning |
|------------|---------|
| `@RestController` | REST API controller |
| `@Entity` | JPA database entity |
| `@Service` | Business logic service |
| `@Repository` | Data access layer |
| `@Configuration` | Configuration class |

For mapping file: [spring-boot-mapping.yaml](../../mappings/backend/spring-boot-mapping.yaml)
