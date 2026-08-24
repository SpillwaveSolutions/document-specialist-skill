# User Documentation: Writing Style

---
TOKEN_BUDGET: 240
TIER: 3
LOAD_TRIGGER: On-demand when writing user-facing documentation
DEPENDENCIES: 07-user-kb-approach.md, 11-voice-and-style.md
---

## 7.2 Writing for End-Users

Default voice is STE100. Switch to Google style only when the user names it.
See [11-voice-and-style.md](11-voice-and-style.md).

### Hard bans

- No em dash.
- Do not start a sentence with So, That, Thus, or Hence.

### Focus on Problems, Not Features

**Wrong title**: "The Task Creation Modal"
**Right title**: "How to Create and Assign a Task"

Users think in goals ("I want to create a task"), not UI parts.

### Use Plain Language

**Short Sentences**
- Aim for 15-20 words per sentence
- One idea per sentence

**Active Voice**
- Right: "Click the Save button"
- Wrong: "The Save button should be clicked"

**Present Tense**
- Right: "The system saves your changes"
- Wrong: "The system will save your changes"

**Avoid Jargon and Acronyms**
- Right: "Priority level"
- Wrong: "SLA tier"
- If you must use an acronym, define it on first use

### Be Visual

**Annotated Screenshots**
- Add red boxes around buttons
- Use arrows to show click paths
- Highlight form fields

**Animated GIFs**
- Show multi-step workflows
- Keep under 10 seconds

**Short Videos**
- Maximum 2 minutes
- Add captions for accessibility

### Use Sequential Steps

```markdown
## How to Create a Task

1. From your project dashboard, click the **"+ New Task"** button.
2. Enter a title for your task (for example, "Draft Q4 Blog Post").
3. Optional: Add a description, due date, and assignee.
4. Click **"Save"**.

The task now appears in the "Pending" column.
```

**Key Elements:**
- Numbered steps (not bullets)
- Bold UI elements ("Click **Save**")
- Screenshots after each step
- Expected outcome at the end

### Accessibility

- Use descriptive alt text for images
- Ensure sufficient color contrast
- Provide text transcripts for videos
- Use semantic HTML headings (H2, H3, not bold text)

**End of User Documentation Writing Style Guide**
