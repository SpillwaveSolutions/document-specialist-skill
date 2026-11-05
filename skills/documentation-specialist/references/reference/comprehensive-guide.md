# Modern Software Development Documentation: Navigation Guide

---
TOKEN_BUDGET: 150
TIER: 3
LOAD_TRIGGER: On-demand as navigation/index to all reference guides
DEPENDENCIES: All 01-10 reference files
---

## Overview

This guide has been split into focused, small files following Progressive Disclosure Architecture (PDA) principles. Each file is ~150-400 tokens for efficient loading.

**Total Files**: 28 focused guides organized into 10 sections

---

## 📚 Complete Reference Guide Index

### 1. Documentation Philosophy

**Core Principles** (~190 tokens):
- [01-philosophy.md](01-philosophy.md) - Docs-as-code, living documentation, MVD, three audiences

---

### 2. Requirements and Use Cases

**Requirements Documentation** (~650 tokens total):
- [02-requirements-srs-vs-prd.md](02-requirements-srs-vs-prd.md) - SRS vs PRD, risk-based approach (~200 tokens)
- [02-requirements-writing.md](02-requirements-writing.md) - Atomic requirements, user stories, acceptance criteria (~250 tokens)
- [02-requirements-traceability.md](02-requirements-traceability.md) - Traceability matrices, system context diagrams (~200 tokens)

---

### 3. Design and Architecture

**Architecture Documentation** (~730 tokens total):
- [03-design-arc42.md](03-design-arc42.md) - arc42 template, 12 sections, C4 integration (~280 tokens)
- [03-design-adrs.md](03-design-adrs.md) - Architecture Decision Records, template, best practices (~300 tokens)
- [03-design-requirements-matrix.md](03-design-requirements-matrix.md) - Mapping requirements to design (~150 tokens)

---

### 4. Diagrams and Visual Modeling

**Diagram Selection and Creation** (~770 tokens total):
- [04-diagrams-selection.md](04-diagrams-selection.md) - Decision matrix, common scenarios (~220 tokens)
- [04-diagrams-state-vs-activity.md](04-diagrams-state-vs-activity.md) - State machine vs activity diagrams (~350 tokens)
- [04-diagrams-c4-hierarchy.md](04-diagrams-c4-hierarchy.md) - C4 model levels 1-4 (~200 tokens)

---

### 5. API Documentation

**API Documentation Standards** (~760 tokens total):
- [05-api-stripe-gold-standard.md](05-api-stripe-gold-standard.md) - Stripe's best practices (~180 tokens)
- [05-api-openapi.md](05-api-openapi.md) - OpenAPI 3.x specification, examples (~380 tokens)
- [05-api-checklist.md](05-api-checklist.md) - API documentation checklist (~200 tokens)

---

### 6. Deployment and Operations

**Deployment Documentation** (~910 tokens total):
- [06-deployment-documentation.md](06-deployment-documentation.md) - Structure, configuration, monitoring (~380 tokens)
- [06-deployment-diagrams.md](06-deployment-diagrams.md) - UML deployment diagrams (~250 tokens)
- [06-deployment-runbooks.md](06-deployment-runbooks.md) - Runbook template, operational procedures (~280 tokens)

---

### 7. User Documentation

**User-Facing Documentation** (~670 tokens total):
- [07-user-kb-approach.md](07-user-kb-approach.md) - Knowledge base vs manuals, modern KB features (~200 tokens)
- [07-user-writing-style.md](07-user-writing-style.md) - Plain language, visual content, accessibility (~220 tokens)
- [07-user-kb-template.md](07-user-kb-template.md) - KB article template, metadata, quality checklist (~250 tokens)

---

### 8. Agile Documentation Process

**Agile Workflows** (~280 tokens total):
- [08-agile-process.md](08-agile-process.md) - Just-in-time docs, DoD, CI/CD integration, documentation debt (~280 tokens)

---

### 9. Code-to-Documentation Reverse Engineering

**Brownfield Documentation** (~730 tokens total):
- [09-code-to-docs-when.md](09-code-to-docs-when.md) - Use cases, ROI calculation (~150 tokens)
- [09-code-to-docs-detection.md](09-code-to-docs-detection.md) - Framework detection patterns (~200 tokens)
- [09-code-to-docs-workflow.md](09-code-to-docs-workflow.md) - 7-step extraction process (~180 tokens)
- [09-code-to-docs-example.md](09-code-to-docs-example.md) - Spring Boot to OpenAPI example (~200 tokens)

---

### 10. Quality and Maintenance

**Documentation Quality** (~620 tokens total):
- [10-quality-checklist.md](10-quality-checklist.md) - Quality checklist for all doc types (~220 tokens)
- [10-quality-bonsai-pruning.md](10-quality-bonsai-pruning.md) - Pruning dead docs, deletion mandate (~180 tokens)
- [10-quality-metrics.md](10-quality-metrics.md) - Health metrics, process metrics, dashboard (~220 tokens)

---

## 🎯 Quick Navigation by Use Case

**I need to...**

| Task | Start Here |
|------|-----------|
| Understand documentation philosophy | [01-philosophy.md](01-philosophy.md) |
| Create requirements (SRS/PRD) | [02-requirements-srs-vs-prd.md](02-requirements-srs-vs-prd.md) |
| Write good requirements | [02-requirements-writing.md](02-requirements-writing.md) |
| Document architecture | [03-design-arc42.md](03-design-arc42.md) |
| Record architectural decisions | [03-design-adrs.md](03-design-adrs.md) |
| Choose the right diagram | [04-diagrams-selection.md](04-diagrams-selection.md) |
| Understand state vs activity diagrams | [04-diagrams-state-vs-activity.md](04-diagrams-state-vs-activity.md) |
| Create C4 diagrams | [04-diagrams-c4-hierarchy.md](04-diagrams-c4-hierarchy.md) |
| Document an API | [05-api-stripe-gold-standard.md](05-api-stripe-gold-standard.md) |
| Write OpenAPI specs | [05-api-openapi.md](05-api-openapi.md) |
| Audit API documentation | [05-api-checklist.md](05-api-checklist.md) |
| Document deployment | [06-deployment-documentation.md](06-deployment-documentation.md) |
| Create deployment diagrams | [06-deployment-diagrams.md](06-deployment-diagrams.md) |
| Write runbooks | [06-deployment-runbooks.md](06-deployment-runbooks.md) |
| Create user documentation | [07-user-kb-approach.md](07-user-kb-approach.md) |
| Write user-friendly content | [07-user-writing-style.md](07-user-writing-style.md) |
| Create KB articles | [07-user-kb-template.md](07-user-kb-template.md) |
| Set up agile docs process | [08-agile-process.md](08-agile-process.md) |
| Document existing code | [09-code-to-docs-when.md](09-code-to-docs-when.md) |
| Detect framework/tech stack | [09-code-to-docs-detection.md](09-code-to-docs-detection.md) |
| Extract docs from code | [09-code-to-docs-workflow.md](09-code-to-docs-workflow.md) |
| Audit documentation quality | [10-quality-checklist.md](10-quality-checklist.md) |
| Clean up old documentation | [10-quality-bonsai-pruning.md](10-quality-bonsai-pruning.md) |
| Measure documentation health | [10-quality-metrics.md](10-quality-metrics.md) |

---

## 📊 Token Budget Summary

| Section | Files | Total Tokens |
|---------|-------|--------------|
| 1. Philosophy | 1 | ~190 |
| 2. Requirements | 3 | ~650 |
| 3. Design | 3 | ~730 |
| 4. Diagrams | 3 | ~770 |
| 5. API Docs | 3 | ~760 |
| 6. Deployment | 3 | ~910 |
| 7. User Docs | 3 | ~670 |
| 8. Agile Process | 1 | ~280 |
| 9. Code-to-Docs | 4 | ~730 |
| 10. Quality | 3 | ~620 |
| **Total** | **27** | **~6,310** |

**Average per file**: ~234 tokens

**PDA Compliance**: ✅ All files <500 tokens, load on-demand

---

## 🗂️ Original Archive

The original monolithic comprehensive-guide.md (846 lines, ~4,230 tokens) has been archived as:
- `comprehensive-guide.md.backup`

---

## 🔄 Version History

**v2.0-PDA** (2025-01-14):
- Split monolithic guide into 27 focused files
- Achieved PDA compliance (<500 tokens per file)
- Organized by topic for on-demand loading
- Added navigation index and quick reference

**v1.0** (2025-01-13):
- Original comprehensive guide (single file)

---

**End of Navigation Guide**
