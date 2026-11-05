# Runbook: PostgreSQL Primary Database Failover

**Owner**: Data Platform Team
**Risk Level**: Critical
**Last Updated**: 2025-01-18
**Last Tested**: 2025-01-15
**Approved By**: VP Engineering
**Version**: 2.1.0

---

## Quick Reference

| Attribute | Value |
|-----------|-------|
| **Execution Time** | ~15 minutes |
| **Impact Window** | 2-5 minutes downtime |
| **Rollback Time** | ~10 minutes |
| **Prerequisites** | Database admin access, VPN connection |

---

## Scope & Use Case

### When to Use This Runbook
Use when primary PostgreSQL database is unavailable and must failover to standby replica.

**Triggers**:
- Alert: "Primary DB Unresponsive" fires for >5 minutes
- Manual intervention required during maintenance
- Primary instance failure detected

### Expected Outcome
Standby replica promoted to primary, application reconnected, full read/write capability restored.

### What This Does NOT Cover
- Multi-region failover (see Runbook-DB-003)
- Planned maintenance failover (see Runbook-DB-002)

---

## Prerequisites

### Required Access
- [ ] AWS Admin access to production account (role: `DatabaseAdmin`)
- [ ] VPN connected to production network
- [ ] PagerDuty incident created

### Required Tools
- [ ] aws-cli 2.0+ configured with production profile
- [ ] psql client 14+
- [ ] kubectl 1.28+ with production cluster access

**Verify tools**:
```bash
aws sts get-caller-identity --profile production
psql --version
kubectl config current-context  # Should show: production
```

### System State Requirements
- [ ] Standby replica in sync (replication lag <10 seconds)
- [ ] No active database migrations running
- [ ] Backup completed within last 6 hours

### Communication
- [ ] Create P1 incident: https://company.pagerduty.com
- [ ] Notify #incidents channel: "DB failover in progress"
- [ ] Page on-call DBA if not already engaged

---

## Pre-Flight Checks

### Check 1: Verify Standby Health
```bash
aws rds describe-db-instances \
  --db-instance-identifier prod-db-replica \
  --query 'DBInstances[0].[DBInstanceStatus,ReplicationState]' \
  --output table
```

✅ **Pass**: Status=`available`, ReplicationState=`replicating`
❌ **Fail**: STOP - Standby not healthy, escalate to DBA team

---

### Check 2: Check Replication Lag
```bash
psql -h prod-db-replica.abc123.us-east-1.rds.amazonaws.com \
  -U admin -d postgres -c \
  "SELECT NOW() - pg_last_xact_replay_timestamp() AS replication_lag;"
```

✅ **Pass**: Lag <10 seconds
❌ **Fail**: Wait for replica to catch up or escalate

---

### Check 3: Confirm Recent Backup
```bash
aws rds describe-db-snapshots \
  --db-instance-identifier prod-db \
  --query 'DBSnapshots[0].[DBSnapshotIdentifier,SnapshotCreateTime]' \
  --output table
```

✅ **Pass**: Backup from within last 6 hours
❌ **Fail**: Trigger manual snapshot, wait for completion

---

## Step-by-Step Procedure

### Step 1: Put Application in Read-Only Mode
**What this does**: Prevents write attempts during failover

```bash
kubectl scale deployment/api-server --replicas=0 -n production
```

**Expected output**:
```
deployment.apps/api-server scaled
```

**Verification**:
```bash
kubectl get pods -n production | grep api-server
# Should show: No resources found
```

✅ **Success**: All API pods terminated
⚠️ **If failed**: Force delete pods, then proceed

---

### Step 2: Promote Standby to Primary
**What this does**: Converts read replica to standalone primary database

```bash
aws rds promote-read-replica \
  --db-instance-identifier prod-db-replica \
  --profile production
```

**Expected output**:
```json
{
    "DBInstance": {
        "DBInstanceIdentifier": "prod-db-replica",
        "DBInstanceStatus": "modifying"
    }
}
```

**Wait for promotion** (typically 3-5 minutes):
```bash
while true; do
  STATUS=$(aws rds describe-db-instances \
    --db-instance-identifier prod-db-replica \
    --query 'DBInstances[0].DBInstanceStatus' \
    --output text)
  echo "Status: $STATUS"
  [[ "$STATUS" == "available" ]] && break
  sleep 15
done
```

---

### Step 3: Update Application Configuration
**What this does**: Points app to new primary database

```bash
# Update Kubernetes secret with new endpoint
kubectl create secret generic db-connection \
  --from-literal=host=prod-db-replica.abc123.us-east-1.rds.amazonaws.com \
  --from-literal=port=5432 \
  --dry-run=client -o yaml | kubectl apply -f -
```

**Restart application pods**:
```bash
kubectl scale deployment/api-server --replicas=3 -n production
```

**Wait for pods to be ready**:
```bash
kubectl wait --for=condition=ready pod \
  -l app=api-server \
  -n production \
  --timeout=180s
```

---

### Step 4: Verify Database Connectivity
```bash
# Test write operation
psql -h prod-db-replica.abc123.us-east-1.rds.amazonaws.com \
  -U admin -d postgres -c \
  "CREATE TABLE failover_test (id serial, ts timestamp default now()); \
   DROP TABLE failover_test;"
```

✅ **Success**: Table created and dropped without errors

---

## Verification

### Check 1: Application Health
```bash
curl -s https://api.company.com/health | jq .
```

**Expected**:
```json
{
  "status": "healthy",
  "database": "connected",
  "uptime": 60
}
```

---

### Check 2: Monitor Metrics (10 minutes)
**Dashboards**:
- Error Rate: https://grafana.company.com/d/errors
  - Target: <0.1%
- Query Latency: https://grafana.company.com/d/db-perf
  - Target: P95 <50ms
- Connection Pool: https://grafana.company.com/d/db-connections
  - Target: <80% utilized

---

### Check 3: Sample Data Queries
```bash
psql -h prod-db-replica... -c "SELECT COUNT(*) FROM users;"
psql -h prod-db-replica... -c "SELECT COUNT(*) FROM orders WHERE created_at > NOW() - INTERVAL '1 hour';"
```

Verify counts match expected values.

---

## Rollback Procedure

### When to Rollback
- Error rate exceeds 5%
- Database writes failing
- Critical functionality broken

### Rollback Steps
**Note**: Rollback to old primary requires restoring from backup

1. **Scale down application**:
   ```bash
   kubectl scale deployment/api-server --replicas=0 -n production
   ```

2. **Restore from latest snapshot**:
   ```bash
   aws rds restore-db-instance-from-db-snapshot \
     --db-instance-identifier prod-db-restored \
     --db-snapshot-identifier <latest-snapshot> \
     --profile production
   ```

3. **Wait for restore** (~20 minutes)

4. **Update connection config** to point to restored instance

5. **Restart application**

---

## Troubleshooting

### Issue: Promotion Stuck in "modifying"
**Diagnosis**:
```bash
aws rds describe-events \
  --source-identifier prod-db-replica \
  --source-type db-instance \
  --duration 30
```

**Solution**: Wait up to 10 minutes. If still stuck, contact AWS support (Priority: Urgent).

---

### Issue: Application Can't Connect
**Diagnosis**:
```bash
# Check security group rules
aws ec2 describe-security-groups \
  --group-ids sg-abc123 \
  --query 'SecurityGroups[0].IpPermissions'

# Test connection from pod
kubectl run -it --rm debug --image=postgres:14 --restart=Never -- \
  psql -h prod-db-replica... -U admin -c '\conninfo'
```

**Solution**: Verify security group allows traffic from application subnet.

---

## Post-Execution

### Immediate
- [ ] Update incident with "Failover complete"
- [ ] Notify #incidents: "Service restored"
- [ ] Monitor for 30 minutes

### Within 24 Hours
- [ ] Review RDS events for issues
- [ ] Rebuild standby replica from new primary
- [ ] Document actual execution time: ____ minutes
- [ ] Update runbook if steps changed

### Within 1 Week
- [ ] Post-mortem meeting scheduled
- [ ] Root cause identified
- [ ] Action items created
- [ ] Share learnings with engineering

---

## Monitoring

**During Execution**:
- Database Health: https://cloudwatch.aws.amazon.com/db-health
- Application Metrics: https://grafana.company.com/d/app-overview
- Error Logs: https://kibana.company.com/app/discover

**Alert Channels**:
- Critical: PagerDuty rotation
- Warnings: #alerts-production Slack

---

## Escalation

| Contact | Role | When to Engage |
|---------|------|----------------|
| On-Call DBA | Database expert | Replication issues |
| AWS Support | Infrastructure | RDS API failures |
| Engineering Manager | Decision authority | >30 min outage |

---

**Last Reviewed**: 2025-01-15
**Next Review**: 2025-04-15
**Feedback**: data-platform@company.com
