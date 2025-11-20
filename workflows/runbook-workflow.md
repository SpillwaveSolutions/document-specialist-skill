# Operational Runbook Workflow

---
TOKEN_BUDGET: 1100
TIER: 3
LOAD_TRIGGER: Intent = CREATE_RUNBOOK (create operational procedures, incident response docs)
DEPENDENCIES: SKILL.md, templates/markdown/runbook.md, reference/06-operational-docs.md
---

## Overview

This workflow guides the creation of operational runbooks for DevOps teams. Use this when documenting incident response procedures, deployment processes, maintenance tasks, or any operational procedure that needs to be repeatable and reliable.

**Supported Runbook Types:**
- **Incident Response**: Handle system outages, security incidents
- **Deployment Procedures**: Release software, rollback changes
- **Maintenance Tasks**: Database backups, log rotation, certificate renewal
- **On-Call Procedures**: Triage alerts, escalation paths

**Token Budget**: This workflow consumes ~1,100 tokens. Load only when intent is CREATE_RUNBOOK.

---

## Workflow Steps

### Step 1: Identify Runbook Type and Scope

Based on user request, classify the runbook:

| Keywords | Runbook Type | Template Section | Use Case |
|----------|--------------|------------------|----------|
| "incident", "outage", "down" | Incident Response | templates/markdown/runbook.md | System recovery, triage |
| "deploy", "release", "rollback" | Deployment | templates/markdown/runbook.md | Software releases |
| "backup", "restore", "maintenance" | Maintenance | templates/markdown/runbook.md | Scheduled tasks |
| "on-call", "alert", "triage" | On-Call | templates/markdown/runbook.md | Alert handling |

### Step 2: Load Template and Reference Guide

**For All Runbooks**:
- Template: `templates/markdown/runbook.md`
- Reference: `reference/06-operational-docs.md`
- Example: `examples/brownfield/database-failover-runbook.md`

### Step 3: Gather Context

**Essential Information**:

1. **Runbook Purpose**:
   - What problem does this solve?
   - When should this runbook be used?
   - What's the expected outcome?
   - Risk level? (low, medium, high, critical)

2. **Prerequisites**:
   - Required permissions/access levels?
   - Tools needed? (kubectl, aws-cli, etc.)
   - System state requirements?
   - Team notification requirements?

3. **System Context**:
   - Which services/systems involved?
   - Dependencies to check?
   - Monitoring dashboards to watch?

4. **Automation Opportunities**:
   - Can any steps be scripted?
   - Existing automation to reference?
   - Manual steps that should be automated?

**If context is missing**: Use AskUserQuestion to gather required details.

### Step 4: Structure the Runbook

**Required Sections**:

1. **Metadata** (Top):
   ```markdown
   **Title**: [Clear, action-oriented title]
   **Owner**: [Team/Person responsible]
   **Risk Level**: [Low/Medium/High/Critical]
   **Last Updated**: [Date]
   **Approved By**: [Approver if high-risk]
   ```

2. **Scope & Use Case**:
   - When to use this runbook
   - Expected outcome
   - What this runbook does NOT cover

3. **Prerequisites**:
   - Access requirements
   - Tool installations
   - System state validations
   - Communication (who to notify before starting)

4. **Pre-Flight Checks**:
   - Verify system health
   - Confirm backup exists
   - Check active users/traffic
   - Validate rollback capability

5. **Step-by-Step Procedure**:
   - Numbered, actionable steps
   - Commands to execute (copy-pasteable)
   - Expected output for each step
   - Idempotent operations (safe to re-run)

6. **Verification**:
   - How to confirm success
   - Metrics to monitor
   - Health checks to run

7. **Rollback Procedure**:
   - When to rollback
   - Safe recovery steps
   - How to restore previous state

8. **Troubleshooting**:
   - Common errors
   - Escalation criteria
   - Who to contact for help

9. **Post-Execution**:
   - Notifications to send
   - Logs to capture
   - Documentation to update

### Step 5: Apply Runbook Best Practices

**Clarity & Precision**:
- ✅ Every step is actionable (starts with verb: "Run...", "Check...", "Verify...")
- ✅ Commands are copy-pasteable with no placeholders or minimal placeholders
- ✅ Expected output shown for verification
- ✅ No assumptions about user knowledge

**Safety & Reliability**:
- ✅ Pre-flight checks prevent disasters
- ✅ Rollback procedure tested and documented
- ✅ High-risk operations have approval gates
- ✅ Idempotent steps (safe to re-run)

**Automation**:
- ✅ Repetitive steps scripted
- ✅ Scripts stored in version control
- ✅ Automation documented (what it does, how to run)
- ✅ Manual fallback if automation fails

**Governance**:
- ✅ Owner assigned
- ✅ Review schedule (quarterly minimum)
- ✅ Version controlled
- ✅ Change log maintained

**Accessibility**:
- ✅ Discoverable (wiki, docs site, on-call portal)
- ✅ Searchable (good metadata/tags)
- ✅ Mobile-friendly (for on-call use)

### Step 6: Automation Integration

**Script Integration Pattern**:
```markdown
### Step 3: Restart Application Pods
```bash
# Manual command (if automation unavailable)
kubectl rollout restart deployment/myapp -n production

# Or use automation script (recommended)
./scripts/restart-deployment.sh myapp production
```

**Expected output:**
```
deployment.apps/myapp restarted
Waiting for rollout to finish: 0 of 3 updated replicas are available...
Waiting for rollout to finish: 2 of 3 updated replicas are available...
deployment "myapp" successfully rolled out
```

**Verification:**
```bash
kubectl get pods -n production | grep myapp
# All pods should show STATUS: Running
```
```

**Workflow Automation References**:
- Link to CI/CD pipeline if applicable
- Reference to infrastructure-as-code (Terraform, Pulumi)
- Integration with incident management (PagerDuty, OpsGenie)

### Step 7: Risk Mitigation

**For High-Risk Runbooks**:
- Add approval requirement before execution
- Require confirmation prompts in scripts
- Document rollback triggers ("Rollback if error rate > 5%")
- Add circuit breaker conditions

**Risk Matrix**:
| Risk Level | Approval Required | Testing Required | Rollback Plan |
|------------|-------------------|------------------|---------------|
| **Low** | Self-service | Test in dev | Optional |
| **Medium** | Team lead | Test in staging | Recommended |
| **High** | Director | Full staging test | Required |
| **Critical** | VP + Change Board | Production-like test | Mandatory + rehearsed |

### Step 8: Add Monitoring & Observability

**Dashboard Links**:
```markdown
## Monitoring During Execution
- **Application Dashboard**: https://grafana.company.com/d/app-health
- **Error Rate**: https://datadog.company.com/dashboard/errors
- **Database Performance**: https://cloudwatch.aws.amazon.com/db-metrics
```

**Alert Thresholds**:
```markdown
## Rollback Triggers
Execute rollback if ANY of these occur:
- Error rate > 5% (dashboard link)
- P95 latency > 500ms for 5 minutes
- Database connections exhausted
- Memory usage > 90%
```

### Step 9: Quality Checklist

**All Runbooks Must Have**:
- [ ] Clear, action-oriented title
- [ ] Owner and last updated date
- [ ] Risk level classification
- [ ] Scope and use case
- [ ] Prerequisites checklist
- [ ] Pre-flight validation steps
- [ ] Step-by-step procedure (numbered)
- [ ] Expected output for each step
- [ ] Verification procedure
- [ ] Rollback procedure
- [ ] Troubleshooting section
- [ ] Post-execution tasks
- [ ] Approval requirements (if high-risk)

**Testing Requirements**:
- All commands tested in non-production
- Rollback procedure tested
- Time estimates accurate (track actual execution time)
- Screenshots/outputs current

### Step 10: Generate Output

**Markdown Output** (Primary):
- Save to `docs/runbooks/` or `ops/runbooks/`
- Use descriptive filename: `runbook-database-failover.md`
- Include in runbook index/catalog

**Automation Artifacts**:
- Shell scripts in `scripts/` directory
- Terraform/Pulumi code in `infrastructure/`
- CI/CD pipeline configs

**Integration**:
- Add to on-call wiki
- Link from incident management system
- Reference in monitoring alerts

---

## Common Patterns

### Pattern 1: Incident Response Runbook
```markdown
# Runbook: API Gateway Outage Response

**Risk Level**: Critical
**Owner**: Platform Team
**On-Call Escalation**: @platform-oncall

## Use Case
API Gateway returns 5xx errors for >5 minutes. Use this runbook to diagnose and restore service.

## Prerequisites
- [ ] VPN connected
- [ ] AWS CLI configured
- [ ] kubectl access to production cluster
- [ ] Notify #incidents channel before starting

## Pre-Flight Checks
1. Verify outage scope: Check status page reports
2. Check recent deployments: Any changes in last 2 hours?
3. Validate monitoring: Are alerts firing correctly?

## Procedure
### Step 1: Check API Gateway Health
```bash
aws apigatewayv2 get-apis --query "Items[?Name=='production-api'].ApiEndpoint"
curl -I https://api.company.com/health
```

Expected: HTTP 200 with `{"status":"healthy"}`

If failing: Proceed to Step 2

[Continue with diagnosis and remediation steps]
```

### Pattern 2: Deployment Runbook
```markdown
# Runbook: Deploy Web Application (Production)

**Risk Level**: High
**Owner**: DevOps Team
**Approval Required**: Engineering Manager

## Use Case
Deploy new web application version to production during change window.

## Prerequisites
- [ ] Change ticket approved (CHNG-XXXX)
- [ ] Staging deployment successful
- [ ] Database migrations tested
- [ ] Rollback plan reviewed
- [ ] Notify #engineering 30min before

## Deployment Steps
[Detailed steps with commands]

## Rollback Procedure
If deployment fails OR error rate > 3%:
1. Immediately revert to previous version:
   ```bash
   kubectl rollout undo deployment/web-app -n production
   ```
2. Clear CDN cache
3. Notify stakeholders
4. Post-mortem within 24 hours
```

### Pattern 3: Maintenance Runbook
```markdown
# Runbook: Monthly Database Backup Verification

**Risk Level**: Medium
**Owner**: Data Team
**Schedule**: First Saturday of each month

## Use Case
Verify database backups are restorable and meet RPO/RTO requirements.

## Procedure
1. Identify latest backup:
   ```bash
   aws rds describe-db-snapshots --db-instance-identifier prod-db \
     --query "DBSnapshots[0].DBSnapshotIdentifier"
   ```

2. Restore to test environment:
   ```bash
   ./scripts/restore-db-snapshot.sh <snapshot-id> test-restore
   ```

3. Verify data integrity:
   ```sql
   SELECT COUNT(*) FROM users;  -- Should match production
   SELECT MAX(created_at) FROM users;  -- Should be recent
   ```

4. Document results:
   - Restore time: [X] minutes (RTO target: <30 min)
   - Data age: [X] hours (RPO target: <4 hours)
   - Issues: None | [Description]

5. Cleanup test environment
```

---

## Error Handling

**Issue**: Runbook steps fail but no rollback defined
**Solution**: Immediately stop execution, assess blast radius, engage incident commander

**Issue**: Automation script not working
**Solution**: Document manual fallback steps in runbook, fix automation post-incident

**Issue**: Runbook outdated (commands don't work)
**Solution**: Mark runbook as "DEPRECATED" immediately, schedule update within 1 week

---

## Integration with Other Workflows

- **Brownfield Code-to-Docs**: Generate runbooks from infrastructure code (Pulumi, Terraform)
- **Diagram Workflow**: Create deployment diagrams, architecture diagrams
- **Convert Workflow**: Export to PDF for offline on-call access

---

## Success Criteria

✅ Runbook can be executed by any authorized engineer (not just author)
✅ All commands tested in non-production environment
✅ Rollback procedure tested and working
✅ Execution time estimate accurate (±20%)
✅ Verification steps clearly define success
✅ High-risk runbooks have approval gates

**Effective runbooks minimize MTTR (Mean Time To Resolution) and reduce operational risk.**
