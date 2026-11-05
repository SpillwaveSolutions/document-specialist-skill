# Runbook: [Action-Oriented Title]

**Owner**: [Team/Person Responsible]
**Risk Level**: [Low/Medium/High/Critical]
**Last Updated**: [Date]
**Last Tested**: [Date]
**Approved By**: [Name] (if High/Critical risk)
**Version**: 1.0.0

---

## Quick Reference

| Attribute | Value |
|-----------|-------|
| **Execution Time** | ~[X] minutes |
| **Impact Window** | [Downtime/No downtime/Read-only mode] |
| **Rollback Time** | ~[X] minutes |
| **Prerequisites** | [Summary of key requirements] |

---

## Scope & Use Case

### When to Use This Runbook
[Describe the specific scenario or trigger that requires this runbook]

**Example Triggers**:
- Alert: [Alert name] fires for >5 minutes
- Event: Scheduled maintenance window
- Request: [Type of request from stakeholder]

### Expected Outcome
[What will be accomplished after successful execution]

### What This Does NOT Cover
- [Exclusion 1]
- [Exclusion 2]
- [Exclusion 3]

---

## Prerequisites

### Required Access & Permissions
- [ ] [Permission/role 1, e.g., "AWS Admin access to production account"]
- [ ] [Permission/role 2, e.g., "Kubernetes cluster-admin role"]
- [ ] [Permission/role 3, e.g., "Database write permissions"]

### Required Tools
- [ ] [Tool 1 with version, e.g., "kubectl 1.28+"]
- [ ] [Tool 2, e.g., "aws-cli configured with production profile"]
- [ ] [Tool 3, e.g., "Terraform 1.5+"]

**Verify tool installation**:
```bash
kubectl version --client
aws --version
terraform --version
```

### System State Requirements
- [ ] [Requirement 1, e.g., "No active deployments in progress"]
- [ ] [Requirement 2, e.g., "Database replication lag <1 second"]
- [ ] [Requirement 3, e.g., "Backup completed within last 24 hours"]

### Communication Requirements
- [ ] Notify [#channel/team] before starting
- [ ] Create incident ticket: [Link to template]
- [ ] Schedule change window if required: [Process link]

---

## Pre-Flight Checks

**STOP**: Do NOT proceed unless ALL checks pass.

### Check 1: Verify System Health
```bash
# Check application health
curl -s https://api.company.com/health | jq .

# Expected output:
# {"status":"healthy","uptime":3600,"database":"connected"}
```

✅ **Pass criteria**: Status is "healthy"
❌ **Fail action**: Investigate health issue before proceeding

---

### Check 2: Confirm Backup Exists
```bash
# Verify recent backup
aws rds describe-db-snapshots \
  --db-instance-identifier production-db \
  --query "DBSnapshots[0].[DBSnapshotIdentifier,SnapshotCreateTime]" \
  --output table
```

✅ **Pass criteria**: Backup exists from within last 24 hours
❌ **Fail action**: Trigger manual backup, wait for completion

---

### Check 3: [Additional Check]
[Command or manual check]

✅ **Pass criteria**: [Expected result]
❌ **Fail action**: [What to do if fails]

---

## Step-by-Step Procedure

### Step 1: [First Major Action]

**What this does**: [Brief explanation]

**Commands**:
```bash
# Set variables (customize these)
ENVIRONMENT="production"
REGION="us-east-1"

# Execute action
[command-to-run]
```

**Expected output**:
```
[Show expected console output]
```

**Verification**:
```bash
# Verify step completed successfully
[verification-command]
```

✅ **Success indicator**: [What to look for]
⚠️ **If failed**: Skip to [Troubleshooting](#troubleshooting) or [Rollback](#rollback-procedure)

---

### Step 2: [Second Major Action]

**What this does**: [Explanation]

**Manual steps** (if not automated):
1. Navigate to [location]
2. Click [button/menu]
3. Confirm [action]

**Or use automation** (recommended):
```bash
./scripts/[automation-script].sh $ENVIRONMENT
```

**Expected output**:
```
[Output from script or UI confirmation]
```

**Verification**:
- [ ] [Check 1]
- [ ] [Check 2]
- [ ] [Check 3]

---

### Step 3: [Continue Pattern for Each Step]

[Repeat structure: What it does → Commands → Expected output → Verification]

---

## Verification & Success Criteria

### Post-Execution Checks

#### Check 1: Application Health
```bash
# Test application endpoints
curl -s https://api.company.com/health
curl -s https://api.company.com/metrics
```

**Success criteria**:
- HTTP 200 status
- Response time <200ms
- No errors in logs for 5 minutes

---

#### Check 2: Metrics Validation
**Monitor these dashboards**:
- **Error Rate**: https://grafana.company.com/d/errors (should be <0.1%)
- **Latency**: https://grafana.company.com/d/latency (P95 <500ms)
- **Throughput**: https://grafana.company.com/d/throughput (baseline ±10%)

**Watch for 10 minutes** before declaring success.

---

#### Check 3: [Additional Verification]
[Specific checks for this runbook]

---

## Rollback Procedure

### When to Rollback

Execute rollback immediately if ANY of these occur:
- ⚠️ Error rate exceeds 5%
- ⚠️ P95 latency >2x baseline for 5 minutes
- ⚠️ Critical functionality broken
- ⚠️ [Specific failure condition]

### Rollback Steps

#### Step 1: Stop Current Process
```bash
# Immediately halt any ongoing changes
[stop-command]
```

#### Step 2: Restore Previous State
```bash
# Revert to last known good configuration
[rollback-command]

# Example for Kubernetes deployment:
kubectl rollout undo deployment/[app-name] -n production
```

**Expected output**:
```
[Rollback success message]
```

#### Step 3: Verify Restoration
```bash
# Confirm system returned to previous state
[verification-command]
```

**Success criteria**:
- Metrics return to baseline
- No increase in error rate
- Application responding normally

#### Step 4: Notify Stakeholders
- Update incident ticket with rollback status
- Notify in [#channel]
- Schedule post-mortem

---

## Troubleshooting

### Issue 1: [Common Problem]

**Symptoms**:
- [What you see/experience]

**Diagnosis**:
```bash
# Commands to diagnose
[diagnostic-command]
```

**Root Cause**:
[Explanation of why this happens]

**Solution**:
```bash
# Fix the issue
[fix-command]
```

**If persists**: Escalate to [team/person]

---

### Issue 2: [Another Common Problem]

[Follow same pattern: Symptoms → Diagnosis → Root Cause → Solution → Escalation]

---

### Escalation Path

| Severity | First Contact | Response Time | Next Escalation |
|----------|---------------|---------------|-----------------|
| **P1 (Critical)** | On-call engineer | Immediate | Engineering Manager (15 min) |
| **P2 (High)** | Team Slack channel | 30 minutes | Team Lead (1 hour) |
| **P3 (Medium)** | Team Slack channel | 2 hours | N/A |

**Contacts**:
- On-Call Engineer: [PagerDuty/OpsGenie rotation]
- Engineering Manager: @manager-name
- Team Slack: #team-channel

---

## Post-Execution Tasks

### Immediate (Within 5 Minutes)
- [ ] Update incident ticket with outcome
- [ ] Notify stakeholders in [#channel]
- [ ] Confirm all monitoring shows healthy state

### Within 24 Hours
- [ ] Review logs for anomalies
- [ ] Update runbook if any steps changed
- [ ] Document actual execution time
- [ ] Add any new troubleshooting discovered

### Within 1 Week (If Issues Occurred)
- [ ] Conduct post-mortem
- [ ] Identify automation opportunities
- [ ] Update monitoring/alerting if gaps found
- [ ] Share learnings with team

---

## Monitoring & Dashboards

**During Execution, Monitor**:
- Application Health: [Dashboard URL]
- Error Rates: [Dashboard URL]
- Performance Metrics: [Dashboard URL]
- Infrastructure: [Dashboard URL]

**Alert Channels**:
- Critical alerts: [PagerDuty/OpsGenie]
- Warning alerts: [Slack #alerts]

---

## Automation

### Automated Steps
This runbook includes automation for:
- [Step X]: Automated via [script/tool]
- [Step Y]: Automated via [CI/CD pipeline]

### Script Locations
- Main script: `scripts/[runbook-name].sh`
- Helper scripts: `scripts/lib/[helpers].sh`
- Configuration: `config/[environment].yaml`

**Run automation**:
```bash
# Full automation (requires approval for production)
./scripts/[runbook-name].sh --env=production --auto-approve

# Dry run (safe, shows what would execute)
./scripts/[runbook-name].sh --env=production --dry-run
```

### Manual Fallback
If automation fails, follow manual steps in [Step-by-Step Procedure](#step-by-step-procedure).

---

## Compliance & Audit

### Change Management
- **Change Ticket**: Required for High/Critical risk
- **Approval Required**: [Role] for production
- **Testing Required**: Staging environment test within 7 days

### Audit Trail
All executions are logged:
- Command history: Stored in [logging system]
- Outcome: Documented in incident ticket
- Review: Quarterly runbook review

---

## Appendix

### Related Runbooks
- [Related runbook 1 with link]
- [Related runbook 2 with link]

### Reference Documentation
- Architecture diagram: [Link]
- System documentation: [Link]
- API documentation: [Link]

### Version History
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0.0 | [Date] | [Name] | Initial version |

---

**Last Reviewed**: [Date]
**Next Review**: [Date + 3 months]
**Feedback**: Report issues or suggest improvements to [team/email]
