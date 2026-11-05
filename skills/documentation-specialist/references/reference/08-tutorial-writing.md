# Tutorial Writing Best Practices

**Version**: 1.0.0
**Token Budget**: ~450 tokens
**Last Updated**: 2025-01-18

---

## Overview

This guide covers best practices for writing three types of learning-focused documentation:
1. **User Manuals**: Comprehensive reference for end-users
2. **How-To Guides**: Task-oriented instructions
3. **Developer Tutorials**: Project-based learning for technical audiences

---

## Document Type Distinctions

| Aspect | User Manuals | How-To Guides | Developer Tutorials |
|--------|--------------|---------------|---------------------|
| **Purpose** | Reference, troubleshooting | Complete specific task | Teach concepts/skills |
| **Structure** | Modular by feature | Step-by-step single task | Progressive narrative |
| **Audience** | End-users (broad) | End-users (focused) | Developers/technical |
| **Tone** | Neutral, instructional | Friendly, direct | Conversational, explanatory |
| **Examples** | Use cases, workflows | Screenshots per step | Code, sample projects |

---

## User Manual Best Practices

### Structure
```
1. Introduction (What & Who)
2. Getting Started (Quick Win < 5 min)
3. Features Reference (Modular sections)
4. Troubleshooting & FAQ
5. Support Resources
```

### Key Principles
- **Modular**: Each feature in own section
- **Scannable**: Headings, bullets, tables
- **Visual**: Screenshot for every UI interaction
- **Accessible**: WCAG-compliant (alt text, headings)

### Tone
- Second person ("you")
- Active voice ("Click Save" not "Save is clicked")
- Define jargon or link to glossary
- Explain "why" not just "how"

---

## How-To Guide Best Practices

### Structure
```
1. Problem Statement (What task)
2. Prerequisites
3. Step-by-Step Instructions (numbered)
4. Visual Aids (screenshots)
5. Verification (How to confirm success)
6. Related Guides (next steps)
```

### Key Principles
- **Atomic**: One task per guide
- **Concrete**: Realistic examples
- **Current**: Last updated date visible
- **Focused**: No tangents

### Visual Guidelines
- Screenshot at each key step
- Annotate images (arrows, highlights)
- Alt text for accessibility
- Consistent zoom/resolution

---

## Developer Tutorial Best Practices

### Structure
```
1. Learning Objective (What you'll build)
2. Prerequisites (knowledge, tools)
3. Project Setup (< 5 min to working state)
4. Progressive Steps (each builds on previous)
5. Testing & Verification
6. Extensions & Next Steps
```

### Key Principles
- **Progressive**: Simple → Complex
- **Tested**: All code examples work
- **Explanatory**: Explain WHY before HOW
- **Interactive**: Checkpoints to verify progress

### Code Quality
- Syntax highlighting with language tags
- Complete, runnable code (not fragments)
- Include imports/dependencies
- Comment complex logic
- Follow style guides (PEP 8, ESLint)

### Checkpoint Pattern
```markdown
## Checkpoint: Verify API Connection
Run this command:
```bash
curl http://localhost:3000/health
```

Expected: `{"status":"ok"}`
✅ If you see this, proceed!
```

---

## Getting Started Guide Best Practices

### Structure
```
1. Introduction (What & Why)
2. Quick Start (< 5 min, copy-paste commands)
3. Core Concepts (key terminology)
4. First Project (hands-on)
5. FAQ
6. Next Steps
```

### Quick Start Requirements
- Commands ready for copy-paste
- Clear expected output
- Verification step
- Under 5 minutes total

### Core Concepts Section
- Define 3-5 key terms
- Simple explanations
- No jargon without definition

---

## CLI Documentation Best Practices

### Required Sections
1. **Installation** (multiple methods)
2. **Usage Overview** (syntax)
3. **Commands Reference** (each command detailed)
4. **Configuration** (files, env vars)
5. **Examples** (common workflows)
6. **Error Handling** (exit codes)

### Command Documentation Pattern
```markdown
### `cli command [options]`
Description of what it does.

**Syntax**:
```bash
cli command <required> [optional]
```

**Options**:
- `--flag`: Description

**Examples**:
```bash
# Simple
cli command file.txt

# Advanced
cli command file.txt --verbose --output=json
```
```

### Best Practices
- Document ALL public flags
- Provide `--help` and `--version`
- Show error messages and solutions
- Include exit codes table

---

## Visual Documentation

### When to Use Diagrams

**User Manuals**:
- Feature flowcharts
- System context (C4)

**How-To Guides**:
- Process flowcharts
- Decision trees

**Developer Tutorials**:
- Architecture diagrams
- Sequence diagrams (auth flows)
- Data flow diagrams

### Screenshot Guidelines
- Capture full relevant UI section
- Consistent resolution/zoom
- Add annotations (arrows, highlights)
- Alt text: `![Action description](image.png)`
- Web-friendly format (PNG, WebP)

---

## Accessibility Requirements (2025)

### WCAG Compliance
- ✅ Proper heading hierarchy (H1 → H2 → H3)
- ✅ Alt text for all images
- ✅ Color contrast (4.5:1 minimum)
- ✅ No color-only instructions
- ✅ Keyboard navigation described
- ✅ Captions for videos

### Inclusive Language
- Avoid jargon without definition
- Use simple, clear sentences
- Consider multilingual users
- Screen reader friendly

---

## Modern Approaches (2025)

### Docs as Code
- Markdown in version control
- Review process like code
- Automated testing of examples
- CI/CD for documentation

### AI Enhancement
- AI draft generation
- Automated gap detection
- Version consistency checks
- Smart search/discoverability

### Rich Media
- Video tutorials
- Interactive code sandboxes
- Live demos
- AR/VR for complex systems

---

## Quality Checklist

### All Documentation
- [ ] Clear title and description
- [ ] Version number and last updated date
- [ ] Target audience identified
- [ ] Prerequisites listed
- [ ] Verified/tested procedures
- [ ] Visual aids (diagrams/screenshots)
- [ ] No spelling/grammar errors
- [ ] Consistent formatting
- [ ] Feedback mechanism

### User-Facing Docs
- [ ] Friendly, approachable tone
- [ ] No unexplained jargon
- [ ] Common issues addressed
- [ ] Support contact info

### Developer Docs
- [ ] All code tested and working
- [ ] Complete sample project
- [ ] Common errors documented
- [ ] Links to advanced topics

---

## Common Mistakes to Avoid

❌ **Too much theory upfront**: Start with hands-on
❌ **Untested code examples**: All code must work
❌ **Missing prerequisites**: Always list requirements
❌ **No visual aids**: Screenshots essential
❌ **Outdated content**: Date last reviewed
❌ **No verification steps**: Show expected output
❌ **Assuming knowledge**: Define all terms
❌ **Poor structure**: Use clear headings
❌ **No troubleshooting**: Address common errors

---

## Performance & Usability

### Testing Your Documentation
1. **Fresh eyes test**: Have someone unfamiliar follow it
2. **Time estimate**: Actually time how long it takes
3. **Error collection**: Note every stumbling block
4. **Feedback loop**: Add FAQ based on questions

### Continuous Improvement
- Monitor analytics (where users get stuck)
- User feedback forms
- Regular review cycles (quarterly)
- Update when product changes

---

## References

**Industry Standards**:
- IEEE 830 (Software Requirements)
- OpenAPI 3.0 Specification
- WCAG 2.1 (Accessibility)

**Further Reading**:
- [Diátaxis Documentation Framework](https://diataxis.fr/)
- [Google Developer Documentation Style Guide](https://developers.google.com/style)
- [Write the Docs Community](https://www.writethedocs.org/)

---

**Apply these practices to create documentation that users actually want to read!** 📚
