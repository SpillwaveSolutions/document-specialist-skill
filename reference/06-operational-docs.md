# Operational Documentation Best Practices

**Version**: 1.0.0
**Token Budget**: ~400 tokens
**Last Updated**: 2025-01-18

---

## Runbook Essentials

### Purpose
Runbooks enable any authorized engineer to execute complex operational tasks consistently and safely.

### When to Create
- **Repetitive tasks**: Deployments, backups, scaling
- **Critical procedures**: Incident response, disaster recovery
- **Error-prone operations**: Database migrations, certificate renewal
- **On-call procedures**: Alert triage, escalation paths

---

## Structure (2025 Standards)

### Required Sections
1. **Metadata**: Owner, risk level, last updated, approval
2. **Scope**: When to use, expected outcome
3. **Prerequisites**: Access, tools, system state
4. **Pre-Flight Checks**: Validate before execution
5. **Step-by-Step**: Numbered, copy-paste commands
6. **Verification**: Success criteria, monitoring
7. **Rollback**: When and how to revert
8. **Troubleshooting**: Common errors, escalation

### Risk Matrix
| Risk | Approval | Testing | Rollback |
|------|----------|---------|----------|
| Low | Self-service | Dev | Optional |
| Medium | Team lead | Staging | Recommended |
| High | Director | Full staging | Required |
| Critical | VP + Board | Prod-like | Mandatory |

---

## Best Practices

### Clarity
- ✅ Every step starts with action verb
- ✅ Commands copy-pasteable
- ✅ Expected output shown
- ✅ No assumptions about knowledge

### Safety
- ✅ Pre-flight checks prevent disasters
- ✅ Rollback tested and documented
- ✅ High-risk has approval gates
- ✅ Idempotent operations (safe to re-run)

### Automation
- ✅ Repetitive steps scripted
- ✅ Scripts version controlled
- ✅ Manual fallback documented
- ✅ Automation reduces MTTR

### Governance
- ✅ Owner assigned
- ✅ Quarterly review schedule
- ✅ Version controlled
- ✅ Change log maintained

---

## Automation Integration

```bash
# Script with safety checks
./scripts/deploy.sh production --dry-run  # Preview
./scripts/deploy.sh production --execute   # Execute

# Expected output:
# ✓ Pre-flight checks passed
# ✓ Deployment successful
# ✓ Verification passed
```

---

## Monitoring

### Dashboard Links
```markdown
## Monitor During Execution
- Error Rate: {dashboard_url}
- Latency: {dashboard_url}
- Throughput: {dashboard_url}

## Rollback Triggers
- Error rate > 5%
- P95 latency > 500ms for 5min
- Database connections exhausted
```

---

## Success Criteria

✅ Executable by any authorized engineer
✅ All commands tested in non-prod
✅ Rollback tested and working
✅ Execution time ±20% accurate
✅ Verification clearly defines success

**Effective runbooks minimize MTTR and reduce operational risk.**
