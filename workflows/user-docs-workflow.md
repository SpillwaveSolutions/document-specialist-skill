# User Documentation Workflow

---
TOKEN_BUDGET: 1200
TIER: 3
LOAD_TRIGGER: Intent = CREATE_USER_DOCS (create user manuals, how-to guides, KB articles)
DEPENDENCIES: SKILL.md, templates/markdown/user-*.md, reference/08-tutorial-writing.md
---

## Overview

This workflow guides the creation of user-facing documentation including user manuals, how-to guides, knowledge base articles, and getting started guides. Use this when the user wants to create documentation for end-users (not developers).

**Supported Document Types:**
- **User Manuals**: Comprehensive reference for product features and functionality
- **How-To Guides**: Task-oriented instructions for specific procedures
- **KB Articles**: Knowledge base articles for troubleshooting and common questions
- **Getting Started**: Quick onboarding guides for new users

**Token Budget**: This workflow consumes ~1,200 tokens. Load only when intent is CREATE_USER_DOCS.

---

## Workflow Steps

### Step 1: Identify User Documentation Type

Based on user request, classify the document type:

| Keywords in Request | Document Type | Template | Use Case |
|---------------------|---------------|----------|----------|
| "user manual", "user guide", "handbook" | User Manual | templates/markdown/user-manual.md | Comprehensive reference, features, procedures |
| "how-to", "how do I", "step-by-step" | How-To Guide | templates/markdown/howto-guide.md | Task-oriented, single procedure |
| "KB article", "knowledge base", "support" | KB Article | templates/markdown/kb-article.md | Troubleshooting, FAQ, common issues |
| "getting started", "quick start", "onboarding" | Getting Started | templates/markdown/getting-started.md | 5-minute setup, first-time users |

### Step 2: Load Template and Reference Guide

**For User Manuals**:
- Template: `templates/markdown/user-manual.md`
- Reference: `reference/08-tutorial-writing.md` (User Documentation section)
- Example: `examples/greenfield/taskmanager-user-manual.md`

**For How-To Guides**:
- Template: `templates/markdown/howto-guide.md`
- Reference: `reference/08-tutorial-writing.md` (How-To Guides section)

**For Getting Started Guides**:
- Template: `templates/markdown/getting-started.md`
- Example: `examples/greenfield/cli-getting-started.md`

### Step 3: Gather User Context

**Essential Information to Collect**:

1. **Product/Feature Overview**:
   - What product/feature are we documenting?
   - Who is the target audience? (technical level, role)
   - What problem does this solve for users?

2. **Key Features/Tasks**:
   - What are the main features users need to learn?
   - What are the most common tasks users will perform?
   - What are the prerequisites? (account, installation, setup)

3. **Existing Materials**:
   - Is there existing code/UI to reference?
   - Are there screenshots or videos available?
   - Is there existing documentation to update/replace?

4. **Tone and Style**:
   - Formal or friendly tone?
   - Any specific terminology or brand voice guidelines?
   - Accessibility requirements? (WCAG, multilingual)

**If context is missing**: Use AskUserQuestion to gather required details.

### Step 4: Customize Template with User's Context

**Apply Template-Specific Customization**:

**User Manual Structure**:
1. **Introduction** (What & Why):
   - Product overview
   - Target audience
   - Document scope and purpose

2. **Getting Started** (Quick Win):
   - Prerequisites
   - Installation/Setup (5 minutes max)
   - First successful use

3. **Features Reference** (Modular):
   - Each feature in its own section
   - Task-oriented organization
   - Visual aids (screenshots, diagrams)

4. **Troubleshooting & FAQ**:
   - Common issues and solutions
   - Error message explanations
   - Support contact information

**How-To Guide Structure**:
1. **Problem Statement**: What task will this accomplish?
2. **Prerequisites**: What do you need before starting?
3. **Step-by-Step Instructions**: Numbered, actionable steps
4. **Visual Aids**: Screenshot or diagram per key step
5. **Verification**: How to confirm success
6. **Related Guides**: Links to next steps or alternatives

**Getting Started Structure**:
1. **Project Introduction**: What is this? Why use it?
2. **Quick Start**: 5-minute setup (copy-paste commands)
3. **Core Concepts**: Key terminology and principles
4. **Next Steps**: Links to detailed guides
5. **FAQ**: Common first-time user questions

### Step 5: Apply Best Practices

**Structure & Organization**:
- ✅ Use clear, descriptive headings (H2, H3 hierarchy)
- ✅ Keep paragraphs short (2-4 sentences max)
- ✅ Use numbered lists for procedures, bullets for options
- ✅ Modular sections (each can stand alone)

**Tone & Language**:
- ✅ Write in second person ("you") for direct engagement
- ✅ Use active voice ("Click Save" not "Save is clicked")
- ✅ Define jargon on first use or link to glossary
- ✅ Friendly but professional tone
- ✅ Explain "why" not just "how"

**Visual Aids**:
- ✅ Screenshot for every UI interaction
- ✅ Annotate images (arrows, highlights, callouts)
- ✅ Alt text for all images (accessibility)
- ✅ Diagrams for complex workflows
- ✅ Consistent visual style

**Examples & Clarity**:
- ✅ Provide realistic examples
- ✅ Show expected output/results
- ✅ Highlight common mistakes
- ✅ Use callouts for tips, warnings, notes

**Accessibility**:
- ✅ WCAG-compliant (headings, alt text, color contrast)
- ✅ Keyboard navigation described
- ✅ Avoid relying on color alone ("red button" → "Cancel button (red)")

### Step 6: Add Visual Documentation

**When to Generate Diagrams**:
- **User Manual**: System context diagram (C4), feature flowchart
- **How-To Guide**: Process flowchart, decision tree
- **Getting Started**: Installation flowchart, architecture overview

**Diagram Generation**:
1. Invoke mermaid-architect skill for flowcharts and simple diagrams
2. Use PlantUML for activity diagrams showing user workflows

**Screenshot Guidelines**:
- Capture entire relevant UI section (not just button)
- Use consistent resolution and zoom level
- Add annotations with arrows/highlights
- Save in web-friendly format (PNG, WebP)
- Include alt text in markdown: `![Alt text describing action](image.png)`

### Step 7: Review Quality Checklist

**All User Documentation Must Have**:
- [ ] Clear, task-oriented title
- [ ] Version number and last updated date
- [ ] Prerequisites section (if any)
- [ ] Step-by-step instructions (if procedural)
- [ ] Visual aids (screenshots/diagrams)
- [ ] Verification/success criteria
- [ ] Troubleshooting or FAQ section
- [ ] Contact/support information
- [ ] No jargon without definition
- [ ] Consistent formatting and tone

**Usability Test**:
- Can a new user complete the task without prior knowledge?
- Are all steps clear and unambiguous?
- Are all screenshots current and accurate?
- Does the document answer "what," "why," and "how"?

### Step 8: Generate Output

**Markdown Output** (Primary):
- Save as `.md` file
- Include table of contents for documents > 3 pages
- Use proper heading hierarchy
- Include metadata (version, date, author)

**Optional Format Conversion**:
- **DOCX**: Invoke `docx` skill for professional Word format
- **PDF**: Invoke `pdf` skill for distribution-ready document
- **HTML**: For web knowledge base (ask user if needed)

**Output Location**:
- Save to `docs/user-docs/` (create if needed)
- Use descriptive filename: `product-name-user-manual.md`

---

## Common Patterns

### Pattern 1: SaaS Product User Manual
```markdown
# ProductName User Manual

## Introduction
Brief overview, target audience, scope.

## Getting Started
1. Sign up for account
2. Verify email
3. Complete profile setup

## Features
### Feature 1: Dashboard
- What it does
- How to use it
- Screenshot

### Feature 2: Reports
- What it does
- How to use it
- Screenshot

## Troubleshooting
Common issues and solutions

## Support
Contact information
```

### Pattern 2: Task-Oriented How-To Guide
```markdown
# How to Export Data from ProductName

**Problem**: You need to download your data in CSV format.

## Prerequisites
- Active account
- Data export permission

## Steps
1. Navigate to Settings > Data Export
   ![Settings menu](images/settings.png)
2. Select date range
3. Choose CSV format
4. Click "Export"
   ![Export button](images/export.png)
5. Download file from Downloads page

## Verification
You should see a CSV file in your downloads folder with format `export-YYYY-MM-DD.csv`.

## Troubleshooting
- **No data in export**: Check date range covers period with data
- **Export failed**: Try smaller date range

## Related Guides
- [How to Import Data](#)
- [Understanding Data Formats](#)
```

### Pattern 3: Getting Started Guide
```markdown
# Getting Started with CLI-Tool

## Introduction
CLI-Tool is a command-line utility for [purpose]. This guide will get you up and running in under 5 minutes.

## Quick Start
1. **Install**:
   ```bash
   npm install -g cli-tool
   ```
2. **Configure**:
   ```bash
   cli-tool init
   ```
3. **Run**:
   ```bash
   cli-tool start
   ```

## Core Concepts
- **Project**: A workspace for your files
- **Config**: Settings stored in `.cli-toolrc`

## Next Steps
- [CLI Command Reference](#)
- [Tutorial: Build Your First Project](#)

## FAQ
**Q: Where is my config file?**
A: Located at `~/.cli-toolrc`
```

---

## Error Handling

**Issue**: User doesn't specify what product/feature to document
**Solution**: Use AskUserQuestion to gather: product name, target audience, main features

**Issue**: No visual aids available (no screenshots)
**Solution**: Create placeholder sections with instructions for what screenshots to add later

**Issue**: Unclear audience (technical vs non-technical)
**Solution**: Default to beginner-friendly tone, ask user to clarify if needed

---

## Integration with Other Workflows

- **Brownfield Code-to-Docs**: Generate API usage guides from OpenAPI specs
- **Diagram Workflow**: Create flowcharts for complex procedures
- **Convert Workflow**: Export to DOCX/PDF for offline distribution

---

## Success Criteria

✅ Document passes usability test (can new user complete task?)
✅ All visual aids present and annotated
✅ Accessibility compliant (WCAG)
✅ Consistent tone and formatting throughout
✅ No unexplained jargon or acronyms
✅ FAQ/Troubleshooting addresses common questions

**User documentation is effective when users can accomplish their goals without asking for help.**
