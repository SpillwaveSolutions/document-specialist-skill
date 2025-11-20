# Format Conversion Workflow

---
TOKEN_BUDGET: 750
TIER: 3
LOAD_TRIGGER: Intent = CONVERT (transform between formats)
DEPENDENCIES: SKILL.md
---

## Overview

This workflow guides format conversion between Markdown, DOCX, and PDF. Use this when the user wants to convert documentation between formats while preserving structure and professional styling.

**Supported Conversions:**
- Markdown → DOCX (Word)
- Markdown → PDF
- DOCX → Markdown
- Any format → PDF (documentation package)

**Token Budget**: This workflow consumes ~750 tokens. Load only when intent is CONVERT.

---

## Workflow Steps

### Step 1: Identify Source and Target Formats

**Parse user request:**

| Request Pattern | Source | Target | Skill to Invoke |
|----------------|--------|--------|-----------------|
| "Convert [file].md to Word", "Generate DOCX from markdown" | MD | DOCX | docx |
| "Convert [file].md to PDF", "Create PDF from markdown" | MD | PDF | pdf |
| "Convert [file].docx to markdown" | DOCX | MD | docx |
| "Generate PDF package from all docs" | Multiple | PDF | pdf |

### Step 2: Prepare Source Document

**For Markdown → DOCX/PDF:**

1. **Validate Markdown**:
   - Check for proper heading hierarchy (H1 → H2 → H3)
   - Verify all internal links are valid
   - Ensure code blocks have language tags
   - Check for malformed tables

2. **Pre-process if needed**:
   - Add missing table of contents
   - Fix heading levels
   - Add page breaks before major sections (for PDF)

**For DOCX → Markdown:**

1. **Read DOCX structure**:
   - Extract heading styles (Heading 1, Heading 2, etc.)
   - Preserve tables and lists
   - Convert images to embedded or linked

### Step 3: Invoke Appropriate Skill

#### For Markdown → DOCX

**Invoke docx skill:**

```
Skill: docx
Task: Convert markdown to professionally styled Word document
Source: [file path]
Styling requirements:
  - Title: Heading 1 (18pt, bold, blue)
  - Headings: Heading 2-6 hierarchy
  - Code blocks: Courier New font, gray background
  - Tables: Professional grid style
  - Page numbers: Footer, centered
  - Table of contents: Auto-generated
```

**Pass to docx skill**:
- Source file path
- Desired styling template (default or custom)
- Output file path

#### For Markdown → PDF

**Invoke pdf skill:**

```
Skill: pdf
Task: Convert markdown to PDF with professional layout
Source: [file path]
Formatting:
  - Page size: Letter (8.5" x 11")
  - Margins: 1" all sides
  - Header: Document title
  - Footer: Page numbers
  - Font: Times New Roman (body), Arial (headings)
  - Syntax highlighting: Code blocks
```

**Pass to pdf skill**:
- Source file path
- Styling options
- Output file path

#### For DOCX → Markdown

**Invoke docx skill:**

```
Skill: docx
Task: Convert Word document to markdown
Source: [file path]
Conversion rules:
  - Heading 1 → # Markdown H1
  - Heading 2 → ## Markdown H2
  - Tables → Markdown tables
  - Images → Extract and link
  - Lists → Markdown bullets/numbers
```

#### For Multi-Document PDF Package

**Invoke pdf skill:**

```
Skill: pdf
Task: Generate PDF documentation package
Sources: [list of all markdown files]
  - docs/requirements/*.md
  - docs/design/*.md
  - docs/api/*.md
Options:
  - Combine into single PDF with bookmarks
  - Or: Generate separate PDFs in docs/pdf/
  - Include table of contents
  - Add cover page with project name, version, date
```

### Step 4: Verify Output Quality

**For DOCX output:**
- [ ] Table of contents generated
- [ ] Heading styles applied consistently
- [ ] Code blocks formatted with monospace font
- [ ] Tables properly aligned
- [ ] Page breaks before major sections
- [ ] Images embedded or linked correctly

**For PDF output:**
- [ ] All pages rendered correctly
- [ ] Headings in table of contents/bookmarks
- [ ] Code blocks with syntax highlighting
- [ ] Page numbers present
- [ ] No text cutoff or overlapping

**For Markdown output:**
- [ ] Heading hierarchy preserved
- [ ] Tables converted to markdown format
- [ ] Lists (bullets, numbers) formatted correctly
- [ ] Code blocks with language tags
- [ ] Internal links working

### Step 5: Offer Additional Conversions

After successful conversion:

```
I've converted [source file] to [target format]: [output file path]

Would you like me to:
1. Generate additional formats (e.g., PDF from the DOCX)?
2. Convert other related documents?
3. Create a complete documentation package with all formats?
4. Customize the styling/formatting?
```

---

## Example 1: Markdown SRS to Word

**User Request:**
```
Convert docs/requirements/billing-srs.md to Word format
```

**Workflow Execution:**

### Step 1: Identify Formats
```
Source: Markdown (docs/requirements/billing-srs.md)
Target: DOCX (Microsoft Word)
```

### Step 2: Prepare Source
```
Read: docs/requirements/billing-srs.md
Validate:
  ✅ Proper heading hierarchy (H1 → H2 → H3)
  ✅ All internal links valid
  ✅ Tables well-formed
```

### Step 3: Invoke docx Skill
```
Skill: docx
Task: Convert markdown to Word
Source: docs/requirements/billing-srs.md
Output: docs/requirements/billing-srs.docx
Styling: IEEE-compliant SRS template
  - Cover page with document metadata
  - Table of contents (auto-generated)
  - Heading 1: 18pt Arial Bold Blue
  - Heading 2: 16pt Arial Bold Black
  - Body: 12pt Times New Roman
  - Code blocks: 10pt Courier New, gray background
  - Tables: Professional grid
  - Page numbers: Bottom center
  - Headers: Document title (top left), version (top right)
```

### Step 4: Verify Output
```
Check: docs/requirements/billing-srs.docx
✅ Table of contents on page 2
✅ Heading styles consistent
✅ Requirements traceability matrix table formatted
✅ Page breaks before major sections
```

### Step 5: Offer Additional Conversions
```
I've converted docs/requirements/billing-srs.md to Word format:
→ docs/requirements/billing-srs.docx

Would you like me to:
1. Generate a PDF version as well?
2. Convert other requirements documents?
3. Create a requirements documentation package (all formats)?
```

---

## Example 2: Generate PDF Documentation Package

**User Request:**
```
Create a PDF documentation package from all markdown documentation
```

**Workflow Execution:**

### Step 1: Identify Sources
```
Glob: docs/**/*.md
Found:
  - docs/requirements/billing-srs.md
  - docs/requirements/task-management-prd.md
  - docs/design/ecommerce-api-sdd.md
  - docs/api/ecommerce-openapi.yaml (skip - not markdown)
  - docs/user/user-guide.md
Target: PDF package
```

### Step 2: Organize Documents
```
Group by category:
  Requirements:
    - billing-srs.md
    - task-management-prd.md
  Design:
    - ecommerce-api-sdd.md
  User Documentation:
    - user-guide.md
```

### Step 3: Invoke pdf Skill
```
Skill: pdf
Task: Generate combined PDF documentation package
Options:
  - Combine all documents into single PDF
  - Add cover page with:
    - Project: E-Commerce Platform
    - Version: 2.0
    - Date: 2025-01-13
  - Generate table of contents with bookmarks
  - Page numbering: Roman numerals (i, ii, iii) for TOC, Arabic (1, 2, 3) for content
Output: docs/pdf/ecommerce-documentation-v2.0.pdf
```

### Step 4: Verify Output
```
Check: docs/pdf/ecommerce-documentation-v2.0.pdf
✅ Cover page with project metadata
✅ Table of contents with page numbers
✅ Bookmarks for navigation
✅ All 4 documents included (32 pages total)
✅ Page numbers formatted correctly
```

### Step 5: Offer Additional Options
```
I've created a PDF documentation package:
→ docs/pdf/ecommerce-documentation-v2.0.pdf (32 pages)

Includes:
- Billing SRS (12 pages)
- Task Management PRD (8 pages)
- E-Commerce API SDD (10 pages)
- User Guide (2 pages)

Would you like me to:
1. Generate separate PDFs for each document?
2. Add the OpenAPI spec (as appendix)?
3. Include diagrams from docs/diagrams/?
```

---

## Integration with docx and pdf Skills

**docx Skill Capabilities:**
- Markdown → DOCX with professional styling
- DOCX → Markdown conversion
- Custom Word templates
- Heading styles, fonts, spacing
- Table of contents generation
- Header/footer customization
- Image embedding

**pdf Skill Capabilities:**
- Markdown → PDF with syntax highlighting
- DOCX → PDF conversion
- Multi-document PDF packages
- Cover pages and bookmarks
- Page numbering and headers/footers
- PDF merging and splitting
- PDF forms (if needed)

---

## Best Practices

1. **Always validate source before conversion**:
   - Check markdown syntax
   - Verify internal links
   - Ensure proper heading hierarchy

2. **Use appropriate styling**:
   - SRS/SDD: Formal IEEE-style
   - PRD: Modern, agile-friendly
   - User Guides: Clean, accessible

3. **Preserve structure**:
   - Maintain heading levels
   - Keep table formatting
   - Preserve code block highlighting

4. **Optimize for target format**:
   - PDF: Add page breaks, headers/footers
   - DOCX: Use Word styles (not direct formatting)
   - Markdown: Clean, simple formatting

5. **Test output**:
   - Open in target application
   - Check rendering on different devices
   - Verify all links and references

---

## Troubleshooting

**Issue: Tables not rendering correctly in PDF/DOCX**
- Solution: Simplify table structure, avoid nested tables

**Issue: Code blocks losing formatting**
- Solution: Specify language for syntax highlighting (```java, ```python)

**Issue: Images not showing in converted document**
- Solution: Use absolute paths or embed images

**Issue: Heading hierarchy broken after conversion**
- Solution: Fix markdown heading levels (must be sequential H1 → H2 → H3)

---

## Quick Reference

| Task | Skill | Command Example |
|------|-------|-----------------|
| MD → DOCX | docx | "Convert my SRS to Word format" |
| MD → PDF | pdf | "Generate PDF from my design document" |
| DOCX → MD | docx | "Convert this Word doc to markdown" |
| Multi-doc PDF | pdf | "Create PDF package from all documentation" |

---

**End of Convert Workflow Guide**
