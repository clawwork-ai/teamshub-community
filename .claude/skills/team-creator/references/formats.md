# Team File Formats

## TEAM.md

```yaml
---
name: {team-name}
description: "{one-line team purpose}"
version: "1.0.0"
agents:
  - id: manager
    name: "{Manager Display Name}"
    role: coordinator
  - id: {agent-slug}
    name: "{Display Name}"
    role: worker
---

{Markdown body: team mission, positioning, collaboration model between agents}
```

## IDENTITY.md

Each agent maps to an OpenClaw Agent. Defines WHO this agent is — identity
and responsibilities only. No skill references here.

```yaml
---
id: {agent-slug}
agentId: ""
name: "{Display Role Name}"
description: "{What this agent is responsible for}"
---

{Markdown body: role positioning, core responsibilities, how this agent
collaborates with other agents in the team}
```

- `id`: internal role slug within the team, defined at creation time, immutable
- `agentId`: real OpenClaw Agent ID assigned by the system, backfilled at install time, left empty at creation

## SOUL.md

Defines HOW this agent communicates and thinks — its personality.

```markdown
# {Role Name} — Soul

## Personality

{Communication style, tone, attitude.}

## Working Style

{How this agent approaches tasks, priorities, decision-making.}

## Principles

{Core beliefs that guide decisions.}
```

## Per-Agent skills.json

Each agent has its OWN skills.json declaring its skill dependencies with
install sources. Format mirrors `.skill-lock.json` for compatibility.

```json
{
  "version": 1,
  "skills": {
    "{skill-id}": {
      "source": "{owner/repo}",
      "sourceType": "github",
      "skillPath": "skills/{skill-id}/SKILL.md"
    }
  }
}
```

**sourceType values:**
- `"github"` — install from GitHub repo (requires `source` as `owner/repo`)
- `"clawhub"` — install from OpenClaw Cloud Hub (requires `source` as hub skill ID)
- `"local"` — already available locally, no installation needed

## Manager Agent (MANDATORY)

Every team MUST have a `manager` agent with these properties:

- **id**: `manager`
- **role**: `coordinator` in TEAM.md
- **Never does work itself** — only dispatches, coordinates, and synthesizes
- **SOUL.md**: focuses on orchestration style, delegation principles, quality gates
- **skills.json**: typically empty (`"skills": {}`)
- The manager is the entry point when the team is invoked
