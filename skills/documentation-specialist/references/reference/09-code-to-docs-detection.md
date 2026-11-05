# Code-to-Docs: Framework Detection Patterns

---
TOKEN_BUDGET: 200
TIER: 3
LOAD_TRIGGER: On-demand when detecting technology stack for brownfield documentation
DEPENDENCIES: 09-code-to-docs-when.md
---

## 9.2 Framework Detection Patterns

### Backend Frameworks

**Spring Boot:**
- **Files**: `pom.xml` or `build.gradle`
- **Annotations**: `@SpringBootApplication`, `@RestController`, `@Service`
- **Grep patterns**: `import org.springframework`

**FastAPI:**
- **Files**: `requirements.txt` with `fastapi`, `main.py` or `app.py`
- **Patterns**: `app = FastAPI()`, `@app.get()`, `@app.post()`
- **Grep patterns**: `from fastapi import`

**Express.js:**
- **Files**: `package.json` with `"express"`
- **Patterns**: `const express = require('express')`, `app.listen()`
- **Grep patterns**: `require('express')` or `import express`

**Django:**
- **Files**: `manage.py`, `settings.py`, `requirements.txt` with `Django`
- **Patterns**: `django.conf`, `urls.py`, `views.py`
- **Grep patterns**: `from django`

**Flask:**
- **Files**: `requirements.txt` with `Flask`, `app.py`
- **Patterns**: `from flask import Flask`, `app = Flask(__name__)`
- **Grep patterns**: `from flask import`

---

### Infrastructure as Code

**Pulumi:**
- **Files**: `Pulumi.yaml`, `__main__.py` or `index.ts`
- **Patterns**: `import pulumi`, resource declarations
- **Grep patterns**: `pulumi.aws`, `pulumi.gcp`

**Terraform:**
- **Files**: `*.tf`, `terraform.tfstate`
- **Patterns**: `resource "aws_*"`, `provider "aws"`
- **Grep patterns**: `resource "`

**AWS CDK:**
- **Files**: `cdk.json`, `package.json` with `aws-cdk`
- **Patterns**: `new cdk.Stack`, `cdk deploy`
- **Grep patterns**: `import * as cdk`

---

### Frontend Frameworks

**React:**
- **Files**: `package.json` with `"react"`
- **Patterns**: `import React`, `function Component()`, JSX syntax
- **Grep patterns**: `from 'react'`

**Next.js:**
- **Files**: `next.config.js`, `pages/` directory
- **Patterns**: `export default function Page()`, `getServerSideProps`
- **Grep patterns**: `from 'next`

**Vue.js:**
- **Files**: `package.json` with `"vue"`
- **Patterns**: `<template>`, `<script>`, `.vue` files
- **Grep patterns**: `from 'vue'`

---

### Detection Algorithm

1. **Scan for detection files** (Glob):
   ```
   pom.xml, build.gradle, requirements.txt, package.json, Pulumi.yaml
   ```

2. **Confirm framework patterns** (Grep):
   ```
   @SpringBootApplication, from fastapi import, const express
   ```

3. **Load framework-specific mapping**:
   ```
   mappings/backend/spring-boot-mapping.yaml
   ```

---

**End of Framework Detection Patterns Guide**
