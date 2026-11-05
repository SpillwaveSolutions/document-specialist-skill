# SRS Generation Guide

---
TOKEN_BUDGET: 250
TIER: 3
LOAD_TRIGGER: CREATE_NEW + SRS document type
DEPENDENCIES: greenfield-workflow.md
---

## SRS Structure (IEEE 830-based)

### 1. Introduction (1-2 pages)
- Purpose, scope, intended audience
- Document conventions (Given-When-Then, traceability IDs)
- Project objectives

### 2. Overall Description (2-3 pages)
- Product perspective (system context)
- User classes and characteristics
- Operating environment
- Constraints (technical, regulatory, business)

### 3. System Features (5-10 pages)
Each requirement includes:
- **Unique ID**: FR-{CATEGORY}-{NUMBER} (e.g., FR-AUTH-001)
- **Description**: What the system shall do
- **Acceptance Criteria**: Given-When-Then format
- **Priority**: Must Have / Should Have / Could Have / Won't Have

### 4. Non-Functional Requirements (2-3 pages)
- **NFR-PERF-xxx**: Performance (response times, throughput)
- **NFR-SEC-xxx**: Security (encryption, authentication)
- **NFR-SCALE-xxx**: Scalability (concurrent users, data volume)
- **NFR-USABILITY-xxx**: Usability (accessibility, mobile)
- **NFR-COMPLIANCE-xxx**: Compliance (GDPR, HIPAA, PCI-DSS)

### 5. External Interfaces (1-2 pages)
- User interfaces, hardware interfaces
- Software interfaces, communication interfaces

### 6. Appendix (1-2 pages)
- Glossary
- Requirements traceability matrix

## Compliance Patterns

**HIPAA** (Healthcare):
```markdown
**FR-AUTH-001**: HIPAA-Compliant MFA
- **And** all authentication events logged for 7 years
- **And** failed logins locked after 3 attempts
```

**PCI-DSS** (Payment):
```markdown
**NFR-SEC-001**: Payment Data Encryption
- All cardholder data encrypted with AES-256
- Key rotation every 90 days
```

**GDPR** (EU Data):
```markdown
**FR-PRIVACY-001**: Right to Deletion
- **Given** a user requests data deletion
- **Then** all personal data removed within 30 days
```

## Reference

For requirements writing best practices: [02-requirements-writing.md](../../reference/02-requirements-writing.md)

For complete SRS example: [billing-srs.md](../../examples/greenfield/billing-srs.md)
