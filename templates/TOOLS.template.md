# TOOLS.md - Local Notes

<!--
Environment-specific configuration that shouldn't be shared.
Skills define HOW tools work. This file is for YOUR specifics.
-->

## What Goes Here

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- API endpoints (not keys!)
- Anything environment-specific

---

## TTS / Voice

- Voice: [Voice name and description]
- Voice ID: [Provider-specific ID]
- Model: [Model name]

## Smart Home

### [Device Category]
- Script: `scripts/[name].mjs`
- Commands: `[how to run]`
- **Devices:**
  - `[0]` **[Name]** — [location/description]
  - `[1]` **[Name]** — [location/description]

## Weather

- Location: [City, Country]
- Coords: lat [X], lon [Y]
- API: [Provider]

## Notification Routing

### [Platform] Group
- **Group ID**: `[ID]`
- **Group Name**: [Name]

### Topic Thread IDs
| Thread ID | Topic | Route |
|-----------|-------|-------|
| 1 | General | Default |
| [X] | [Topic] | [What goes here] |

### Routing Rules
- **[Task type]** → [Topic]
- **[Task type]** → [Topic]
- **Don't DM user with automated updates** — use group topics

---

## Scripts Reference

| Script | Purpose |
|--------|---------|
| `scripts/[name]` | [What it does] |

---

<!--
SECURITY: Never put API keys or passwords in this file.
Use environment variables for secrets.
-->
