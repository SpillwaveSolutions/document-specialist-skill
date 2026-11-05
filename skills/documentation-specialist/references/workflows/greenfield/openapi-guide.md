# OpenAPI Generation Guide

---
TOKEN_BUDGET: 250
TIER: 3
LOAD_TRIGGER: CREATE_NEW + OpenAPI/API spec
DEPENDENCIES: greenfield-workflow.md
---

## OpenAPI 3.0 Structure

### 1. Info Section
```yaml
openapi: "3.0.3"
info:
  title: "[API Name]"
  description: "[Purpose and overview]"
  version: "1.0.0"
  contact:
    name: API Support
    email: api@example.com
```

### 2. Servers
```yaml
servers:
  - url: https://api.example.com/v1
    description: Production
  - url: https://staging-api.example.com/v1
    description: Staging
```

### 3. Tags (Logical Grouping)
```yaml
tags:
  - name: Users
    description: User management operations
  - name: Authentication
    description: Auth and authorization
```

### 4. Components (Reusable)

**Security Schemes**:
```yaml
components:
  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```

**Schemas** (Data Models):
```yaml
  schemas:
    User:
      type: object
      required: [id, email]
      properties:
        id:
          type: string
          format: uuid
        email:
          type: string
          format: email
```

**Common Responses**:
```yaml
  responses:
    NotFound:
      description: Resource not found
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
```

### 5. Paths (Endpoints)

```yaml
paths:
  /users/{id}:
    get:
      tags: [Users]
      summary: Get user by ID
      operationId: getUserById
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
            format: uuid
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          $ref: '#/components/responses/NotFound'
      security:
        - BearerAuth: []
```

## Best Practices

1. **Use $ref** for reusable components
2. **Include examples** for request/response bodies
3. **Document all response codes** (200, 400, 401, 404, 500)
4. **Add descriptions** to all fields
5. **Use semantic operationIds** (getUserById, createUser)

## Reference

For API documentation standards: [05-api-openapi.md](../../reference/05-api-openapi.md)

For Stripe-style best practices: [05-api-stripe-gold-standard.md](../../reference/05-api-stripe-gold-standard.md)

For complete example: [task-api-openapi.yaml](../../examples/greenfield/task-api-openapi.yaml)
