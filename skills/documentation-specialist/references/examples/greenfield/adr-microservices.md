# ADR-001: Adopt Microservices Architecture over Monolith

---
**Status**: Accepted
**Date**: 2025-01-10
**Deciders**: Engineering Team, CTO, Product Lead
**Supersedes**: None
**Superseded by**: None

TOKEN_BUDGET: 400
TIER: 3 (Example)
LOAD_TRIGGER: Few-shot example for ADR creation
---

## Context

Our e-commerce platform currently runs as a single Ruby on Rails monolith deployed on Heroku. We're experiencing several challenges:

1. **Scaling limitations**: Billing service needs 10x more resources than catalog service, but we scale the entire monolith
2. **Deployment risk**: Every deployment affects all features, leading to slow release cycles (monthly deploys)
3. **Team bottlenecks**: 15 engineers working on same codebase, merge conflicts frequent
4. **Compliance isolation**: Billing (PCI-DSS) and user data (GDPR) require strict isolation, hard in a monolith
5. **Technology lock-in**: Stuck on Rails 5.2, can't experiment with new stacks (Go for performance, Node.js for real-time)

**Key Question**: Should we migrate to microservices or continue evolving the monolith?

---

## Decision

We will migrate to a microservices architecture with the following services:

| Service | Responsibility | Tech Stack | Team |
|---------|---------------|------------|------|
| **User Service** | Auth, profiles, GDPR | Node.js | Identity Team |
| **Catalog Service** | Products, inventory | Rails (existing code) | Catalog Team |
| **Cart Service** | Shopping cart, sessions | Node.js + Redis | Checkout Team |
| **Billing Service** | Payments, PCI-DSS | Go | Payment Team |
| **Notification Service** | Email, SMS, push | Python + Celery | Growth Team |
| **API Gateway** | Routing, auth, rate limiting | Kong | Platform Team |

**Migration Strategy**: Strangler Fig Pattern (gradual extraction, not big bang rewrite)

---

## Rationale

### Why Microservices?

**Independent Scaling**:
- Billing service: 5 instances during peak hours
- Catalog service: 2 instances (mostly reads, cached)
- **Cost savings**: ~40% reduction vs scaling entire monolith

**Faster Deployments**:
- Teams deploy independently (no coordination)
- Smaller services = faster CI/CD (5 mins vs 30 mins)
- Blue-green deployments per service
- **Target**: Daily deploys per team

**Compliance Isolation**:
- Billing service: Isolated network, PCI-DSS certified
- User service: GDPR-compliant data retention policies
- **Audit**: Easier to demonstrate compliance per service

**Team Autonomy**:
- Each team owns a service end-to-end
- Choose best tech stack per service
- Faster iteration (no monolith coordination)

**Failure Isolation**:
- If notification service fails, checkout still works
- Circuit breakers prevent cascading failures
- **Improved uptime**: 99.9% → 99.95% target

---

## Consequences

### Positive

✅ **Scalability**: Scale services independently based on load
✅ **Deployment velocity**: Teams ship daily instead of monthly
✅ **Technology flexibility**: Use best tool per service (Go for performance, Node for real-time)
✅ **Team ownership**: Clear boundaries reduce coordination overhead
✅ **Compliance**: Easier PCI-DSS and GDPR certification per service
✅ **Resilience**: Failures isolated to specific services

---

### Negative

❌ **Operational complexity**: More services to monitor, deploy, and maintain
- Mitigation: Invest in observability (Datadog), automation (Terraform, Helm)

❌ **Distributed system challenges**: Network latency, eventual consistency, distributed transactions
- Mitigation: Use sagas for distributed workflows, avoid distributed transactions

❌ **Data consistency**: No ACID transactions across services
- Mitigation: Event-driven architecture (Kafka) for eventual consistency

❌ **Testing complexity**: Integration tests span multiple services
- Mitigation: Contract testing (Pact), service virtualization

❌ **Initial migration cost**: 6-9 months to fully migrate
- Mitigation: Strangler Fig pattern (gradual migration, immediate value)

---

## Alternatives Considered

### Alternative 1: Modular Monolith

**Description**: Keep single codebase, organize into strict modules with clear boundaries

**Pros**:
- Simpler operations (one deployment)
- ACID transactions across modules
- Easier local development

**Cons**:
- Still requires scaling entire application
- Technology locked to Rails
- Team coordination still required
- **Rejected because**: Doesn't solve scaling or compliance isolation needs

---

### Alternative 2: Monolith + Background Workers

**Description**: Extract async jobs (email, reports) to Sidekiq workers, keep core logic in monolith

**Pros**:
- Low-hanging fruit (easy to implement)
- Isolate expensive background jobs

**Cons**:
- Doesn't solve billing isolation (PCI-DSS)
- Still monolith deployment risk
- Doesn't enable team autonomy
- **Rejected because**: Partial solution, doesn't address core problems

---

### Alternative 3: Serverless (AWS Lambda)

**Description**: Break into serverless functions (Lambda per API endpoint)

**Pros**:
- Auto-scaling built-in
- Pay-per-use pricing

**Cons**:
- Cold start latency (not acceptable for checkout)
- Vendor lock-in (AWS)
- Complex orchestration (Step Functions)
- Limited runtime (15-minute timeout)
- **Rejected because**: Too granular, operational complexity outweighs benefits

---

## Implementation Plan

### Phase 1: Extract Notification Service (Month 1-2)
- Low risk, isolated functionality
- Proof of concept for microservices

### Phase 2: Extract Billing Service (Month 3-5)
- High priority (PCI-DSS compliance)
- Use strangler pattern (dual-write during migration)

### Phase 3: Extract User Service (Month 6-7)
- GDPR compliance
- Authentication as separate service

### Phase 4: Extract Cart Service (Month 8-9)
- Real-time cart updates (WebSockets)
- Redis-backed for performance

**Validation Criteria**: Each service deployed to production, handling 10% traffic before cutover

---

## Related Decisions

- **ADR-002**: Choose Kafka for inter-service communication (linked)
- **ADR-003**: Adopt API Gateway (Kong) for routing and auth (linked)
- **ADR-005**: Use Docker + Kubernetes for deployment (linked)

---

## Notes

**Key Metrics to Track**:
- Deployment frequency (target: daily per team)
- Mean time to recovery (MTTR) (target: <30 mins)
- Service uptime (target: 99.95%)
- API latency (target: p95 <200ms)

**Review Date**: 2025-07-10 (6 months after full migration)

---

**End of ADR Example - Microservices Architecture**
