# Quality: The Bonsai Tree - Pruning Dead Documentation

---
TOKEN_BUDGET: 180
TIER: 3
LOAD_TRIGGER: On-demand when cleaning up or archiving documentation
DEPENDENCIES: 01-philosophy.md
---

## 10.2 The Bonsai Tree: Pruning Dead Documentation

**The Principle**: Documentation should be "alive but frequently trimmed, like a bonsai tree."

---

### Signs of Dead Documentation

**🚨 Delete or archive if:**
- [ ] Last updated > 1 year ago
- [ ] Describes features that no longer exist
- [ ] Contradicts current implementation
- [ ] Receives no views/searches (check analytics)
- [ ] Has "TODO" or "Coming Soon" sections
- [ ] References deprecated APIs or libraries
- [ ] No owner or maintainer identified

---

### The Deletion Mandate

**Out-of-date docs are worse than no docs.**

**Why?**
- Misleads developers
- Wastes time (following wrong instructions)
- Erodes trust in all documentation
- Creates confusion when contradicts code

**Action**: Delete it. Seriously.

---

### Deletion Process

**Step 1: Identify candidates**
- Run analytics: What docs get zero views?
- Check last-modified dates
- Survey team: "What docs are wrong?"

**Step 2: Classify**
- **Delete**: Outdated, no longer relevant
- **Archive**: Historical value, move to `/archive/`
- **Update**: Still relevant, needs refresh
- **Keep**: Fresh and accurate

**Step 3: Execute**
```bash
# Archive old docs
mv docs/legacy-v1-api.md docs/archive/

# Delete dead docs
rm docs/unused-feature.md

# Commit
git commit -m "docs: archive v1 API docs, delete unused feature docs"
```

**Step 4: Update navigation**
- Remove links from TOC
- Update internal references
- Add redirect if needed

---

### Annual Documentation Review

**Quarterly or Annual:**
1. **Inventory**: List all documentation
2. **Classify**: Active | Archive | Delete
3. **Update**: Refresh "Active" docs for accuracy
4. **Archive**: Move old versions to `/archive/`
5. **Delete**: Remove dead documentation
6. **Templates**: Update templates and guides

**Make it a ritual**: Block a day each quarter for "Documentation Spring Cleaning"

---

### Archive Strategy

**What to archive:**
- Old versions (API v1 docs when v3 is current)
- Deprecated features (still useful for legacy support)
- Historical decisions (old ADRs superseded by new ones)

**Where to archive:**
- `/docs/archive/` directory
- Mark clearly: "⚠️ ARCHIVED - For historical reference only"
- Include archive date and reason

---

**End of Bonsai Tree Pruning Guide**
