# FastAPI Code-to-Docs Guide

---
TOKEN_BUDGET: 250
TIER: 3
LOAD_TRIGGER: CODE_TO_DOCS + FastAPI detected
DEPENDENCIES: brownfield-workflow.md
---

## Detection

```
Glob: "requirements.txt" or "pyproject.toml"
Grep: "from fastapi import|fastapi"
Grep: "app = FastAPI()"
```

## Extraction Commands

### Architecture (Step 3.1)
```
Grep: "app = FastAPI()" → Main app instance
Read: main.py or app.py → App configuration
Read: config.py or settings.py → Settings
Grep: "BaseSettings" → Pydantic settings
```

### API (Step 3.2)
```
Grep: "@app.get|@app.post|@app.put|@app.delete"
Grep: "@router.get|@router.post" → APIRouter endpoints
For each route:
  Extract: Path, parameters, response_model, dependencies
```

### Data Model (Step 3.3)
```
Grep: "class.*BaseModel" → Pydantic models
Grep: "class.*Base.*Model" → SQLAlchemy models (if used)
Grep: "Column\(|relationship\(" → SQLAlchemy fields
```

### Business Logic (Step 3.4)
```
Read: services/*.py → Service functions
Grep: "async def" → Async operations
Grep: "Depends\(" → Dependency injection
```

### Security (Step 3.5)
```
Grep: "OAuth2PasswordBearer|HTTPBearer"
Grep: "Depends.*get_current_user"
Read: auth.py or security.py
```

### Deployment (Step 3.6)
```
Read: Dockerfile
Read: docker-compose.yml
Grep: "uvicorn|gunicorn" → ASGI server config
```

## Output Files

| Artifact | Location |
|----------|----------|
| SDD | `docs/design/{project}-sdd.md` |
| OpenAPI | `docs/api/{project}-openapi.yaml` |
| C4 Diagram | `docs/diagrams/c4-container.md` |

## FastAPI Advantage

FastAPI auto-generates OpenAPI! Check for existing:
```
Read: /openapi.json endpoint output
```

If available, use as base and enhance with additional context.

For mapping file: [fastapi-mapping.yaml](../../mappings/backend/fastapi-mapping.yaml)
