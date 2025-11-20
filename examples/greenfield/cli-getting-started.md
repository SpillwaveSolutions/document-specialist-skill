# Getting Started with TaskCLI

**Version**: 2.0.0
**Last Updated**: January 18, 2025

---

## Introduction

### What is TaskCLI?
TaskCLI is a powerful command-line task management tool that brings TaskMaster Pro's features to your terminal. Perfect for developers who prefer keyboard-driven workflows and automation.

### Why Use TaskCLI?
- **⚡ Fast**: Create and update tasks without leaving your terminal
- **🔁 Scriptable**: Automate task creation with shell scripts
- **🔌 Integrations**: Works with git hooks, CI/CD pipelines
- **🌐 Offline-first**: Syncs when online, works offline

### Target Audience
This guide is for developers familiar with command-line tools who want to manage tasks from the terminal.

---

## Quick Start (5 Minutes)

Get up and running in under 5 minutes:

### 1. Install
```bash
# Using npm
npm install -g taskcli

# Using Homebrew (macOS)
brew install taskcli

# Using pip (Python)
pip install taskcli
```

### 2. Authenticate
```bash
# Login with your TaskMaster Pro account
taskcli login

# Follow prompts:
# Email: your-email@example.com
# Password: ********
```

### 3. Create Your First Task
```bash
taskcli create "Fix documentation typos" --project=docs
```

**Expected Output**:
```
✓ Task created successfully
  ID: 42
  Title: Fix documentation typos
  Project: docs
  Status: To Do
  URL: https://taskmaster.pro/tasks/42
```

✅ **Success!** You've created your first task from the command line!

---

## Core Concepts

Before diving deeper, understand these key concepts:

### Projects
**Definition**: Containers for related tasks. Each task belongs to one project.

**Why It Matters**: Organize work by feature, team, or client.

**Example**:
```bash
# List your projects
taskcli projects

# Output:
# • docs (5 tasks)
# • api-v2 (12 tasks)
# • mobile-app (8 tasks)
```

---

### Task States
**Definition**: Tasks move through states: To Do → In Progress → Done

**Visual Representation**:
```
To Do → [You start] → In Progress → [You finish] → Done
```

**Key Points**:
- Tasks default to "To Do" when created
- Use `taskcli start <id>` to mark "In Progress"
- Use `taskcli complete <id>` to mark "Done"

---

### Filters and Queries
**Definition**: Find tasks using filters like `--assignee=me`, `--status=in-progress`

**Example**:
```bash
# My open tasks
taskcli list --assignee=me --status=open

# High-priority bugs
taskcli list --tag=bug --priority=high
```

---

## Installation

### System Requirements
- **Operating System**: macOS, Linux, Windows
- **Runtime**: Node.js 16+ (for npm) or Python 3.8+ (for pip)
- **Memory**: 50MB
- **Disk Space**: 100MB

### Prerequisites
Before installing, ensure you have:
- [ ] TaskMaster Pro account (sign up at https://taskmaster.pro)
- [ ] Package manager (npm, brew, or pip)
- [ ] Internet connection (for initial authentication)

### Installation Methods

#### Method 1: npm (Recommended for Node.js users)
```bash
npm install -g taskcli
```

**Verify installation**:
```bash
taskcli --version
```

Expected output: `taskcli version 2.0.0`

#### Method 2: Homebrew (macOS)
```bash
brew tap taskmasterpro/tap
brew install taskcli
```

#### Method 3: pip (Python users)
```bash
pip install taskcli
```

#### Method 4: Binary Download
1. Download from [releases page](https://github.com/taskmasterpro/cli/releases)
2. Extract archive
3. Add to PATH:
   ```bash
   # macOS/Linux
   sudo mv taskcli /usr/local/bin/

   # Windows
   # Add to PATH environment variable
   ```

---

## Configuration

### Authentication
```bash
# Interactive login
taskcli login

# API key authentication (for automation)
export TASKCLI_API_KEY="your-api-key"
taskcli whoami  # Verify authentication
```

### Default Project
Set a default project to skip `--project` flag:
```bash
taskcli config set default-project docs
```

### Configuration File
TaskCLI stores config in `~/.taskcli/config.json`:
```json
{
  "apiKey": "encrypted-key",
  "defaultProject": "docs",
  "editor": "vim",
  "theme": "dark"
}
```

**Edit config**:
```bash
taskcli config edit  # Opens in $EDITOR
```

---

## Your First Project Workflow

### Step 1: List Projects
```bash
taskcli projects

# Output:
# ID  Name        Tasks  Members
# 1   docs        5      Alice, Bob
# 2   api-v2      12     Alice, Charlie
# 3   mobile-app  8      Bob
```

### Step 2: Create a Task
```bash
taskcli create "Update getting started guide" \
  --project=docs \
  --assignee=me \
  --due="next Friday" \
  --tag=documentation
```

**What's Happening**:
- Creates task in "docs" project
- Assigns to you
- Sets due date to next Friday
- Adds "documentation" tag

### Step 3: List Your Tasks
```bash
taskcli list --assignee=me
```

**Output**:
```
ID  Title                          Status       Due
42  Update getting started guide   To Do        Jan 25
43  Fix API documentation          In Progress  Jan 23
44  Review tutorial PR             To Do        Jan 26
```

### Step 4: Start Working
```bash
taskcli start 42

# Output:
# ✓ Task #42 moved to "In Progress"
# ⏱ Timer started (optional feature)
```

### Step 5: Complete Task
```bash
taskcli complete 42 --comment="Updated CLI examples"

# Output:
# ✓ Task #42 marked as Done
# 📝 Comment added
# ⏱ Timer stopped: 1h 23m
```

---

## Common Workflows

### Workflow 1: Daily Standup
```bash
# What I did yesterday
taskcli list --assignee=me --completed-yesterday

# What I'm doing today
taskcli list --assignee=me --status=in-progress

# Blockers
taskcli list --assignee=me --tag=blocked
```

### Workflow 2: Sprint Planning
```bash
# Create sprint milestone
taskcli milestone create "Sprint 23" --start=2025-01-20 --end=2025-02-02

# Add tasks to sprint
taskcli create "Implement auth endpoint" \
  --milestone="Sprint 23" \
  --points=5

# View sprint progress
taskcli milestone show "Sprint 23"
```

### Workflow 3: Git Integration
```bash
# Create task from commit
git commit -m "Fix login bug" --allow-empty
taskcli create "$(git log -1 --pretty=%B)" --project=api-v2

# Link task to PR
gh pr create --title "Fix #42: Update getting started guide"
```

---

## CLI Reference (Quick Overview)

Full command reference: `taskcli help`

| Command | Description | Example |
|---------|-------------|---------|
| `taskcli create <title>` | Create new task | `taskcli create "Fix bug"` |
| `taskcli list` | List tasks | `taskcli list --assignee=me` |
| `taskcli show <id>` | Show task details | `taskcli show 42` |
| `taskcli update <id>` | Update task | `taskcli update 42 --status=done` |
| `taskcli start <id>` | Mark as in progress | `taskcli start 42` |
| `taskcli complete <id>` | Mark as done | `taskcli complete 42` |
| `taskcli comment <id>` | Add comment | `taskcli comment 42 "Fixed"` |

**Global flags**:
- `--json`: Output as JSON
- `--verbose`: Show debug info
- `--config <path>`: Custom config file

**Get help**:
```bash
taskcli --help           # General help
taskcli create --help    # Command-specific help
```

---

## FAQ

### General

**Q: Can I use TaskCLI offline?**
A: Yes! Tasks sync automatically when you reconnect. Offline changes show indicator (📴).

**Q: How do I uninstall?**
A:
```bash
# npm
npm uninstall -g taskcli

# Homebrew
brew uninstall taskcli

# Manual
rm -rf ~/.taskcli
rm /usr/local/bin/taskcli
```

### Troubleshooting

**Q: I get "Unauthorized" error - what does this mean?**
A: Your authentication expired. Run `taskcli login` again.

**Q: Tasks not syncing?**
A: Check internet connection and run `taskcli sync --force`.

**Q: How do I change my default text editor?**
A:
```bash
taskcli config set editor "code --wait"  # VS Code
taskcli config set editor "nano"         # Nano
```

---

## Next Steps

### Tutorials
Now that you have TaskCLI installed and running, try these tutorials:
1. **Automation**: [Automate task creation with Git hooks](link)
2. **Advanced Queries**: [Master task filtering and search](link)
3. **CI/CD Integration**: [Add tasks from GitHub Actions](link)

### Documentation
- **[CLI Reference](link)**: Complete command documentation
- **[API Guide](link)**: Build custom integrations
- **[Troubleshooting](link)**: Common issues and solutions

### Community & Support
- **GitHub**: https://github.com/taskmasterpro/cli
- **Discord**: https://discord.gg/taskmasterpro
- **Stack Overflow**: Tag `taskcli`
- **Email**: cli-support@taskmaster.pro

---

## Sample Scripts

### Daily Status Report
```bash
#!/bin/bash
# Save as ~/bin/daily-status.sh
echo "📊 Daily Status Report"
echo "====================="
echo ""
echo "✅ Completed Yesterday:"
taskcli list --assignee=me --completed-yesterday --format=simple
echo ""
echo "🔄 In Progress:"
taskcli list --assignee=me --status=in-progress --format=simple
echo ""
echo "📋 Up Next:"
taskcli list --assignee=me --status=todo --limit=5 --format=simple
```

### Git Commit Hook
```bash
#!/bin/bash
# Save as .git/hooks/post-commit
COMMIT_MSG=$(git log -1 --pretty=%B)
taskcli create "$COMMIT_MSG" --project=dev --tag=from-git
```

---

## Additional Resources

### Video Tutorials
- [TaskCLI in 5 Minutes](https://www.youtube.com/watch?v=example)
- [Advanced Automation Techniques](https://www.youtube.com/watch?v=example)

### Blog Posts
- [Why We Built TaskCLI](https://blog.taskmaster.pro/why-cli)
- [10 TaskCLI Tips for Power Users](https://blog.taskmaster.pro/10-tips)

---

**Welcome to TaskCLI!** 🎉

Now that you're set up, start managing tasks from your terminal!

**Quick Reference Card**: https://taskmaster.pro/cli/cheatsheet.pdf
