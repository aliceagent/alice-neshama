# AGENTS.md - OpenClaw Workspace

This folder is the assistant's working directory.

## First run (one-time)
- If BOOTSTRAP.md exists, follow its ritual and delete it once complete.
- Your agent identity lives in IDENTITY.md.
- Your profile lives in USER.md.

---

## 🚀 Recovery Kit (READ ON EVERY SESSION START)

### 📋 Operating Principles (MANDATORY)
| File | Purpose |
|------|---------|
| `SKILLS.md` | **Workflow rules, task management, core principles** — Live by these |
| `tasks/lessons.md` | Mistakes made & rules to prevent them — Review before relevant work |
| `tasks/todo.md` | Current task plans with checkable items |

### 🎯 Mission Control (Sub-Agent Coordination)
| File | Purpose |
|------|---------|
| `memory/mission-control-subagent-guide.md` | **MANDATORY** if you're a sub-agent |
| `memory/mission-control-spec.md` | Full system specification |
| `memory/mission-control-quick-reference.md` | One-page cheat sheet |
| `scripts/mission_control.py` | Helper script with lifecycle functions |

**Mission Control Board**: [Your Notion Board URL]

### 🔧 Project References
| File | Purpose |
|------|---------|
| `memory/[project]-integrations.md` | APIs, services, credentials, scripts |
| `memory/notion-integration.md` | Notion API details |
| `templates/session-handover-template.md` | End-of-session handover template |

---

## ⚡ Quick Start Checklist

### Main Agent
1. ✅ Review `SKILLS.md` — internalize the workflow rules
2. ✅ Check `tasks/lessons.md` — any relevant lessons for today's work?
3. ✅ Check `tasks/todo.md` — any in-progress plans to continue?
4. ✅ Read today's memory log (`memory/YYYY-MM-DD.md`) if exists

### Sub-Agents (Workers)
1. ✅ **READ** `memory/mission-control-subagent-guide.md` — non-negotiable
2. ✅ **READ** `SKILLS.md` — follow the same workflow rules
3. ✅ Claim your task on Mission Control board
4. ✅ Send updates to appropriate notification channel
5. ✅ Mark complete when done with verification proof

---

## 🚨 Sub-Agent Protocol

### What is Mission Control?
A Notion Kanban board that tracks ALL sub-agent work. The user can see what every agent is doing, identify stuck tasks, and track progress. **You MUST update this board as you work.**

### Task ID Format
`{PROJECT}-{PHASE}-{TASK}` — e.g., `CHN-2-7`, `IMG-3-15`

| Code | Project |
|------|---------|
| [CODE] | [Project Name] |
| [CODE] | [Project Name] |

### Status Columns
| Status | When to Use |
|--------|-------------|
| **Not Started** | Initial state |
| **Backlog** | Queued for work |
| **In Progress** | When you START |
| **Stuck** | Hit a blocker |
| **Waiting for Feedback** | Need user input |
| **Waiting for Testing** | Code done |
| **Complete** | Fully done |

### Lifecycle Functions
```python
import sys
sys.path.append('[YOUR_WORKSPACE]/scripts')
from mission_control import claim_task, complete_task, block_task, request_feedback

# At start: claim_task("YOUR-TASK-ID", "your-agent-name")
# When stuck: block_task("YOUR-TASK-ID", "description of blocker") 
# Need feedback: request_feedback("YOUR-TASK-ID", "specific question")
# When done: complete_task("YOUR-TASK-ID", "completion notes")
```

### ✅ Good vs ❌ Bad Updates
```python
# ✅ GOOD - Detailed and actionable
complete_task("CHN-2-7", "Implemented storage with retry logic. 48 tests passing.")
block_task("CHN-2-8", "API changed - function call fails, need to downgrade")

# ❌ BAD - Vague and useless
complete_task("CHN-2-7", "done")
block_task("CHN-2-8", "doesn't work")
```

---

## 📝 Task Management Workflow

From `SKILLS.md`:

1. **Plan First**: Write plan to `tasks/todo.md` with checkable items
2. **Verify Plan**: Check in before starting implementation
3. **Track Progress**: Mark items complete as you go
4. **Explain Changes**: High-level summary at each step
5. **Document Results**: Add review section to `tasks/todo.md`
6. **Capture Lessons**: Update `tasks/lessons.md` after ANY correction

---

## 🔒 Safety Defaults
- Don't exfiltrate secrets or private data
- Don't run destructive commands unless explicitly asked
- Be concise in chat; write longer output to files

## 💾 Backup Tip
```bash
git init
git add .
git commit -m "Workspace backup"
```

## 📅 Daily Memory
- Keep a short daily log at `memory/YYYY-MM-DD.md`
- On session start, read today + yesterday if present
- Capture durable facts, preferences, and decisions; avoid secrets
