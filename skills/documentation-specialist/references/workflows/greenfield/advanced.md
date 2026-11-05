# Advanced Greenfield Topics

---
TOKEN_BUDGET: 200
TIER: 3
LOAD_TRIGGER: Multi-project, documentation packages, continuous docs
DEPENDENCIES: greenfield-workflow.md
---

## Multi-Project Documentation

When documenting multiple projects in a directory:

1. **Discover projects**: `find . -name 'pom.xml' -o -name 'package.json'`
2. **Detect framework** for each project
3. **Generate individual docs** for each
4. **Create overview document** linking all projects
5. **Generate system-wide C4 context diagram**

Output structure:
```
docs/
├── overview.md           # Links to all project docs
├── c4-context.png        # System-wide diagram
├── service-a/
│   ├── srs.md
│   └── api.yaml
└── service-b/
    ├── srs.md
    └── api.yaml
```

## Documentation Packages

For release documentation packages:

1. Generate or update all document types:
   - SRS (if high-risk features)
   - PRD (for new features)
   - SDD (architecture)
   - API documentation
   - User guide
   - Deployment guide

2. Create all relevant diagrams

3. Convert to multiple formats (MD, DOCX, PDF)

4. Package in `docs-v{version}/` directory

5. Generate README index with links

## Custom Templates

To use a custom template:

```
Use my custom SRS template at templates/my-srs-template.md
```

Workflow:
1. Read custom template file
2. Identify placeholders in custom template
3. Apply same customization logic
4. Generate document using custom structure

## Continuous Documentation (Docs-as-Code)

Setup for CI/CD integration:

**Pre-commit hook**:
```bash
#!/bin/bash
# Validate documentation on commit
python scripts/validate-docs.py
```

**GitHub Actions**:
```yaml
- name: Validate Documentation
  run: |
    npm run docs:validate
    npm run docs:build
```

**Key principles**:
- Update docs in same commit as code
- Automated validation in CI
- Documentation review in PR process
- Keep docs close to code
