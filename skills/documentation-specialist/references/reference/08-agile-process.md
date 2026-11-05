# Agile Documentation Process

---
TOKEN_BUDGET: 280
TIER: 3
LOAD_TRIGGER: On-demand when setting up agile documentation workflows
DEPENDENCIES: 01-philosophy.md
---

## 8.1 Just Enough, Just in Time

### Agile Documentation Principles

1. **Minimum Viable Documentation**: Create what's needed, when it's needed
2. **Living Documents**: Update docs as features evolve
3. **Docs-as-Code**: Store in Git, review in PRs
4. **Automate**: Generate docs from code (OpenAPI, class diagrams)

**Contrast with Waterfall:**
- ❌ Waterfall: Write comprehensive docs upfront → Code → Docs become stale
- ✅ Agile: Write minimal docs → Code → Update docs in same PR → Docs stay fresh

---

## 8.2 Documentation in the Definition of Done

**Example Definition of Done (DoD):**
- [ ] Code is written and reviewed
- [ ] Unit tests pass (>80% coverage)
- [ ] Integration tests pass
- [ ] **API endpoints are documented in OpenAPI spec**
- [ ] **User-facing changes are documented in KB**
- [ ] **Architecture decisions are recorded in ADRs**
- [ ] Code is deployed to staging

**Key Insight**: Documentation is not a separate phase; it's part of "done."

---

## 8.3 Tools and Workflow

### Documentation Tools

| Doc Type | Tool | Why |
|----------|------|-----|
| Developer docs (SDD, API) | Markdown + Git | Version control, code review |
| Requirements (PRD, SRS) | Confluence/Notion | Collaborative editing, comments |
| API docs | OpenAPI + Swagger UI | Interactive, auto-generated |
| User docs | Zendesk/Intercom | Searchable, analytics |
| Architecture docs | Markdown + Mermaid/PlantUML | Diagrams as code |

### CI/CD Integration

**Automate Documentation:**
1. **Generate OpenAPI from code**:
   - Spring Boot: Springdoc
   - FastAPI: Built-in
   - Express: swagger-jsdoc

2. **Lint markdown**:
   ```bash
   markdownlint docs/
   ```

3. **Deploy docs to static site**:
   - Tools: Docusaurus, MkDocs, GitBook
   - Trigger: On every commit to `main`

4. **Fail builds if OpenAPI diverges from code**:
   - Compare generated OpenAPI with committed spec
   - Fail CI if differences found

**Example GitHub Actions Workflow:**
```yaml
name: Documentation CI

on: [push, pull_request]

jobs:
  docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Lint Markdown
        run: markdownlint docs/

      - name: Generate OpenAPI
        run: npm run generate:openapi

      - name: Check OpenAPI up-to-date
        run: git diff --exit-code docs/api/openapi.yaml

      - name: Build documentation site
        run: |
          cd docs
          npm install
          npm run build

      - name: Deploy to GitHub Pages
        if: github.ref == 'refs/heads/main'
        run: npm run deploy
```

---

## 8.4 Documentation Debt

Like technical debt, **documentation debt** accumulates when:
- Docs are not updated with code changes
- Features ship without documentation
- Outdated docs are not deleted

**Managing Documentation Debt:**
1. **Track in backlog**: Create tickets for missing/outdated docs
2. **Allocate time**: 10-20% of sprint capacity for docs
3. **Quarterly reviews**: Audit and prune dead documentation
4. **Make it visible**: Dashboard showing docs coverage (% of APIs documented)

---

**End of Agile Documentation Process Guide**
