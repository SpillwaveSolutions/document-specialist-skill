# Quality: Documentation Metrics

---
TOKEN_BUDGET: 220
TIER: 3
LOAD_TRIGGER: On-demand when measuring documentation health or effectiveness
DEPENDENCIES: 10-quality-bonsai-pruning.md
---

## 10.3 Documentation Metrics

### Health Metrics

**1. Freshness**
- **Metric**: % of docs updated in last 6 months
- **Target**: >80%
- **How to measure**: Git commit dates, last-modified metadata

**2. Coverage**
- **Metric**: % of APIs/features with documentation
- **Target**: 100% of public APIs, 80% of features
- **How to measure**: Compare OpenAPI endpoints vs documented endpoints

**3. Accuracy**
- **Metric**: Issues reported due to doc errors
- **Target**: <5 issues per month
- **How to measure**: Support ticket categorization

**4. Findability**
- **Metric**: Average search result relevance
- **Target**: >90% searches find relevant results
- **How to measure**: Search analytics, "no results" rate

**5. Usefulness**
- **Metric**: "Was this helpful?" positive rate
- **Target**: >70%
- **How to measure**: Feedback widgets on docs pages

---

### Process Metrics

**1. Docs-as-Code**
- **Metric**: % of code PRs that include doc updates
- **Target**: >60%
- **How to measure**: GitHub PR analysis

**2. Review Coverage**
- **Metric**: % of docs that go through review
- **Target**: 100%
- **How to measure**: PR review requirements

**3. Automation**
- **Metric**: % of docs auto-generated from code
- **Target**: 80% of API docs
- **How to measure**: Count auto-generated vs manual docs

**4. Staleness Detection**
- **Metric**: Time to detect outdated docs
- **Target**: <1 week
- **How to measure**: CI checks, automated alerts

---

### Dashboard Example

```
Documentation Health Dashboard
===============================

📊 Coverage:        87% (target: 80%) ✅
🕐 Freshness:       73% (target: 80%) ⚠️
✅ Accuracy:        3 issues (target: <5) ✅
🔍 Findability:     92% (target: 90%) ✅
👍 Usefulness:      68% (target: 70%) ⚠️

📝 Process Metrics:
- Docs-as-Code:    65% PRs include docs ✅
- Review:          100% docs reviewed ✅
- Automation:      75% APIs auto-documented ⚠️

⚠️ Action Items:
1. Refresh 27% stale docs (older than 6 months)
2. Improve usefulness score (survey users)
3. Increase API doc automation (target: 80%)
```

---

### Tracking Tools

**Google Analytics / Plausible**:
- Page views per doc
- Search queries
- Bounce rate

**GitHub Insights**:
- Commit frequency to `/docs`
- PR inclusion of doc changes
- Doc file modification dates

**Custom Scripts**:
```bash
# Find docs not updated in 6 months
find docs/ -name "*.md" -mtime +180

# Count total docs
find docs/ -name "*.md" | wc -l

# Docs-as-code metric
git log --since="1 month ago" --name-only \
  | grep "^docs/" | wc -l
```

**Documentation Linters**:
- markdownlint (style)
- alex (inclusive language)
- write-good (clarity)

---

### Continuous Improvement

**Monthly Review**:
1. Check dashboard metrics
2. Identify low-performing docs
3. Prioritize updates
4. Track improvements

**Quarterly Goals**:
- Set targets for next quarter
- Celebrate wins (improved metrics)
- Adjust processes based on data

---

**End of Documentation Metrics Guide**
