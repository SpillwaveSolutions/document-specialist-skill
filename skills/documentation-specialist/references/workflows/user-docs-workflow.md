# User Documentation Workflow

---
TOKEN_BUDGET: 300
TIER: 2
LOAD_TRIGGER: Intent = CREATE_USER_DOCS
DEPENDENCIES: SKILL.md
---

## Overview

Create user-facing documentation for end-users (not developers).

**Supported**: User Manuals, How-To Guides, KB Articles, Getting Started Guides

## Workflow Steps

### Step 1: Identify Document Type

| Keywords | Type | Template |
|----------|------|----------|
| "user manual", "user guide" | User Manual | templates/markdown/user-manual.md |
| "how-to", "step-by-step" | How-To Guide | templates/markdown/howto-guide.md |
| "getting started", "quick start" | Getting Started | templates/markdown/getting-started.md |

### Step 2: Load Template

Read template and reference if needed:
- User writing style: [07-user-writing-style.md](../reference/07-user-writing-style.md)
- Example: [taskmanager-user-manual.md](../examples/greenfield/taskmanager-user-manual.md)

### Step 3: Gather Context

Extract from user request:
1. **Product name** - Subject of documentation
2. **Target audience** - Technical level, job role
3. **Key tasks** - Tasks users need to accomplish
4. **Prerequisites** - Account, setup, permissions

### Step 4: Generate Content

**User Manual Structure**:
1. Introduction & Overview
2. Getting Started
3. Feature Guides (task-oriented chapters)
4. Troubleshooting
5. FAQ
6. Glossary

**How-To Guide Structure**:
1. Goal (what you'll accomplish)
2. Prerequisites
3. Step-by-step instructions (numbered)
4. Expected result
5. Troubleshooting

**Getting Started Structure**:
1. Introduction (30 seconds)
2. Prerequisites
3. Installation/Setup (2 minutes)
4. First task (2 minutes)
5. Next steps

### Step 5: Apply Writing Best Practices

- **Plain language**: 8th-grade reading level
- **Active voice**: "Click the button" not "The button should be clicked"
- **Short paragraphs**: 2-4 sentences max
- **Visual aids**: Screenshots for complex steps
- **Scannable**: Headers, bullets, numbered lists

### Step 6: Format & Save

Save to: `docs/user/{product}-{doc-type}.md`

Present options to user:
1. Convert to PDF
2. Add screenshots
3. Create related how-to guides

## Quality Checklist

- [ ] Clear, descriptive title
- [ ] Prerequisites listed
- [ ] Steps numbered (for procedures)
- [ ] Screenshots for complex steps
- [ ] Troubleshooting section
- [ ] Glossary for technical terms
