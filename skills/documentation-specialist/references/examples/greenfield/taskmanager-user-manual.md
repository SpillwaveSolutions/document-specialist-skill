# TaskMaster Pro User Manual

**Version**: 3.2.0
**Last Updated**: January 18, 2025
**Author**: TaskMaster Documentation Team

---

## Table of Contents
1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Features](#features)
4. [Troubleshooting](#troubleshooting)
5. [FAQ](#faq)
6. [Support](#support)

---

## Introduction

### What is TaskMaster Pro?
TaskMaster Pro is a collaborative task management platform designed to help teams organize projects, track progress, and meet deadlines efficiently. With real-time updates, customizable workflows, and powerful reporting, TaskMaster Pro keeps your team aligned and productive.

### Who Should Use This Manual?
This manual is for end-users (team members, project managers, and administrators) who want to learn how to use TaskMaster Pro effectively.

### Document Scope
This manual covers:
- ✅ Creating and managing tasks
- ✅ Team collaboration features
- ✅ Project boards and workflows
- ✅ Reporting and analytics
- ❌ API integration (see Developer Guide)
- ❌ Enterprise administration (see Admin Guide)

---

## Getting Started

### Prerequisites
Before you begin, ensure you have:
- [ ] An active TaskMaster Pro account
- [ ] Modern web browser (Chrome 90+, Firefox 88+, Safari 14+)
- [ ] Team invitation link (for joining existing workspace)

### First-Time Setup

#### Step 1: Create Your Account
1. Navigate to https://taskmaster.pro/signup
2. Enter your email address and create a strong password
3. Verify your email by clicking the link sent to your inbox

#### Step 2: Set Up Your Profile
1. Click your avatar in the top-right corner
2. Select "Profile Settings"
3. Add your name, photo, and time zone
4. Click "Save Changes"

**✅ Verification**: Your profile photo should now appear in the top-right corner.

#### Step 3: Join or Create a Workspace
**To join existing workspace**:
1. Click the invitation link from your team
2. Accept the invitation

**To create new workspace**:
1. Click "Create Workspace" from dashboard
2. Enter workspace name and description
3. Invite team members by email

### Quick Start Guide (5 Minutes)
To get productive immediately:
1. **Create your first task**: Click "+ New Task", add title and due date
2. **Assign it**: Click task → Select assignee from dropdown
3. **Track progress**: Drag task between "To Do", "In Progress", "Done" columns

---

## Features

### Feature 1: Task Management

#### Overview
Tasks are the core building blocks of TaskMaster Pro. Each task can have a title, description, assignee, due date, priority, tags, and attachments.

#### How to Create a Task
1. **Open your project board**:
   - Click "Projects" in left sidebar
   - Select the project you want to add a task to

2. **Create the task**:
   - Click the "+ New Task" button
   - Fill in task details:
     - **Title**: Brief description (e.g., "Design landing page")
     - **Description**: Detailed requirements (supports Markdown)
     - **Assignee**: Team member responsible
     - **Due Date**: Target completion date
     - **Priority**: High, Medium, or Low
     - **Tags**: Optional labels (e.g., "design", "urgent")

3. **Save the task**:
   - Click "Create Task"
   - Task appears in "To Do" column

#### Common Use Cases
- **Bug tracking**: Use "bug" tag and High priority
- **Feature requests**: Link to design documents in description
- **Recurring tasks**: Use task templates (see Templates section)

#### Tips & Best Practices
💡 **Tip**: Use Markdown in descriptions for formatting:
```markdown
## Requirements
- [ ] Responsive design
- [ ] Mobile-first
- [ ] Accessibility (WCAG 2.1)
```

⚠️ **Warning**: Tasks deleted from "Done" column are permanently removed after 30 days.

---

### Feature 2: Project Boards

#### Overview
Project boards visualize your team's workflow using customizable columns. Move tasks between columns to track progress from start to finish.

#### How to Create a Project Board
1. **Navigate to Projects**:
   - Click "Projects" in sidebar
   - Click "+ New Project"

2. **Configure your board**:
   - **Name**: Project name
   - **Template**: Choose workflow template:
     - **Kanban**: To Do → In Progress → Done
     - **Scrum**: Backlog → Sprint → In Progress → Review → Done
     - **Custom**: Create your own columns
   - **Members**: Add team members

3. **Create the board**:
   - Click "Create Project"
   - Customize columns by clicking "Board Settings"

#### Advanced Options
For power users:
- **Automation**: Auto-move tasks when status changes
- **Swim Lanes**: Group tasks by assignee or priority
- **WIP Limits**: Set maximum tasks per column

---

### Feature 3: Real-Time Collaboration

#### Overview
TaskMaster Pro updates in real-time. See changes as teammates edit tasks, move cards, or add comments.

#### How to Collaborate
1. **Comments**:
   - Click any task
   - Type comment in text box
   - Mention teammates with `@username`
   - Attach files by drag-and-drop

2. **Activity Feed**:
   - View all project activity in right sidebar
   - Filter by team member or action type

3. **Notifications**:
   - Get notified when:
     - You're mentioned in a comment
     - Task assigned to you
     - Due date approaching
   - Configure in Settings → Notifications

#### Tips
💡 Use `@all` to notify entire team
💡 Reactions (👍 ❤️ 🎉) provide quick feedback

---

## Troubleshooting

### Common Issues

#### Issue: Can't See Tasks in Project
**Symptoms**: Project board appears empty
**Cause**: Filter settings hiding tasks
**Solution**:
1. Click "Filter" button in top-right
2. Reset filters: Click "Clear All"
3. Tasks should now be visible

**Prevention**: Check filter status indicator in toolbar

---

#### Issue: Task Not Updating in Real-Time
**Symptoms**: Changes made by teammates not appearing
**Cause**: Browser cache or network connectivity
**Solution**:
1. Refresh page (Ctrl+R / Cmd+R)
2. Check internet connection
3. Clear browser cache: Settings → Privacy → Clear Cache

---

#### Issue: Can't Upload Attachments
**Symptoms**: "Upload failed" error message

| Error Message | Cause | Solution |
|---------------|-------|----------|
| "File too large" | File > 25MB | Compress file or use cloud link |
| "File type not supported" | Executable files blocked | Upload as .zip or link to cloud storage |
| "Quota exceeded" | Workspace storage full | Upgrade plan or delete old files |

---

## FAQ

### General Questions

**Q: Is there a mobile app?**
A: Yes! Download TaskMaster Pro from App Store (iOS) and Google Play (Android).

**Q: Can I work offline?**
A: Yes, changes sync when you reconnect. Tasks show offline indicator (📴).

**Q: How many projects can I create?**
A: Depends on plan:
- Free: 3 projects
- Pro: 25 projects
- Enterprise: Unlimited

### Account & Billing

**Q: How do I upgrade my plan?**
A: Settings → Billing → Select new plan → Confirm

**Q: Can I cancel anytime?**
A: Yes, cancel in Settings → Billing. Access continues until period end.

### Technical Questions

**Q: What browsers are supported?**
A:
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

---

## Support

### Getting Help

**Documentation Resources**:
- 📘 User Manual (this document)
- 📗 [Video Tutorials](https://taskmaster.pro/learn)
- 📙 [API Documentation](https://api.taskmaster.pro/docs)
- 🎓 [TaskMaster Academy](https://academy.taskmaster.pro)

**Contact Support**:
- **Email**: support@taskmaster.pro
- **Phone**: 1-800-TASK-PRO (Mon-Fri 9AM-6PM EST)
- **Live Chat**: Click chat icon in bottom-right
- **Help Center**: https://help.taskmaster.pro

**Response Times**:
- Free: 48 hours
- Pro: 24 hours
- Enterprise: 4 hours (priority support)

### Community Resources
- **Forum**: https://community.taskmaster.pro
- **Feature Requests**: https://ideas.taskmaster.pro
- **Status Page**: https://status.taskmaster.pro
- **Twitter**: [@TaskMasterPro](https://twitter.com/taskmasterpro)

---

## Appendix

### Glossary
- **Board**: Visual workspace containing tasks organized in columns
- **Sprint**: Time-boxed period for completing tasks (Scrum methodology)
- **Tag**: Label for categorizing tasks (e.g., "bug", "feature")
- **Workspace**: Top-level container for teams and projects
- **WIP Limit**: Work In Progress limit - maximum tasks allowed in a column

### Keyboard Shortcuts
| Action | Windows/Linux | macOS |
|--------|---------------|-------|
| New Task | Ctrl+N | Cmd+N |
| Search | Ctrl+K | Cmd+K |
| Quick Switch Project | Ctrl+P | Cmd+P |
| Toggle Sidebar | Ctrl+\\ | Cmd+\\ |

### Version History
| Version | Date | Changes |
|---------|------|---------|
| 3.2.0 | Jan 2025 | Added automation rules, swim lanes |
| 3.1.0 | Dec 2024 | Real-time collaboration improvements |
| 3.0.0 | Nov 2024 | New UI redesign, dark mode |

---

**© 2025 TaskMaster Technologies Inc. All rights reserved.**
