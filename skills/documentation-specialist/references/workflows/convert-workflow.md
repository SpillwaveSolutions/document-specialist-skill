# Format Conversion Workflow

---
TOKEN_BUDGET: 250
TIER: 2
LOAD_TRIGGER: Intent = CONVERT
DEPENDENCIES: SKILL.md
---

## Overview

Convert documentation between Markdown, DOCX, and PDF formats.

## Workflow Steps

### Step 1: Identify Formats

| Request | Source | Target | Skill |
|---------|--------|--------|-------|
| "Convert to Word" | MD | DOCX | docx |
| "Generate PDF" | MD | PDF | pdf |
| "Convert to markdown" | DOCX | MD | docx |
| "PDF package" | Multiple | PDF | pdf |

### Step 2: Validate Source

For Markdown → DOCX/PDF:
- Check heading hierarchy (H1 → H2 → H3)
- Verify internal links
- Ensure tables are well-formed

### Step 3: Invoke Skill

**Markdown → DOCX**:
```
Skill: docx
Source: [file path]
Styling: Professional template
  - TOC, heading styles, page numbers
```

**Markdown → PDF**:
```
Skill: pdf
Source: [file path]
Options: Page size, margins, syntax highlighting
```

**Multi-Document PDF**:
```
Skill: pdf
Sources: docs/**/*.md
Options: Combined PDF with bookmarks, cover page
```

### Step 4: Verify & Present Options

After conversion, present options to user:
```
Converted [source] to [target]: [output path]

Options:
1. Generate additional formats
2. Convert other documents
3. Create complete documentation package
```

## Quick Reference

| Task | Skill |
|------|-------|
| MD → DOCX | docx |
| MD → PDF | pdf |
| DOCX → MD | docx |
| Multi-doc PDF | pdf |
