# Documentation Philosophy

---
TOKEN_BUDGET: 190
TIER: 3
LOAD_TRIGGER: On-demand when creating any type of documentation
DEPENDENCIES: None
---

## Overview

This guide covers the fundamental philosophy behind effective software documentation: docs-as-code, living documentation, and minimum viable documentation.

---

## 1.1 Living Documentation: The Docs-as-Code Mandate

The most critical failure of traditional documentation is **staleness**. A document that is out of date is worse than no document at all—it actively misleads developers and stakeholders.

**The Bonsai Tree Principle**: Documentation should be "alive but frequently trimmed, like a bonsai tree". Teams must have a culture of "deleting dead documentation" as a continuous process.

**Key Practice:** "Change your documentation in the same commit as the code change." A pull request that adds a new API endpoint must also include the changes to the OpenAPI specification.

---

## 1.2 Minimum Viable Documentation (MVD)

"A small set of fresh and accurate docs is better than a large assembly of 'documentation' in various states of disrepair."

**Focus on:**
- Short, useful documents that are essential for the target audience
- Documents that answer specific questions
- Documentation that reduces support burden

**Avoid:**
- Exhaustive "complete" documentation that becomes unmaintainable
- Documentation that duplicates what the code already expresses
- Over-engineered documentation processes

---

## 1.3 The Three Core Audiences

Documentation is not one-size-fits-all. The content, style, and location depend on **who will be reading it**:

| Audience | Focus | Documents |
|----------|-------|-----------|
| **Stakeholders** | Why & What | PRD, SRS, Use Cases |
| **Developers** | How | SDD, arc42, API Docs, Deployment Docs |
| **End-Users** | How-To | User Guides, KB Articles, Help Centers |

**Critical:** Don't try to force all documentation into a single tool. Developers won't look for API specs where customers look for how-to guides.

---

**End of Documentation Philosophy Guide**
