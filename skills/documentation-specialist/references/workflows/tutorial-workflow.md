# Tutorial and Developer Guide Workflow

---
TOKEN_BUDGET: 300
TIER: 2
LOAD_TRIGGER: Intent = CREATE_TUTORIAL
DEPENDENCIES: SKILL.md
---

## Overview

Create developer-focused tutorials, API guides, and CLI documentation.

**Supported**: Developer Tutorials, API Usage Guides, CLI Documentation

## Workflow Steps

### Step 1: Identify Document Type

| Keywords | Type | Template |
|----------|------|----------|
| "tutorial", "walkthrough" | Developer Tutorial | templates/markdown/developer-tutorial.md |
| "API guide", "integration" | API Usage Guide | (use tutorial template) |
| "CLI docs", "command reference" | CLI Documentation | (use getting-started template) |

### Step 2: Load Template

Read template and reference if needed:
- Tutorial writing: [08-tutorial-writing.md](../reference/08-tutorial-writing.md)
- Example: [rest-api-tutorial.md](../examples/greenfield/rest-api-tutorial.md)

### Step 3: Gather Context

Extract from user request:
1. **Topic** - Technology/API/tool being covered
2. **Goal** - What reader will build or learn
3. **Audience** - Beginner/intermediate/advanced level
4. **Prerequisites** - Languages, tools, accounts needed

### Step 4: Generate Content

**Developer Tutorial Structure**:
1. Introduction (what you'll build)
2. Prerequisites
3. Project setup
4. Step-by-step implementation (with code)
5. Testing
6. Conclusion & next steps

**API Usage Guide Structure**:
1. Overview (what the API does)
2. Authentication setup
3. Making your first request
4. Common use cases (with code examples)
5. Error handling
6. Reference to full API docs

**CLI Documentation Structure**:
1. Installation
2. Basic usage
3. Command reference (alphabetical)
4. Configuration
5. Examples

### Step 5: Apply Tutorial Best Practices

- **Working code**: Every example must run
- **Progressive complexity**: Build on previous steps
- **Explain the "why"**: Not just "what" to do
- **Multiple languages**: Python, JavaScript, curl examples
- **Copy-pasteable**: Code blocks with language tags

### Step 6: Format & Save

Save to: `docs/tutorials/{topic}-tutorial.md`

Present options to user:
1. Generate Jupyter notebook version
2. Create video script
3. Add more code examples

## Quality Checklist

- [ ] Clear learning objective
- [ ] Prerequisites listed
- [ ] All code examples tested
- [ ] Language tags on code blocks
- [ ] Progressive difficulty
- [ ] Next steps provided
