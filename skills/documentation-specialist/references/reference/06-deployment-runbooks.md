# Deployment: Runbooks and Operational Guides

---
TOKEN_BUDGET: 280
TIER: 3
LOAD_TRIGGER: On-demand when creating runbooks or operational procedures
DEPENDENCIES: 06-deployment-documentation.md
---

## 6.3 Runbooks and Operational Guides

A **runbook** is a step-by-step procedure for handling operational tasks or incidents.

### Runbook Template

```markdown
# Runbook: Database Failover Procedure

## When to Use
When the primary database becomes unresponsive or corrupted.

## Prerequisites
- Access to AWS RDS console
- `psql` client installed
- VPN connected to production network

## Severity
🔴 **Critical** - Affects all users

## Steps

### 1. Verify Issue
```bash
psql -h primary.db.com -U admin -c "SELECT 1"
```
**Expected**: Query should return in <100ms
**If timeout**: Proceed to failover

### 2. Promote Read Replica
- Log into AWS RDS console: https://console.aws.amazon.com/rds
- Navigate to Databases → Select `taskmanager-replica-1`
- Actions → "Promote read replica"
- Confirm promotion
- **Wait**: 2-5 minutes for promotion to complete

### 3. Update Application Config
```bash
kubectl set env deployment/api \
  DATABASE_URL=postgres://admin:pass@replica.db.com:5432/tasks
```

### 4. Verify Application Health
```bash
curl https://api.taskmanager.com/health
```
**Expected**: `{"status": "healthy"}`

### 5. Notify Team
Post in #incidents Slack channel:
```
🔴 Database failover completed
- Old primary: primary.db.com (down)
- New primary: replica.db.com (promoted)
- Application: healthy
- Action: Investigate root cause
```

## Rollback
If issues occur:
```bash
kubectl set env deployment/api \
  DATABASE_URL=postgres://admin:pass@primary.db.com:5432/tasks
```

## Post-Incident
- [ ] Document root cause
- [ ] Review logs from failed primary
- [ ] Update monitoring alerts
- [ ] Schedule post-mortem meeting
```

### Types of Runbooks

1. **Incident Response**: Database failover, service restart, rollback deployment
2. **Routine Operations**: Backups, log rotation, certificate renewal
3. **Disaster Recovery**: Full system restore, data center failover
4. **Scaling**: Add capacity, resize databases, update autoscaling rules

### Best Practices

1. **Test Regularly**: Run through runbooks during game days
2. **Keep Updated**: Review after every incident
3. **Make Them Executable**: Use scripts where possible
4. **Include Rollback**: Every action should have an undo
5. **Specify Timing**: How long should each step take?
6. **Add Verification**: How do you know the step worked?

---

**End of Runbooks Guide**
