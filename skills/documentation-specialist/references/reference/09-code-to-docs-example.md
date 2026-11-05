# Code-to-Docs: Spring Boot to OpenAPI Example

---
TOKEN_BUDGET: 200
TIER: 3
LOAD_TRIGGER: On-demand when demonstrating code-to-docs extraction
DEPENDENCIES: 09-code-to-docs-workflow.md
---

## 9.4 Example: Spring Boot API to OpenAPI

### Input (Java)

```java
@RestController
@RequestMapping("/api/v1/tasks")
public class TaskController {

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public TaskDTO createTask(@Valid @RequestBody CreateTaskRequest request) {
        return taskService.create(request);
    }

    @GetMapping("/{id}")
    public TaskDTO getTask(@PathVariable String id) {
        return taskService.findById(id);
    }

    @GetMapping
    public List<TaskDTO> listTasks(
        @RequestParam(required = false) String status,
        @RequestParam(defaultValue = "20") int limit
    ) {
        return taskService.findAll(status, limit);
    }
}
```

---

### Extraction Process

**Step 1: Detect @RestController**
```bash
grep -r "@RestController" src/
# Found: src/main/java/com/example/TaskController.java
```

**Step 2: Extract Endpoints**
- `@PostMapping` → POST /api/v1/tasks
- `@GetMapping("/{id}")` → GET /api/v1/tasks/{id}
- `@GetMapping` → GET /api/v1/tasks

**Step 3: Extract Parameters**
- POST body: `CreateTaskRequest`
- Path param: `id` (String)
- Query params: `status` (String, optional), `limit` (int, default 20)

**Step 4: Extract Response**
- POST returns: `TaskDTO` (201 Created)
- GET returns: `TaskDTO` or `List<TaskDTO>` (200 OK)

---

### Output (OpenAPI)

```yaml
paths:
  /api/v1/tasks:
    post:
      summary: Create a new task
      operationId: createTask
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreateTaskRequest'
      responses:
        '201':
          description: Task created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/TaskDTO'

    get:
      summary: List tasks
      operationId: listTasks
      parameters:
        - name: status
          in: query
          required: false
          schema:
            type: string
        - name: limit
          in: query
          required: false
          schema:
            type: integer
            default: 20
      responses:
        '200':
          description: List of tasks
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/TaskDTO'

  /api/v1/tasks/{id}:
    get:
      summary: Get task by ID
      operationId: getTask
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Task details
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/TaskDTO'
```

---

### Automation Tools

**Spring Boot**:
- Springdoc OpenAPI (auto-generates OpenAPI 3.0)
- Swagger annotations for customization

**FastAPI**:
- Built-in OpenAPI generation

**Express.js**:
- swagger-jsdoc + swagger-ui-express

---

**End of Spring Boot to OpenAPI Example Guide**
