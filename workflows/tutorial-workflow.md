# Tutorial and Developer Guide Workflow

---
TOKEN_BUDGET: 1300
TIER: 3
LOAD_TRIGGER: Intent = CREATE_TUTORIAL (create developer tutorials, API guides, CLI docs)
DEPENDENCIES: SKILL.md, templates/markdown/developer-tutorial.md, reference/08-tutorial-writing.md
---

## Overview

This workflow guides the creation of developer-focused documentation including tutorials, API usage guides, CLI documentation, and getting started guides for technical audiences. Use this when the user wants to create documentation for developers or technically advanced users.

**Supported Document Types:**
- **Developer Tutorials**: Project-based learning with code examples
- **API Usage Guides**: How to integrate with REST/GraphQL APIs
- **CLI Documentation**: Command-line tool reference and usage
- **Getting Started (Developer)**: Quick setup for developers

**Token Budget**: This workflow consumes ~1,300 tokens. Load only when intent is CREATE_TUTORIAL.

---

## Workflow Steps

### Step 1: Identify Developer Documentation Type

Based on user request, classify the document type:

| Keywords in Request | Document Type | Template | Use Case |
|---------------------|---------------|----------|----------|
| "tutorial", "learn", "walkthrough" | Developer Tutorial | templates/markdown/developer-tutorial.md | Project-based learning, teach concepts |
| "API guide", "API usage", "integration" | API Usage Guide | templates/markdown/api-usage-guide.md | How to call APIs, authentication, examples |
| "CLI documentation", "command reference" | CLI Documentation | templates/markdown/cli-documentation.md | Command syntax, flags, examples |
| "getting started", "quick start" | Getting Started (Dev) | templates/markdown/getting-started.md | 5-minute setup for developers |

### Step 2: Load Template and Reference Guide

**For Developer Tutorials**:
- Template: `templates/markdown/developer-tutorial.md`
- Reference: `reference/08-tutorial-writing.md` (Developer Tutorials section)
- Example: `examples/greenfield/rest-api-tutorial.md`

**For API Usage Guides**:
- Template: `templates/markdown/api-usage-guide.md`
- Reference: `reference/05-api-docs.md`
- Example: Can generate from OpenAPI spec via brownfield workflow

**For CLI Documentation**:
- Template: `templates/markdown/cli-documentation.md`
- Reference: `reference/11-cli-documentation.md`
- Example: `examples/greenfield/cli-getting-started.md`

### Step 3: Gather Developer Context

**Essential Information to Collect**:

1. **Learning Objective**:
   - What will developers learn from this tutorial?
   - What problem does this solve?
   - What's the end state? (working app, deployed API, etc.)

2. **Prerequisites**:
   - Required knowledge? (languages, frameworks, concepts)
   - Required tools? (Node.js, Docker, git, etc.)
   - Account requirements? (API keys, cloud accounts)

3. **Technical Stack**:
   - Programming language(s)?
   - Frameworks and libraries?
   - Development environment? (local, cloud, containers)

4. **Code Samples**:
   - Is there existing code to reference?
   - Should we create sample project from scratch?
   - GitHub repository for complete code?

5. **Depth and Complexity**:
   - Beginner, intermediate, or advanced?
   - Length? (15-min quick start or 2-hour deep dive)
   - Interactive elements? (live code, sandboxes)

**If context is missing**: Use AskUserQuestion to gather required details.

### Step 4: Customize Template with Developer's Context

**Developer Tutorial Structure**:

1. **Learning Objective** (What & Why):
   - Clear statement: "In this tutorial, you'll build..."
   - Why it matters: real-world use case
   - Time estimate: "~30 minutes"

2. **Prerequisites** (Checklist):
   - Knowledge: "Familiarity with JavaScript ES6+"
   - Tools: "Node.js 18+, npm, text editor"
   - Accounts: "GitHub account (free)"

3. **Project Setup** (Quick Win):
   - Clone repo or initialize project
   - Install dependencies
   - Verify setup with "Hello World"
   - **Goal**: Working output in < 5 minutes

4. **Step-by-Step Implementation** (Progressive):
   - Each step builds on the previous
   - Explain WHY before HOW
   - Show code + output for each step
   - Highlight key concepts inline

5. **Testing & Verification**:
   - How to run the project
   - Expected output
   - Common errors and fixes

6. **Extensions & Next Steps**:
   - "What you learned"
   - Advanced variations
   - Related tutorials
   - Links to deeper documentation

**API Usage Guide Structure**:

1. **API Overview**:
   - What the API does
   - Base URL and versioning
   - Rate limits and quotas

2. **Authentication**:
   - How to get API keys
   - Where to store credentials (env vars, config)
   - Example authenticated request

3. **Core Endpoints**:
   - List most important endpoints
   - Request/response examples
   - Common parameters

4. **Common Use Cases**:
   - Real-world scenarios with code
   - Best practices
   - Error handling

5. **SDKs and Libraries**:
   - Official client libraries
   - Community tools
   - Installation and usage

**CLI Documentation Structure**:

1. **Introduction**:
   - Tool purpose and capabilities
   - Installation

2. **Usage Overview**:
   - Basic syntax: `mycli <command> [options]`
   - Global flags
   - Help command

3. **Commands Reference**:
   - Each command in its own section
   - Syntax, description, flags
   - Examples (simple and complex)

4. **Configuration**:
   - Config file location and format
   - Environment variables
   - Precedence rules

5. **Examples & Workflows**:
   - Common tasks with full commands
   - Combining commands
   - Advanced usage patterns

6. **Error Handling**:
   - Exit codes and meanings
   - Common errors and solutions
   - Debug mode

### Step 5: Apply Developer Documentation Best Practices

**Code Quality**:
- ✅ All code examples are tested and working
- ✅ Use syntax highlighting (specify language)
- ✅ Show complete, runnable code (not fragments)
- ✅ Include imports/dependencies at top
- ✅ Comment complex logic
- ✅ Follow language style guides (PEP 8, ESLint, etc.)

**Progressive Complexity**:
- ✅ Start simple, add complexity gradually
- ✅ Each step adds ONE new concept
- ✅ Explain before implementing
- ✅ Show output/results after each step

**Explanations**:
- ✅ Explain "why" not just "what"
- ✅ Highlight key concepts in callouts
- ✅ Link to deeper documentation for advanced topics
- ✅ Anticipate and address common questions

**Interactive Elements**:
- ✅ Encourage experimentation
- ✅ Suggest variations to try
- ✅ Link to live code sandboxes (CodePen, CodeSandbox, Repl.it)
- ✅ Include "checkpoint" sections to verify progress

**Error Handling**:
- ✅ Show common errors and solutions
- ✅ Explain error messages
- ✅ Provide debugging tips
- ✅ Link to troubleshooting resources

**Tone & Voice**:
- ✅ Conversational but professional
- ✅ Encouraging and supportive
- ✅ Assume baseline technical knowledge
- ✅ Define new terms on first use

### Step 6: Add Visual Documentation

**When to Generate Diagrams**:
- **Tutorial**: Architecture diagram, data flow, component relationships
- **API Guide**: Sequence diagram for auth flow, API call patterns
- **CLI Docs**: Command syntax flowchart, decision trees for options

**Diagram Types**:
- **Sequence Diagrams** (PlantUML): API authentication flows, request/response cycles
- **Component Diagrams** (Mermaid): System architecture, module relationships
- **Flowcharts** (Mermaid): Decision logic, workflow processes

### Step 7: Code Examples and Samples

**Inline Code Examples**:
```markdown
Install dependencies:
```bash
npm install express dotenv
```

Create `server.js`:
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.json({ message: 'Hello World' });
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

Run the server:
```bash
node server.js
```

Output:
```
Server running on port 3000
```
```

**Complete Sample Projects**:
- Create GitHub repository with complete code
- Include README with setup instructions
- Add comments throughout code
- Provide working `package.json`, `requirements.txt`, etc.

**Code Snippets Library**:
- Reusable code blocks for common tasks
- Authentication examples
- Error handling patterns
- Database connection examples

### Step 8: Interactive Testing Guidance

**Help Developers Verify Their Work**:

1. **Checkpoint Sections**:
   ```markdown
   ## Checkpoint: Verify API Connection

   Run this command to test your setup:
   ```bash
   curl http://localhost:3000/health
   ```

   Expected output:
   ```json
   {"status": "ok"}
   ```

   If you see this, you're ready to proceed!
   ```

2. **Common Errors Section**:
   ```markdown
   ## Troubleshooting

   **Error: "EADDRINUSE: address already in use"**
   - **Cause**: Port 3000 is already in use
   - **Solution**: Kill process on port 3000 or change port in code

   **Error: "MODULE_NOT_FOUND"**
   - **Cause**: Dependencies not installed
   - **Solution**: Run `npm install`
   ```

3. **Self-Assessment**:
   ```markdown
   ## What You've Learned

   ✅ How to set up Express server
   ✅ How to create API endpoints
   ✅ How to handle errors gracefully

   ## Challenge

   Try adding a POST endpoint that accepts JSON data.
   Hint: Use `express.json()` middleware.
   ```

### Step 9: Review Quality Checklist

**All Developer Tutorials Must Have**:
- [ ] Clear learning objective stated upfront
- [ ] Prerequisites list (knowledge, tools, accounts)
- [ ] Time estimate
- [ ] Project setup with verification (< 5 min to working state)
- [ ] Progressive steps (each builds on previous)
- [ ] Complete, tested code examples
- [ ] Expected output shown for each step
- [ ] Checkpoint sections to verify progress
- [ ] Common errors and solutions
- [ ] "What you learned" summary
- [ ] Next steps and related resources
- [ ] Complete sample project in GitHub (if applicable)

**Technical Quality**:
- All code examples tested and working
- Syntax highlighting applied
- No security anti-patterns (hardcoded secrets, etc.)
- Best practices followed
- Error handling included

### Step 10: Generate Output

**Markdown Output** (Primary):
- Save as `.md` file
- Include table of contents for long tutorials
- Use proper heading hierarchy
- Include metadata (last tested date, version)

**Companion Files**:
- Complete code in GitHub repository
- `README.md` with setup instructions
- `.env.example` for configuration
- `package.json` / `requirements.txt` / etc.

**Optional Formats**:
- **Interactive Notebook**: Invoke `jupyter-notebook-converter` skill for `.ipynb`
- **PDF**: For offline distribution
- **Video**: Suggest recording screen capture walkthrough

**Output Location**:
- Save to `docs/tutorials/` or `docs/guides/`
- Use descriptive filename: `tutorial-build-rest-api-node.md`

---

## Common Patterns

### Pattern 1: REST API Tutorial
```markdown
# Build a Task Management API with Node.js

**Learning Objective**: Create a RESTful API with CRUD operations, authentication, and database persistence.

**Time**: ~45 minutes
**Level**: Intermediate

## Prerequisites
- Node.js 18+ installed
- Basic JavaScript knowledge
- Familiarity with REST concepts

## What You'll Build
A task management API with:
- User authentication (JWT)
- CRUD operations for tasks
- SQLite database
- Error handling

## Quick Setup (5 minutes)

1. **Clone starter project**:
   ```bash
   git clone https://github.com/example/task-api-starter
   cd task-api-starter
   npm install
   ```

2. **Start development server**:
   ```bash
   npm run dev
   ```

3. **Verify setup**:
   ```bash
   curl http://localhost:3000/health
   # Output: {"status":"ok"}
   ```

## Step 1: Create User Model
First, we'll define our User schema...

[Continue with progressive steps]
```

### Pattern 2: CLI Documentation
```markdown
# mycli Command Reference

**Version**: 2.1.0

## Installation
```bash
npm install -g mycli
# or
brew install mycli
```

## Usage
```
mycli <command> [options]
```

## Global Options
- `-h, --help`: Show help
- `-v, --version`: Show version
- `--verbose`: Enable debug output
- `--config <path>`: Specify config file

## Commands

### `mycli init`
Initialize a new project.

**Syntax**:
```bash
mycli init [directory] [options]
```

**Options**:
- `--template <name>`: Use template (default: basic)
- `--git`: Initialize git repository

**Examples**:
```bash
# Basic initialization
mycli init my-project

# With template
mycli init my-project --template=react

# Current directory
mycli init . --git
```

### `mycli build`
Build the project for production.

[Continue with each command]
```

### Pattern 3: API Usage Guide
```markdown
# Getting Started with ProductAPI

## Authentication

### 1. Get Your API Key
Sign up at https://product.com/api/keys and create an API key.

### 2. Authenticate Requests
Include your API key in the Authorization header:

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://api.product.com/v1/users
```

## Common Operations

### List Users
```bash
curl https://api.product.com/v1/users?limit=10
```

**Response**:
```json
{
  "users": [
    {"id": 1, "name": "Alice"},
    {"id": 2, "name": "Bob"}
  ],
  "total": 156,
  "page": 1
}
```

### Create User
```bash
curl -X POST https://api.product.com/v1/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Charlie","email":"charlie@example.com"}'
```

[Continue with more operations]
```

---

## Error Handling

**Issue**: Code examples don't work
**Solution**: Test all code before including; provide troubleshooting for common environment issues

**Issue**: Tutorial too complex for stated level
**Solution**: Break into multiple tutorials (Basic → Intermediate → Advanced)

**Issue**: No sample project repository
**Solution**: Create minimal repo with starter code, or provide inline code blocks for copy-paste

---

## Integration with Other Workflows

- **Brownfield Code-to-Docs**: Extract API usage examples from OpenAPI specs
- **Diagram Workflow**: Create sequence diagrams for API flows
- **Convert Workflow**: Export tutorials to PDF or Jupyter notebooks

---

## Success Criteria

✅ Tutorial can be completed by target audience in stated time
✅ All code examples tested and working
✅ Checkpoints verify progress at each step
✅ Common errors documented with solutions
✅ Complete sample project available (if applicable)
✅ Links to next steps and related resources

**Developer tutorials are effective when developers can complete them without external help and feel confident applying what they learned.**
