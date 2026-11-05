# Operational Runbook Workflow

---
TOKEN_BUDGET: 300
TIER: 2
LOAD_TRIGGER: Intent = CREATE_RUNBOOK
DEPENDENCIES: SKILL.md
---

## Overview

Create operational runbooks for DevOps teams.

**Supported**: Incident Response, Deployment Procedures, Maintenance Tasks, On-Call Procedures

## Workflow Steps

### Step 1: Identify Runbook Type

| Keywords | Type | Focus |
|----------|------|-------|
| "incident", "outage" | Incident Response | Triage, recovery |
| "deploy", "release", "rollback" | Deployment | Release procedures |
| "backup", "maintenance" | Maintenance | Scheduled tasks |
| "on-call", "alert" | On-Call | Alert handling |

### Step 2: Load Template

Read: `templates/markdown/runbook.md`
Example: [database-failover-runbook.md](../examples/brownfield/database-failover-runbook.md)

### Step 3: Gather Context

Extract from user request:
1. **Purpose** - Problem this runbook solves
2. **Trigger** - Conditions for using this runbook
3. **Owner** - Team or person responsible
4. **Systems** - Services involved
5. **SLA** - Time targets for resolution

### Step 4: Generate Content

**Runbook Structure**:

```markdown
# [Procedure Name] Runbook

## Overview
- Purpose: [What this runbook accomplishes]
- Owner: [Team/person responsible]
- Last Updated: [Date]
- SLA: [Time target]

## Prerequisites
- [ ] Access to [systems]
- [ ] Credentials for [services]
- [ ] Tools: [required tools]

## Procedure

### Step 1: [Action]
```bash
# Command to execute
command --flag value
```
**Expected result**: [What should happen]
**If this fails**: [Recovery action]

### Step 2: [Action]
...

## Verification
- [ ] [Check 1]
- [ ] [Check 2]

## Rollback
If the procedure fails:
1. [Rollback step 1]
2. [Rollback step 2]

## Escalation
- L1: [Contact]
- L2: [Contact]
- L3: [Contact]
```

### Step 5: Apply Runbook Best Practices

- **Executable commands**: Copy-pasteable, tested
- **No ambiguity**: One interpretation per step
- **Verification steps**: How to confirm success
- **Rollback plan**: Every procedure is reversible
- **Escalation path**: Who to call when stuck

### Step 6: Format & Save

Save to: `docs/runbooks/{system}-{procedure}.md`

Present options to user:
1. Generate related runbooks
2. Create monitoring dashboard config
3. Add architecture diagram

## Quality Checklist

- [ ] Clear trigger/when to use
- [ ] Prerequisites listed
- [ ] Commands are copy-pasteable
- [ ] Expected results documented
- [ ] Rollback procedure included
- [ ] Escalation contacts provided
