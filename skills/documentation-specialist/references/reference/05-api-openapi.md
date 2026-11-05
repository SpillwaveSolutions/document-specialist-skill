# API Documentation: OpenAPI Specification

---
TOKEN_BUDGET: 380
TIER: 3
LOAD_TRIGGER: On-demand when creating OpenAPI specifications
DEPENDENCIES: 05-api-stripe-gold-standard.md
---

## 5.2 OpenAPI Specification (Swagger)

The modern standard for API documentation is the **OpenAPI 3.x** specification.

### Key Sections

```yaml
openapi: 3.0.3
info:
  title: Task Manager API
  version: 1.0.0
  description: API for managing tasks and projects

servers:
  - url: https://api.taskmanager.com/v1
    description: Production
  - url: https://staging-api.taskmanager.com/v1
    description: Staging

paths:
  /tasks:
    get:
      summary: List tasks
      description: Retrieve a list of tasks with optional filtering
      parameters:
        - name: status
          in: query
          description: Filter by task status
          schema:
            type: string
            enum: [pending, in_progress, completed]
        - name: limit
          in: query
          description: Number of tasks to return
          schema:
            type: integer
            default: 20
            maximum: 100
      responses:
        '200':
          description: List of tasks
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Task'
        '401':
          description: Unauthorized
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'

    post:
      summary: Create task
      description: Create a new task
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
                $ref: '#/components/schemas/Task'

components:
  schemas:
    Task:
      type: object
      required:
        - id
        - title
        - status
      properties:
        id:
          type: string
          format: uuid
          example: "550e8400-e29b-41d4-a716-446655440000"
        title:
          type: string
          example: "Complete documentation"
        description:
          type: string
          nullable: true
        status:
          type: string
          enum: [pending, in_progress, completed]
        createdAt:
          type: string
          format: date-time

    CreateTaskRequest:
      type: object
      required:
        - title
      properties:
        title:
          type: string
        description:
          type: string

    Error:
      type: object
      properties:
        code:
          type: string
        message:
          type: string

  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
      description: JWT token obtained from /auth/login

security:
  - BearerAuth: []
```

### Best Practices

1. **Use components for reusable schemas**: Define Task, Error once, reference everywhere
2. **Include examples**: Help developers understand expected formats
3. **Document all status codes**: 200, 201, 400, 401, 404, 500
4. **Specify enums**: Constrain values (status: [pending, in_progress, completed])
5. **Mark required fields**: Use `required` array
6. **Use descriptions**: Explain non-obvious parameters

---

**End of OpenAPI Specification Guide**
