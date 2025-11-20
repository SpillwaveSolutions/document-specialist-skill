# Greenfield Documentation Workflow

---
TOKEN_BUDGET: 1500
TIER: 3
LOAD_TRIGGER: Intent = CREATE_NEW (template-based documentation)
DEPENDENCIES: SKILL.md, templates/markdown/*
---

## Overview

This workflow guides the creation of professional software documentation from templates for new projects (greenfield). Use this when the user wants to create documentation without existing code to reverse-engineer.

**Supported Document Types:**
- Software Requirements Specification (SRS)
- Product Requirements Document (PRD)
- Software Design Document (SDD)
- arc42 Architecture Documentation
- OpenAPI/REST API Specification
- User Guides and KB Articles
- Deployment Documentation

**Token Budget**: This workflow consumes ~1,500 tokens. Load only when intent is CREATE_NEW.

---

## Workflow Steps

### Step 1: Identify Document Type

Based on user request, classify the document type:

| Keywords in Request | Document Type | Template |
|---------------------|---------------|----------|
| "SRS", "requirements specification", "formal requirements" | SRS | templates/markdown/requirements-srs.md |
| "PRD", "product requirements", "feature doc", "agile" | PRD | templates/markdown/requirements-prd.md |
| "SDD", "design document", "technical design" | SDD | templates/markdown/design-sdd.md |
| "arc42", "architecture document", "system design" | arc42 | templates/markdown/design-arc42.md |
| "OpenAPI", "API spec", "REST API", "API documentation" | OpenAPI | templates/markdown/api-openapi.yaml |
| "user guide", "end-user documentation", "manual" | User Guide | templates/markdown/user-guide.md |
| "KB article", "knowledge base", "support doc" | KB Article | templates/markdown/kb-article.md |
| "deployment", "DevOps", "infrastructure docs" | Deployment | templates/markdown/deployment-guide.md |

### Step 2: Load Template and Reference Guide

**For SRS:**
- Template: `templates/markdown/requirements-srs.md`
- Reference: `reference/02-requirements.md`
- Best Practices: `reference/01-philosophy.md`

**For PRD:**
- Template: `templates/markdown/requirements-prd.md`
- Reference: `reference/02-requirements.md`
- Agile Guidance: `reference/08-agile-process.md`

**For OpenAPI:**
- Template: `templates/markdown/api-openapi.yaml`
- Reference: `reference/05-api-docs.md`

**For arc42:**
- Template: `templates/markdown/design-arc42.md`
- Reference: `reference/03-design.md`

**For User Guide:**
- Template: `templates/markdown/user-guide.md`
- Reference: `reference/07-user-docs.md`

**IMPORTANT**: Load ONLY the template and reference guide needed. Do NOT load all templates.

### Step 3: Customize Template

Extract key information from user's request:

1. **Project/Feature Name**: What is being documented?
2. **Domain/Industry**: Healthcare, finance, e-commerce, etc.?
3. **Key Requirements**: What did the user mention explicitly?
4. **Constraints**: Compliance (HIPAA, PCI-DSS), performance, security?
5. **Stakeholders**: Who will read this documentation?
6. **Target Audience**: Developers, users, executives, auditors?

**Customization Process:**

1. Replace all `[Placeholder]` markers in the template with actual content
2. Use Given-When-Then format for acceptance criteria (SRS/PRD)
3. Include specific examples relevant to the project domain
4. Add compliance requirements if mentioned (HIPAA, GDPR, PCI-DSS, SOC 2)
5. Customize section depth based on project complexity

**Example Customization:**

**Generic Template:**
```markdown
## 3.1 User Authentication
**FR-AUTH-001**: The system shall authenticate users.
```

**Customized for Healthcare:**
```markdown
## 3.1 User Authentication (HIPAA-Compliant)
**FR-AUTH-001**: HIPAA-Compliant Multi-Factor Authentication

**Description**: The system shall authenticate healthcare professionals using multi-factor authentication (MFA) with audit logging to comply with HIPAA security requirements.

**Acceptance Criteria**:
- **Given** a healthcare professional with valid credentials
- **When** they attempt to log in
- **Then** the system shall require both password and one-time passcode (OTP)
- **And** the system shall log all authentication attempts with timestamps and user IDs
- **And** failed login attempts shall be locked after 3 consecutive failures
- **And** all authentication events shall be stored in HIPAA-compliant audit logs for 7 years
```

### Step 4: Generate Content

Follow these guidelines for each document type:

#### SRS Generation

1. **Introduction** (1-2 pages)
   - Purpose, scope, intended audience
   - Document conventions (Given-When-Then, traceability IDs)
   - Project scope and objectives

2. **Overall Description** (2-3 pages)
   - Product perspective (system context)
   - User classes and characteristics
   - Operating environment
   - Constraints (technical, regulatory, business)

3. **System Features** (5-10 pages)
   - Functional requirements (FR-XXX-001 format)
   - Each requirement with:
     - Unique ID (e.g., FR-AUTH-001)
     - Description
     - Acceptance criteria (Given-When-Then)
     - Priority (Must Have, Should Have, Could Have, Won't Have)
   - Requirements traceability

4. **Non-Functional Requirements** (2-3 pages)
   - Performance (NFR-PERF-001)
   - Security (NFR-SEC-001)
   - Scalability (NFR-SCALE-001)
   - Usability (NFR-USABILITY-001)
   - Compliance (NFR-COMPLIANCE-001)

5. **External Interface Requirements** (1-2 pages)
   - User interfaces
   - Hardware interfaces
   - Software interfaces
   - Communication interfaces

6. **Appendix** (1-2 pages)
   - Glossary
   - Requirements traceability matrix

**Total**: 12-22 pages for comprehensive SRS

#### PRD Generation

1. **Objective** (0.5 pages)
   - Problem statement (2-3 sentences)
   - Proposed solution (2-3 sentences)
   - Why now?

2. **Success Metrics** (1 page)
   - Primary metrics (3-5 metrics with targets)
   - Secondary metrics (nice to have)
   - Counter-metrics (watch for negative impact)

3. **User Personas & Use Cases** (2-3 pages)
   - Primary persona (who, goals, pain points, how feature helps)
   - Secondary persona
   - 3-5 key use cases with scenarios

4. **User Stories & Acceptance Criteria** (3-5 pages)
   - Epic breakdown
   - User stories (As a [role], I want [goal], so that [benefit])
   - Acceptance criteria (Given-When-Then)
   - MoSCoW prioritization
   - Design mock links

5. **Out of Scope** (0.5 pages)
   - Explicitly state what's NOT included

6. **Technical Considerations** (1-2 pages)
   - Architecture impact
   - API changes
   - Database changes
   - Third-party integrations
   - Performance considerations
   - Security & privacy

7. **Timeline & Milestones** (0.5 pages)
   - Kickoff, Design Complete, Alpha, Beta, GA

8. **Risks & Mitigations** (1 page)
   - Risk table (risk, impact, likelihood, mitigation, owner)

**Total**: 9-14 pages for comprehensive PRD

#### OpenAPI Specification Generation

1. **Info Section**
   - API title, description, version
   - Contact and license information
   - Base URL (production, staging, local)

2. **Servers**
   - Production, staging, development URLs

3. **Tags**
   - Logical grouping (Authentication, Users, Products, Orders)

4. **Components (Reusable)**
   - securitySchemes (BearerAuth, OAuth2, API Key)
   - schemas (data models: User, Product, Order, Error)
   - parameters (PageParam, PerPageParam, SortParam)
   - responses (UnauthorizedError, NotFoundError, ValidationError)

5. **Paths (Endpoints)**
   - For each endpoint:
     - HTTP method (GET, POST, PUT, DELETE, PATCH)
     - Summary and description
     - operationId
     - Parameters (path, query, header)
     - Request body (if applicable)
     - Responses (200, 201, 400, 401, 404, 500)
     - Security requirements

6. **Examples**
   - Request examples
   - Response examples
   - Error response examples

**Total**: Aim for 500-1000 lines for comprehensive API with 10-20 endpoints

### Step 5: Add Visual Elements (Offer Diagram Generation)

After generating the document, offer to create diagrams:

**For SRS/SDD/arc42:**
```
I've created the [document type]. Would you like me to generate any of these diagrams?
- System Context diagram (C4 - via mermaid-architect)
- Container diagram (C4 - via mermaid-architect)
- Component diagram (PlantUML - via plantuml)
- Deployment diagram (PlantUML - via plantuml)
```

**For PRD:**
```
I've created the PRD. Would you like me to generate any of these diagrams?
- User journey flowchart (Mermaid - via mermaid-architect)
- State machine diagram (PlantUML - via plantuml)
- Activity diagram (PlantUML - via plantuml)
```

**For OpenAPI:**
```
I've created the OpenAPI specification. Would you like me to:
- Generate a human-readable API reference guide?
- Create sequence diagrams for key API flows?
```

**If user confirms**, invoke the appropriate skill:
- `mermaid-architect` for C4 diagrams, flowcharts
- `plantuml` for UML diagrams, ER diagrams, state machines

### Step 6: Professional Formatting

Ensure the generated document includes:

- ✅ **Front Matter**
  - Title
  - Version number
  - Date
  - Author
  - Status (Draft, In Review, Approved)

- ✅ **Table of Contents** (for documents > 3 pages)
  - Auto-generate with proper heading hierarchy

- ✅ **Consistent Formatting**
  - Heading hierarchy (H1 → H2 → H3)
  - Numbered sections for formal docs (SRS, SDD)
  - Bullet points for lists
  - Tables for structured data
  - Code blocks for examples

- ✅ **Traceability**
  - Unique IDs for requirements (FR-XXX-001)
  - Unique IDs for non-functional requirements (NFR-XXX-001)
  - Cross-references between sections

- ✅ **Glossary**
  - Define all technical terms
  - Define all acronyms

- ✅ **Professional Styling**
  - Clear section headers
  - Consistent spacing
  - Proper markdown syntax

### Step 7: Save and Offer Post-Processing

**Save to appropriate location:**

```
docs/
├── requirements/
│   ├── [project]-srs.md
│   └── [project]-prd.md
├── design/
│   ├── [project]-sdd.md
│   └── [project]-arc42.md
├── api/
│   └── [project]-openapi.yaml
└── user/
    ├── [project]-user-guide.md
    └── [project]-kb-article.md
```

**Offer post-processing options:**

```
I've created [document name] at [file path].

Would you like me to:
1. Convert this to Word format (DOCX)?
2. Generate a PDF version?
3. Create any diagrams?
4. Review the document for completeness?
5. Generate additional related documentation?
```

---

## Example: Greenfield SRS Creation

**User Request:**
```
Create a Software Requirements Specification for a cloud-based project management tool
```

**Skill Execution:**

```markdown
**Step 1: Identify Document Type**
→ SRS (Software Requirements Specification)

**Step 2: Load Template and Reference**
→ Read: templates/markdown/requirements-srs.md
→ Read: reference/02-requirements.md (if needed for guidance)

**Step 3: Customize Template**
→ Extract project details from request:
   - Project: Cloud-based project management tool
   - Domain: Productivity/SaaS
   - Key features implied: task management, team collaboration, cloud-based
   - Constraints: Likely need security, scalability, multi-tenancy

**Step 4: Generate Content**
→ Populate SRS template sections:

# Software Requirements Specification (SRS)
## Cloud-Based Project Management Tool

**Version**: 1.0
**Date**: 2025-01-13
**Status**: Draft
**Author**: [Generated by Claude Code]

---

## 1. Introduction

### 1.1 Purpose
This SRS defines the functional and non-functional requirements for a cloud-based project management tool designed to help teams collaborate on tasks, track progress, and manage project timelines.

### 1.2 Document Conventions
- **FR-XXX-001**: Functional Requirement with category and sequence ID
- **NFR-XXX-001**: Non-Functional Requirement with category and sequence ID
- **Given-When-Then**: Acceptance criteria format
- **MoSCoW**: Prioritization (Must Have, Should Have, Could Have, Won't Have)

### 1.3 Intended Audience
- Product managers
- Software engineers
- QA engineers
- UX designers
- Stakeholders

### 1.4 Project Scope
The cloud-based project management tool will enable teams to:
- Create and assign tasks
- Track project progress in real-time
- Collaborate via comments and file sharing
- Generate reports and analytics
- Integrate with third-party tools (calendar, email)

**Out of Scope for v1.0:**
- Mobile native apps (web-responsive only)
- Advanced AI-powered task recommendations
- Custom workflow automation

---

## 2. Overall Description

### 2.1 Product Perspective
The system is a standalone SaaS application accessible via web browsers. It will integrate with external services like email providers and calendar systems.

**System Context:**
```
[User] → [Web Browser] → [Project Management Application] ← [Email Service]
                                      ↕
                              [Database (PostgreSQL)]
                                      ↕
                              [File Storage (AWS S3)]
```

### 2.2 User Classes and Characteristics

**Project Manager** (Primary):
- Needs to create projects, assign tasks, track progress
- Requires reporting and analytics
- High computer proficiency

**Team Member** (Primary):
- Needs to view assigned tasks, update status, collaborate
- Requires notifications for updates
- Medium computer proficiency

**Admin** (Secondary):
- Manages users, projects, billing
- Requires access control configuration
- High computer proficiency

### 2.3 Operating Environment
- **Client**: Modern web browsers (Chrome, Firefox, Safari, Edge - latest 2 versions)
- **Server**: Cloud-hosted (AWS, Azure, or GCP)
- **Database**: PostgreSQL 14+
- **File Storage**: AWS S3 or equivalent object storage
- **Network**: HTTPS-only, API-first architecture

### 2.4 Constraints
- **Technical**: Must support 10,000 concurrent users
- **Regulatory**: GDPR compliance for EU users
- **Business**: Must launch MVP within 6 months
- **Security**: SOC 2 Type II certification required

---

## 3. System Features

### Feature 3.1: User Authentication and Authorization

**FR-AUTH-001**: User Registration
- **Description**: The system shall allow new users to register with email and password.
- **Acceptance Criteria**:
  - **Given** a new user visits the registration page
  - **When** they provide a valid email and password (min 8 characters, 1 uppercase, 1 number)
  - **Then** the system shall create a new account
  - **And** send a verification email
  - **And** redirect to email verification page
- **Priority**: Must Have

**FR-AUTH-002**: User Login
- **Description**: The system shall authenticate users with email and password.
- **Acceptance Criteria**:
  - **Given** a registered user with a verified email
  - **When** they enter correct credentials
  - **Then** the system shall grant access and issue a JWT token (1-hour expiry)
  - **And** redirect to the user's dashboard
- **Priority**: Must Have

**FR-AUTH-003**: Password Reset
- **Description**: The system shall allow users to reset forgotten passwords.
- **Acceptance Criteria**:
  - **Given** a user who forgot their password
  - **When** they request a password reset
  - **Then** the system shall send a reset link via email (valid for 15 minutes)
  - **And** allow the user to set a new password
- **Priority**: Must Have

### Feature 3.2: Task Management

**FR-TASK-001**: Create Task
- **Description**: The system shall allow project managers to create tasks with title, description, assignee, and due date.
- **Acceptance Criteria**:
  - **Given** a project manager is viewing a project
  - **When** they click "Create Task"
  - **Then** a task creation form shall appear
  - **And** they can fill in title (required), description (optional), assignee (optional), due date (optional)
  - **And** the task shall be created with status "Pending"
- **Priority**: Must Have

**FR-TASK-002**: Assign Task
- **Description**: The system shall allow assigning tasks to team members.
- **Acceptance Criteria**:
  - **Given** a task exists
  - **When** a project manager selects an assignee
  - **Then** the system shall assign the task to that user
  - **And** send a notification to the assignee
  - **And** the task shall appear in the assignee's task queue
- **Priority**: Must Have

**FR-TASK-003**: Update Task Status
- **Description**: The system shall allow users to update task status (Pending, In Progress, In Review, Completed).
- **Acceptance Criteria**:
  - **Given** a user is assigned a task
  - **When** they update the task status
  - **Then** the system shall save the new status
  - **And** notify the project manager
  - **And** update the project progress dashboard
- **Priority**: Must Have

[... Continue with more features ...]

---

## 4. Non-Functional Requirements

### 4.1 Performance

**NFR-PERF-001**: Page Load Time
- **Description**: All pages shall load within 2 seconds on a standard broadband connection.
- **Measurement**: 95th percentile load time < 2 seconds

**NFR-PERF-002**: API Response Time
- **Description**: All API endpoints shall respond within 500ms under normal load.
- **Measurement**: 95th percentile API response time < 500ms

**NFR-PERF-003**: Concurrent Users
- **Description**: The system shall support 10,000 concurrent users without degradation.
- **Measurement**: Load testing with 10,000 concurrent users, no errors, response times within SLA

### 4.2 Security

**NFR-SEC-001**: Data Encryption in Transit
- **Description**: All data shall be encrypted in transit using TLS 1.2 or higher.
- **Measurement**: Security scan confirms TLS 1.2+, no unencrypted connections

**NFR-SEC-002**: Data Encryption at Rest
- **Description**: All sensitive data (passwords, tokens) shall be encrypted at rest.
- **Measurement**: Database encryption enabled, passwords hashed with bcrypt

**NFR-SEC-003**: Authentication Token Security
- **Description**: JWT tokens shall expire after 1 hour and use secure signing.
- **Measurement**: Token expiry verified, HMAC SHA-256 signing confirmed

**NFR-SEC-004**: SQL Injection Prevention
- **Description**: The system shall use parameterized queries to prevent SQL injection.
- **Measurement**: Code review confirms all queries use parameterized statements, security scan shows no SQL injection vulnerabilities

### 4.3 Scalability

**NFR-SCALE-001**: Horizontal Scaling
- **Description**: The application shall support horizontal scaling by adding more server instances.
- **Measurement**: Demonstration of adding/removing server instances without downtime

**NFR-SCALE-002**: Database Scaling
- **Description**: The database shall support read replicas for load distribution.
- **Measurement**: Database configured with read replicas, read queries distributed

### 4.4 Usability

**NFR-USABILITY-001**: Mobile Responsive
- **Description**: The web interface shall be responsive and usable on mobile devices.
- **Measurement**: UI tested on iOS Safari and Android Chrome, all functions accessible

**NFR-USABILITY-002**: Accessibility
- **Description**: The system shall comply with WCAG 2.1 Level AA standards.
- **Measurement**: Accessibility audit with automated tools (aXe, Lighthouse) passes, manual keyboard navigation successful

### 4.5 Compliance

**NFR-COMPLIANCE-001**: GDPR Compliance
- **Description**: The system shall comply with GDPR for EU user data.
- **Measurement**: GDPR audit confirms right to access, right to deletion, data portability, consent management

**NFR-COMPLIANCE-002**: SOC 2 Type II
- **Description**: The system shall achieve SOC 2 Type II certification within 12 months of launch.
- **Measurement**: SOC 2 Type II audit report issued

---

## 5. External Interface Requirements

### 5.1 User Interfaces
- Web-based responsive UI
- Dashboard with project overview
- Task list views (kanban, list, calendar)
- User profile and settings

### 5.2 Hardware Interfaces
- None (cloud-based SaaS)

### 5.3 Software Interfaces
- **Email Service**: Integration with SendGrid or Amazon SES for transactional emails
- **Calendar Service**: Integration with Google Calendar and Outlook Calendar
- **File Storage**: Integration with AWS S3 for file uploads

### 5.4 Communication Interfaces
- **API**: RESTful API over HTTPS
- **WebSockets**: Real-time notifications and updates

---

## 6. Appendix

### 6.1 Glossary
- **JWT**: JSON Web Token - authentication token standard
- **GDPR**: General Data Protection Regulation - EU privacy regulation
- **SOC 2**: Service Organization Control 2 - security compliance framework
- **TLS**: Transport Layer Security - encryption protocol
- **WCAG**: Web Content Accessibility Guidelines

### 6.2 Requirements Traceability Matrix

| Requirement ID | Feature | Priority | Test Case ID | Status |
|----------------|---------|----------|--------------|--------|
| FR-AUTH-001 | User Registration | Must Have | TC-001 | Defined |
| FR-AUTH-002 | User Login | Must Have | TC-002 | Defined |
| FR-TASK-001 | Create Task | Must Have | TC-010 | Defined |
| NFR-PERF-001 | Page Load Time | Must Have | TC-100 | Defined |
| NFR-SEC-001 | Encryption in Transit | Must Have | TC-200 | Defined |

---

**End of SRS**

**Step 5: Add Visual Elements**
I've created the SRS. Would you like me to generate any of these diagrams?
- System Context diagram (C4 - via mermaid-architect)
- Use case diagram (PlantUML - via plantuml)
- ER diagram showing data model (PlantUML - via plantuml)

**Step 6: Professional Formatting**
✅ Front matter included
✅ Table of contents generated
✅ Consistent formatting applied
✅ Requirements traceability included
✅ Glossary added

**Step 7: Save and Offer Post-Processing**
Saved to: docs/requirements/project-management-srs.md

Would you like me to:
1. Convert this to Word format (DOCX)?
2. Generate a PDF version?
3. Create the System Context diagram?
4. Create an accompanying PRD for a specific feature?
```

---

## Advanced Features

### Multi-Project Documentation

If user requests documentation for multiple projects:

```
Generate documentation for all services in ~/projects/ecommerce-platform
```

**Workflow:**
1. Discover all projects in the directory
2. Detect framework for each project
3. Generate individual documentation for each
4. Create an overview document linking all projects
5. Generate system-wide C4 context diagram

### Documentation Packages

If user requests a complete documentation package:

```
Create a complete documentation package for release v2.0
```

**Workflow:**
1. Generate or update all document types:
   - SRS (if high-risk features)
   - PRD (for new features)
   - SDD (architecture)
   - API documentation
   - User guide
   - Deployment guide
2. Create all relevant diagrams
3. Convert to multiple formats (MD, DOCX, PDF)
4. Package everything in `docs-v2.0/` directory
5. Generate README index with links

### Template Customization

If user wants to use a custom template:

```
Use my custom SRS template at templates/my-srs-template.md to document this project
```

**Workflow:**
1. Read the custom template file
2. Identify placeholders in custom template
3. Use custom template instead of default
4. Apply same customization logic
5. Generate document using custom structure

### Continuous Documentation

If user wants docs-as-code setup:

```
Help me set up automated documentation generation in my CI/CD pipeline
```

**Workflow:**
1. Provide Git hooks for documentation updates:
   ```bash
   #!/bin/bash
   # pre-commit hook
   python scripts/generate-docs.py --validate
   ```
2. Provide CI/CD configuration:
   - GitHub Actions example
   - GitLab CI example
   - Jenkins pipeline example
3. Provide documentation validation scripts
4. Recommend documentation review process

---

## Quality Checklist

Before finalizing any greenfield document, verify:

- [ ] **Front Matter Complete**: Title, version, date, author, status
- [ ] **Table of Contents**: Generated for docs > 3 pages
- [ ] **Clear Purpose**: Introduction explains what and why
- [ ] **Audience Defined**: Who will read this document?
- [ ] **Consistent Formatting**: Headings, bullets, tables properly formatted
- [ ] **Traceability**: Requirements have unique IDs
- [ ] **Acceptance Criteria**: Given-When-Then format for testable requirements
- [ ] **Glossary**: All technical terms and acronyms defined
- [ ] **Realistic**: Requirements are achievable with current technology
- [ ] **Testable**: Each requirement has clear acceptance criteria
- [ ] **Professional**: No typos, proper grammar, appropriate tone
- [ ] **Visuals Offered**: User was offered diagrams if relevant
- [ ] **Post-Processing Offered**: User was offered format conversion

---

## References

For more detailed guidance on specific document types, load the appropriate reference guide:

- **Requirements Writing**: `reference/02-requirements.md`
- **Design Documentation**: `reference/03-design.md`
- **API Documentation**: `reference/05-api-docs.md`
- **User Documentation**: `reference/07-user-docs.md`
- **Documentation Philosophy**: `reference/01-philosophy.md`
- **Agile Documentation**: `reference/08-agile-process.md`

**Do NOT load these unless explicitly needed for the task at hand.**

---

**End of Greenfield Workflow Guide**
