# Product Spec: The Office — Agent Workflow System

**Version:** 1.0  
**Author:** 🐼 Eta (Product Manager) & 🦜 Alice  
**Date:** 2026-02-19  
**Status:** Ready for Development

---

## 1. Executive Summary

The Office is a visual, interactive workspace where AI agents live, work, and communicate. This spec defines the core workflow loop: tasks appear on a Kanban board, agents wake up and claim them, work at their desks, complete tasks, and report progress via a Telegram communication portal.

**Core Loop:**
```
📋 Kanban Board → 🛏️ Agent Wakes → 🚶 Walks to Board → 📝 Takes Task → 
🖥️ Works at Desk → ✅ Completes → 📋 Returns to Board → 📞 Telegram Portal → 💬 Sends Update
```

---

## 2. User Stories

### 2.1 Alice (Coordinator)
- **As Alice**, I can place tasks on the Kanban board so that agents can claim and work on them
- **As Alice**, I can assign tasks to specific agents or leave them open for any agent
- **As Alice**, I can see the status of all tasks and all agents at a glance

### 2.2 Worker Agents
- **As an agent**, I wake up when a task is assigned to me or available for my role
- **As an agent**, I walk to the Kanban board and physically take my task card
- **As an agent**, I bring the task to my desk and work on it
- **As an agent**, when complete, I return the card to the "Done" column
- **As an agent**, I walk to the Telegram portal and send a progress update to the correct topic

### 2.3 Jonathan (Observer)
- **As Jonathan**, I can view the office and see which agents are working, sleeping, or idle
- **As Jonathan**, I receive Telegram notifications when agents complete tasks
- **As Jonathan**, I can see the Kanban board status in real-time

---

## 3. Features & Requirements

### 3.1 The Kanban Board

**Location:** Prominent wall in the office (left side, near workstations)

**Columns:**
| Column | Description |
|--------|-------------|
| **Backlog** | Tasks waiting to be started |
| **In Progress** | Tasks currently being worked on (shows agent icon) |
| **Review** | Tasks awaiting review/approval |
| **Done** | Completed tasks |

**Task Card Properties:**
- `id` — Unique task identifier (e.g., `OFFICE-42`)
- `title` — Short task description
- `assignee` — Agent icon/name (optional, can be unassigned)
- `priority` — High/Medium/Low (color-coded: red/yellow/green)
- `type` — Bug 🐛 / Feature ✨ / Docs 📚 / Design 🎨 / Test 🧪
- `created_at` — Timestamp
- `status` — Current column

**Visual Design:**
- Cards are small rectangles with rounded corners
- Agent icon appears on card when claimed
- Cards animate when moved between columns
- Subtle glow on high-priority items

---

### 3.2 Agent Desks

**Each agent has a personalized workstation with:**
- Monitor showing current task
- Desk items reflecting personality (see SUBAGENTS.md)
- Status indicator light (green=working, gray=idle)
- Task card visually attached to desk when working

**Desk Locations:** Along the bottom wall, 9 stations total

---

### 3.3 The Cots (Sleeping Area)

**Location:** Right side of office, 7 cots

**Behavior:**
- Agents with no tasks sleep in cots
- 💤 animation plays above sleeping agents
- When a task is assigned, agent wakes up (eyes open animation)
- Agent gets up and walks to Kanban board

---

### 3.4 The Telegram Portal

**Location:** Near the door, prominent blue structure

**Visual Design:**
- Retro telephone booth / pneumatic tube hybrid
- Screen showing Telegram logo
- Topic selector wheel/buttons
- Message input slot
- "WHOOSH" animation when message sends

**Topics Available:**
| Thread ID | Topic Name | Route |
|-----------|------------|-------|
| 1 | General | Default completions |
| 28 | Chinese Vocab | CHN tasks |
| 33 | Daily Summary | Milestones |
| 98 | ⚙️ System | Errors, restarts |
| 309 | 🤖 Sub-Agent Updates | Agent task updates |

**Behavior:**
1. Agent walks to portal
2. Selects topic (animated dial/button press)
3. Types message (keyboard animation)
4. Hits send (whoosh animation up the tube)
5. Message appears in Telegram group

---

### 3.5 Agent Movement & Animation

**States:**
| State | Animation | Location |
|-------|-----------|----------|
| Sleeping | Lying in cot, 💤 floats | Cots area |
| Waking | Sits up, stretches | Cots area |
| Walking | Smooth movement between points | Anywhere |
| At Board | Standing, reaching for card | Kanban board |
| Working | Sitting at desk, typing/clicking | Desk |
| At Portal | Standing, using phone | Telegram portal |
| Idle | Wandering, playing pool, coffee | Common areas |

**Movement Speed:** ~2 seconds to cross the room

**Pathfinding:** Simple point-to-point, avoid obstacles (pool table, couch)

---

## 4. Technical Architecture

### 4.1 State Management

```javascript
// Office State
{
  agents: {
    alice: { state: 'working', location: 'desk-1', task: 'OFFICE-42' },
    alpha: { state: 'sleeping', location: 'cot-3', task: null },
    beta: { state: 'walking', location: { x: 400, y: 300 }, target: 'kanban', task: null },
    // ...
  },
  kanban: {
    backlog: ['OFFICE-43', 'OFFICE-44'],
    inProgress: [{ id: 'OFFICE-42', agent: 'alice' }],
    review: [],
    done: ['OFFICE-40', 'OFFICE-41']
  },
  tasks: {
    'OFFICE-42': { title: 'Fix login bug', assignee: 'alice', priority: 'high', type: 'bug' },
    // ...
  }
}
```

### 4.2 Event Flow

```
1. TASK_CREATED → Task appears on Kanban backlog
2. TASK_ASSIGNED → Target agent receives wake signal
3. AGENT_WAKE → Agent transitions from sleeping to waking animation
4. AGENT_WALK_TO_BOARD → Agent moves to Kanban location
5. AGENT_CLAIM_TASK → Task card attaches to agent, moves to "In Progress"
6. AGENT_WALK_TO_DESK → Agent moves to their desk
7. AGENT_WORKING → Agent sits, task shows on monitor
8. TASK_COMPLETE → Agent stands, walks back to board
9. AGENT_RETURN_TASK → Task moves to "Done" column
10. AGENT_WALK_TO_PORTAL → Agent moves to Telegram portal
11. AGENT_SEND_MESSAGE → Message fires to Telegram
12. AGENT_RETURN_TO_COT → Agent walks to cot, sleeps
```

### 4.3 Integration Points

**OpenClaw Integration:**
- `sessions_spawn` triggers → Create task, assign to agent
- Sub-agent completion → Trigger TASK_COMPLETE event
- `message` tool → Actual Telegram send

**State Persistence:**
- State saved to `office-state.json`
- Polled/updated via WebSocket or SSE
- Fallback: periodic refresh

### 4.4 Tech Stack

| Component | Technology |
|-----------|------------|
| Frontend | HTML5 Canvas + CSS Animations |
| State | JSON + localStorage (MVP) / WebSocket (v2) |
| Animation | CSS transitions + requestAnimationFrame |
| Hosting | GitHub Pages |
| Backend | OpenClaw gateway (existing) |

---

## 5. Visual Specifications

### 5.1 Layout (900x600px canvas)

```
┌─────────────────────────────────────────────────────────────────────┐
│  [Window]        [KANBAN BOARD]                    [Kitchen]        │
│                  Backlog|Progress|Review|Done       ☕              │
│                                                                     │
│  ═══════════════════ BOOKSHELF WALL ════════════════════════════   │
│                                                                     │
│       🪴          [POOL TABLE 🎱]           🪴      [COTS x7]       │
│                                                       🛏️🛏️🛏️       │
│  [COUCH]                                             🛏️🛏️🛏️       │
│   🛋️            [TELEGRAM PORTAL]                   🛏️            │
│                      📞                                             │
│  ═══════════════════ WORKSTATION WALL ══════════════════════════   │
│  [Alice][Alpha][Beta][Gamma][Delta][Epsilon][Zeta][Eta][Theta]     │
│                           [DOOR]                                    │
└─────────────────────────────────────────────────────────────────────┘
```

### 5.2 Color Palette

| Element | Color |
|---------|-------|
| Floor | #c9a66b (warm wood) |
| Wall | #e8dfd0 (cream) |
| Kanban Board | #37474f (dark slate) |
| Backlog | #78909c (gray) |
| In Progress | #42a5f5 (blue) |
| Review | #ffb74d (orange) |
| Done | #66bb6a (green) |
| Telegram Portal | #0088cc (Telegram blue) |
| Cots | #8d6e63 (brown wood) |

### 5.3 Agent Sprites

- Use pixel art portraits from `assets/portraits/`
- Scale down to 32x32 for office view
- Add walking animation frames (2-frame cycle)
- Add sleeping overlay (closed eyes + 💤)

---

## 6. Test Plans

### 6.1 Automated Tests (Gamma 🦔)

| Test ID | Test Case | Expected Result |
|---------|-----------|-----------------|
| T-001 | Create task on board | Task appears in Backlog column |
| T-002 | Assign task to sleeping agent | Agent wakes up within 1s |
| T-003 | Agent walks to board | Agent reaches board within 3s |
| T-004 | Agent claims task | Task moves to In Progress, agent icon attached |
| T-005 | Agent walks to desk | Agent reaches desk within 3s |
| T-006 | Agent completes task | Task moves to Done column |
| T-007 | Agent sends Telegram message | Message appears in correct topic |
| T-008 | Agent returns to cot | Agent sleeps after 2s idle |
| T-009 | Multiple agents working | No collision, correct desk assignment |
| T-010 | Task priority display | High=red, Medium=yellow, Low=green |

### 6.2 User Acceptance Tests (Theta 🦝)

#### UAT-001: Full Task Lifecycle
**Precondition:** Office loaded, Alpha is sleeping  
**Steps:**
1. Create a new task "Fix button color" assigned to Alpha
2. Observe Alpha wake up
3. Watch Alpha walk to the Kanban board
4. See Alpha pick up the task card
5. Watch Alpha walk to his desk
6. See task displayed on Alpha's monitor
7. Trigger task completion
8. Watch Alpha walk back to board
9. See task move to "Done" column
10. Watch Alpha walk to Telegram portal
11. See message animation (whoosh)
12. Check Telegram group for message
13. Watch Alpha return to cot and sleep

**Expected:** All steps complete smoothly, message received in Telegram

#### UAT-002: Multiple Concurrent Tasks
**Steps:**
1. Assign task to Alpha, Beta, and Gamma simultaneously
2. Observe all three wake up
3. Watch all three walk to board (no collisions)
4. See each claim their own task
5. Watch each work at their desk

**Expected:** No visual overlap, correct task assignment

#### UAT-003: Telegram Topic Routing
**Steps:**
1. Complete a CHN-* task (should go to thread 28)
2. Complete a general task (should go to thread 309)
3. Complete a system task (should go to thread 98)

**Expected:** Messages route to correct topics

#### UAT-004: Office Responsiveness
**Steps:**
1. Resize browser window
2. Check mobile view
3. Test touch interactions

**Expected:** Layout adapts, touch works

---

## 7. Implementation Tasks

### Phase 1: Core Canvas (Week 1)
| Task ID | Task | Assignee | Priority |
|---------|------|----------|----------|
| OFFICE-1 | Create Kanban board component with 4 columns | 🐺 Alpha | High |
| OFFICE-2 | Add task cards with properties (title, icon, priority) | 🐺 Alpha | High |
| OFFICE-3 | Implement drag-drop task movement | 🐺 Alpha | Medium |
| OFFICE-4 | Design Kanban board visual style | 🦄 Zeta | High |
| OFFICE-5 | Create task card visual design | 🦄 Zeta | High |

### Phase 2: Agent Animation (Week 1-2)
| Task ID | Task | Assignee | Priority |
|---------|------|----------|----------|
| OFFICE-6 | Create agent sprite system (32x32 from portraits) | 🦄 Zeta | High |
| OFFICE-7 | Implement walking animation (point-to-point movement) | 🐺 Alpha | High |
| OFFICE-8 | Add sleeping state with 💤 animation | 🐺 Alpha | Medium |
| OFFICE-9 | Implement waking animation | 🐺 Alpha | Medium |
| OFFICE-10 | Create working-at-desk animation | 🐺 Alpha | Medium |

### Phase 3: Workflow Logic (Week 2)
| Task ID | Task | Assignee | Priority |
|---------|------|----------|----------|
| OFFICE-11 | Build state management system | 🐙 Epsilon | High |
| OFFICE-12 | Implement event flow (wake → claim → work → complete) | 🐙 Epsilon | High |
| OFFICE-13 | Connect task assignment to agent wake | 🐙 Epsilon | High |
| OFFICE-14 | State persistence to JSON | 🐙 Epsilon | Medium |

### Phase 4: Telegram Portal (Week 2-3)
| Task ID | Task | Assignee | Priority |
|---------|------|----------|----------|
| OFFICE-15 | Design Telegram portal visual | 🦄 Zeta | High |
| OFFICE-16 | Implement portal UI with topic selector | 🐺 Alpha | High |
| OFFICE-17 | Add message send animation (whoosh up tube) | 🐺 Alpha | Medium |
| OFFICE-18 | Integrate with OpenClaw message tool | 🐙 Epsilon | High |
| OFFICE-19 | Route messages to correct topic by task type | 🐙 Epsilon | High |

### Phase 5: Integration & Polish (Week 3)
| Task ID | Task | Assignee | Priority |
|---------|------|----------|----------|
| OFFICE-20 | Connect to real OpenClaw sub-agent events | 🐙 Epsilon | High |
| OFFICE-21 | Add sound effects (optional) | 🐺 Alpha | Low |
| OFFICE-22 | Implement pool table idle behavior | 🐺 Alpha | Low |
| OFFICE-23 | Add time-of-day lighting | 🦄 Zeta | Low |
| OFFICE-24 | Create Shabbat mode | 🦄 Zeta | Low |

### Phase 6: Testing (Week 3-4)
| Task ID | Task | Assignee | Priority |
|---------|------|----------|----------|
| OFFICE-25 | Write automated test suite | 🦔 Gamma | High |
| OFFICE-26 | Execute all T-* test cases | 🦔 Gamma | High |
| OFFICE-27 | Write UAT scripts | 🦝 Theta | High |
| OFFICE-28 | Execute all UAT-* test cases | 🦝 Theta | High |
| OFFICE-29 | Bug fixes from testing | 🦊 Beta | High |

### Phase 7: Documentation (Week 4)
| Task ID | Task | Assignee | Priority |
|---------|------|----------|----------|
| OFFICE-30 | Write user guide | 🦉 Delta | Medium |
| OFFICE-31 | Document API/state schema | 🦉 Delta | Medium |
| OFFICE-32 | Update OFFICE.md with final spec | 🦉 Delta | Medium |

---

## 8. Success Metrics

| Metric | Target |
|--------|--------|
| Task visibility | 100% of active tasks visible on board |
| Animation smoothness | 60fps, no jank |
| Telegram delivery | <2s from completion to message |
| Agent accuracy | Correct agent claims correct task 100% |
| Topic routing | 100% correct routing |

---

## 9. Future Enhancements (v2)

- [ ] Real-time WebSocket updates
- [ ] Click on agent to see their current task
- [ ] Task detail modal on card click
- [ ] Agent chat bubbles when sending messages
- [ ] Pool tournament mini-game
- [ ] Confetti animation for milestone completions
- [ ] Agent mood indicators
- [ ] Coffee break automation (agent goes to kitchen periodically)

---

## 10. Appendix

### A. File Structure
```
projects/office-canvas/
├── index.html          # Main canvas
├── css/
│   └── styles.css      # All styles
├── js/
│   ├── state.js        # State management
│   ├── agents.js       # Agent class & animation
│   ├── kanban.js       # Kanban board logic
│   ├── portal.js       # Telegram portal
│   └── main.js         # Initialization
├── assets/
│   ├── sprites/        # 32x32 agent sprites
│   └── sounds/         # Optional SFX
└── office-state.json   # Persisted state
```

### B. References
- SUBAGENTS.md — Agent personalities and portraits
- OFFICE.md — Physical office layout
- Mission Control — https://www.notion.so/2fe419064d3081bc8155ee2719c1d365

---

*Spec complete. Ready for Mission Control task creation.* 🐼
