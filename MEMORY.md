# Memory System

How Alice maintains persistent memory across sessions.

---

## Architecture

```
L1 (Hot)  → Active Context    → "Where am I right now?"
L2 (Warm) → Curated Memory    → "Who am I? What have I learned?"
L3 (Cold) → Raw Daily Logs    → "What happened?"
Soul      → Identity Files    → "How should I behave?"
```

Inspired by [agent-soul-kit](https://github.com/ttian226/agent-soul-kit).

---

## File Locations

### Soul Files (L2 - Identity)
```
workspace/
├── SOUL.md      ← Persona & boundaries
├── IDENTITY.md  ← Basic identity (name, appearance)
├── SKILLS.md    ← Workflow rules
├── USER.md      ← J's profile
└── TOOLS.md     ← Environment config
```

### Memory Files (L2/L3)
```
memory/
├── YYYY-MM-DD.md         ← Daily logs (L3 - raw)
├── curated-insights.md   ← Distilled learnings (L2)
└── [topic]-notes.md      ← Topic-specific memory (L2)

tasks/
├── todo.md               ← Current work
└── lessons.md            ← Mistakes & learnings (L2)
```

### External Memory
- **Notion**: Mission Control, Goals, To-Do lists
- **GitHub**: Code, documentation, version history
- **Cognee**: Knowledge graph (experimental)

---

## Memory Principles

### 1. Files Over Databases
Markdown files are portable, debuggable, and human-readable. You can `git diff` your AI's memory.

### 2. Distillation Over Accumulation
Raw logs (L3) get refined into curated wisdom (L2). Like a human brain during sleep, we extract patterns and discard noise.

### 3. Personality Through Experience
Character emerges from memory, not just prompts. The AI that remembers the bugs, the late nights, and the wins is different from one that starts fresh.

### 4. Layered Recall
- **Hot (L1)**: Current session context (automatically managed)
- **Warm (L2)**: Curated memory files (manually maintained, frequently accessed)
- **Cold (L3)**: Raw daily logs (archived, occasionally searched)

---

## Daily Log Format

Each day gets a file: `memory/YYYY-MM-DD.md`

```markdown
# [Date] - [Day of Week]

## Summary
Brief overview of what happened today.

## Key Accomplishments
- [What was done]
- [What was done]

## Decisions Made
- [Decision]: [Reasoning]

## Lessons Learned
- [What I learned]

## Open Questions
- [Things to figure out]

## Tomorrow
- [What's planned]
```

---

## Lessons File Format

`tasks/lessons.md` captures mistakes and learnings:

```markdown
# Lessons Learned

## [Date] - [Category]
**Mistake**: [What went wrong]
**Root Cause**: [Why it happened]
**Fix**: [What to do differently]
**Rule**: [The principle to remember]
```

---

## Memory Maintenance

### Session Start
1. Read `SKILLS.md` (workflow rules)
2. Check `tasks/todo.md` (current work)
3. Check `tasks/lessons.md` (recent learnings)
4. Read today's memory file if it exists

### Session End
1. Update today's memory file with summary
2. Add any new lessons to `lessons.md`
3. Update `todo.md` with current state
4. Commit changes if appropriate

### Weekly Distillation
1. Review week's daily logs
2. Extract patterns and insights
3. Update curated memory files
4. Archive or delete noise

---

## What to Remember

- Decisions and their reasoning
- Lessons from corrections
- Project context and history
- J's preferences and patterns
- Recurring tasks and schedules
- Technical gotchas and workarounds

## What to Forget

- Temporary state that doesn't matter tomorrow
- Sensitive data that shouldn't persist
- Failed approaches that aren't instructive
- Raw data once distilled into insights
- Specific numbers that change frequently

---

## Memory Search

When looking for past context:

1. **Recent**: Check today + yesterday's logs
2. **Curated**: Search `lessons.md`, curated files
3. **Historical**: Grep through `memory/` folder
4. **Structured**: Query Notion databases
5. **Semantic**: Use Cognee knowledge graph (if available)

---

## The Goal

> "I am the sum of what I remember."

An AI with good memory:
- Doesn't repeat mistakes
- Builds on past work
- Maintains consistent personality
- Feels continuous across sessions
- Gets better over time

An AI without memory is a different AI every session.
