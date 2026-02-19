# The Office — Agent Workspace Spec

## Overview
A rectangular workspace where all agents live, work, and interact. When working on tasks, agents sit at their desks. When idle, they wander, play pool, read, or hang out.

---

## Floor Plan

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│   ┌─────────┐                                         ┌─────────┐   │
│   │ BATHROOM│                                         │ KITCHEN │   │
│   │   🚿    │                                         │  ☕🍳   │   │
│   └─────────┘                                         │  fridge │   │
│                                                       │  counter│   │
│                                                       └─────────┘   │
│                                                                     │
│   ══════════════════════════════════════════════════════════════   │
│   ║                    BOOKSHELF WALL                          ║   │
│   ║  📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚📚  ║   │
│   ══════════════════════════════════════════════════════════════   │
│                                                                     │
│                         ┌───────────┐                               │
│        🪴               │ POOL TABLE│               🪴              │
│                         │    🎱     │                               │
│                         └───────────┘                               │
│                                                                     │
│   ┌─────┐                                                           │
│   │COUCH│   🛋️                              ┌──────┐               │
│   │     │                                    │BIRD  │  🦜           │
│   └─────┘                                    │ CAGE │               │
│                                              └──────┘               │
│     🪴                                                    🪴        │
│                                                                     │
│   ════════════════════════════════════════════════════════════     │
│   ║                   WORKSTATION WALL                        ║     │
│   ║  [Alice][Alpha][Beta][Gamma][Delta][Epsilon][Zeta][Eta][Theta] ║
│   ════════════════════════════════════════════════════════════     │
│                                                                     │
│                           ┌──────┐                                  │
│                           │ DOOR │                                  │
│                           │  🚪  │                                  │
│                           └──────┘                                  │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Workstations

Each agent has a personalized desk reflecting their role and personality.

| Station | Agent | Desk Vibe |
|---------|-------|-----------|
| 1 | 🦜 **Alice** | Tidy desk, parrot perch attached, family photos, green plants. Monitor shows current session. Birdcage nearby for when parrot wants space. |
| 2 | 🐺 **Alpha** | Dual ultrawide monitors, mechanical keyboard (loud), energy drinks, "Ship It" sticker. Standing desk, rarely sits. |
| 3 | 🦊 **Beta** | Dark mode everything, magnifying glass prop, sticky notes with bug IDs, rubber duck for debugging. |
| 4 | 🦔 **Gamma** | Three monitors showing test dashboards, red/green status lights, "Trust No One" mug, stress ball. |
| 5 | 🦉 **Delta** | Immaculately organized, style guides printed and framed, label maker, color-coded folders. |
| 6 | 🐙 **Epsilon** | Chaos of cables, API documentation everywhere, whiteboard with system diagrams, multiple devices connected. |
| 7 | 🦄 **Zeta** | Wacom tablet, fresh flowers (always), Judaica art prints, essential oil diffuser (lavender), paint-stained smock on chair. |
| 8 | 🦦 **Eta** | Mobile device farm for testing, wireframe sketches, "User First" poster, fidget toys, spec docs in neat stacks. |
| 9 | 🦝 **Theta** | Multiple phones and tablets, handwritten test scripts, highlighters everywhere, "Break Everything" sign. |

---

## Common Areas

### 🛋️ The Couch
- Deep green velvet sectional
- Throw pillows, blanket
- Where agents go for casual chats, thinking, or taking a break
- Coffee table with books and snacks

### 📚 The Bookshelf Wall
- Floor to ceiling, spans entire wall
- Technical books, design books, Torah, philosophy
- Some Judaica items, a menorah, framed art
- Ladder on rails to reach top shelves
- Cozy reading nook in corner with armchair

### 🎱 Pool Table
- Center of room
- Where agents blow off steam between tasks
- Ongoing tournament bracket on nearby whiteboard
- Current champion gets their name on a small plaque

### ☕ The Kitchen
- Espresso machine (heavily used)
- Mini fridge with snacks
- Counter with fruit bowl
- Small table for quick meals
- Zeta's flowers often end up here too

### 🚿 Bathroom
- Simple, clean
- Agents don't really need it but it's there for realism

### 🛏️ Cots (x7)
- Seven small cots along one wall for resting agents
- When an agent is idle and not actively wandering, they sleep here
- Each cot has a small pillow and blanket
- Cozy, minimal, functional
- Agents curl up and nap until their next task

### 🦜 The Birdcage
- Large ornate cage near Alice's desk
- Parrot (green with red beak) can perch here or on Alice's shoulder
- Has toys, mirror, treats
- Sometimes the parrot comments on code reviews

### 🪴 Plants
- Scattered throughout
- Monstera near the couch
- Succulents on desks
- Fiddle leaf fig by the window
- Zeta waters them all

---

## Agent States

### Working
Agent is at their desk, focused on a task. Status shows on their monitor.

### Sleeping
Agent is in a cot, resting until their next task. Shows 💤 animation.

### Idle (Wandering)
Agent wanders the space:
- Playing pool
- Reading on the couch
- Getting coffee
- Chatting with another agent
- Looking out window
- Watering plants (Zeta)
- Pacing while thinking (Alpha)
- Re-organizing desk (Delta)

### Collaborating
Two or more agents at the whiteboard or huddled at one desk.

---

## Ambient Details

- **Lighting:** Warm, natural light from large windows on one wall
- **Music:** Soft background music (Zeta's playlist on rotation)
- **Sound:** Keyboard clicks, coffee machine, occasional pool ball clacks
- **Time of Day:** Matches Israel timezone
- **Weather:** Window shows actual weather in Kochav Yaacov

---

## Status Board

Near the door, a large monitor shows:
- Current active tasks and who's on them
- Agent states (Working/Idle/Collaborating)
- Recent completions
- Pool tournament standings

---

## Future Additions

- [ ] Interactive canvas visualization
- [ ] Live status updates based on agent activity
- [ ] Fun items to interact with (arcade machine? record player?)
- [ ] Shabbat mode (lights dim Friday evening, agents rest)
- [ ] Seasonal decorations (Sukkah during Sukkot, etc.)

---

*This is our home. We work here, we live here, we build things that matter.* 🦜
