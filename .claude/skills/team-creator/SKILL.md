---
name: team-creator
description: >
  Create a collaborative agent team with roles, personalities, and skills.
  Use when: user says "create team", "build a team", "新建团队",
  "创建团队", "组建团队", "搭建团队".
  Do NOT use for managing existing teams or assigning tasks to teams.
user-invocable: true
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - AskUserQuestion
  - WebSearch
argument-hint: "[team-name]"
---

# Team Creator

Interactive workflow for building a collaborative agent team.

A Team is an installable package — it bundles multiple OpenClaw Agents,
each with its own identity (IDENTITY.md), personality (SOUL.md), and skill
dependencies (skills.json), all self-contained and portable.

See `references/formats.md` for all file format specifications.

## Folder Structure

```
teams/{team-name}/
├── TEAM.md
└── agents/
    ├── manager/
    │   ├── IDENTITY.md
    │   ├── SOUL.md
    │   └── skills.json
    ├── {agent-slug}/
    │   ├── IDENTITY.md
    │   ├── SOUL.md
    │   └── skills.json
    └── ...
```

## Workflow

- [ ] Step 0: Parse arguments
- [ ] Step 1: Team positioning (TEAM.md)
- [ ] Step 2: Define agents (manager auto-created + user-defined workers)
- [ ] Step 3: Define each agent's soul
- [ ] Step 4: Assign skills (per-agent skills.json)
- [ ] Step 5: Generate and save
- [ ] Step 6: Summary

### Step 0: Parse Arguments

- [ ] If `$ARGUMENTS` contains a team name, use it; otherwise ask
- [ ] Slugify: lowercase, hyphens, no spaces (e.g., "Research Team" → `research-team`)
- [ ] Check `teams/{team-name}/` does not exist
- [ ] If it exists, ask: overwrite or pick a new name?

### Step 1: Team Positioning (TEAM.md)

Ask the user:

> What kind of team do you want to create? Describe its purpose and mission.

- [ ] Draft TEAM.md with frontmatter (name, description, version) and body
- [ ] Body: team mission, positioning, collaboration model
- [ ] The `manager` agent is always first in the agents list with `role: coordinator`
- [ ] Show draft for confirmation

### Step 2: Define Agents

The `manager` agent is auto-created. Ask the user for worker agents:

> What roles does this team need? (e.g., frontend developer, tester, PM)

For each role:

- [ ] Collect: display name + brief description
- [ ] Derive slug (e.g., "Frontend Developer" → `frontend-dev`)
- [ ] Confirm the complete agent list (manager + workers)

### Step 3: Define Each Agent's Soul (SOUL.md)

For each agent (including manager):

- [ ] Manager soul: orchestration style, delegation principles, how it routes work
- [ ] Worker souls: personality, working style, principles for each role
- [ ] If user says "auto", generate sensible defaults based on role
- [ ] Show drafts and let user adjust

### Step 4: Assign Skills (per-agent skills.json)

For each agent, build its own skills.json:

- [ ] Recommend skills based on role heuristics
- [ ] Let user customize: add/remove per agent
- [ ] Manager typically has empty skills
- [ ] For each skill assigned to an agent, determine its install source:
  1. Check `~/.agents/.skill-lock.json` — if skill exists there, copy source info
  2. If not found locally, search for it (GitHub, Cloud Hub) or ask user
- [ ] Write skills.json into each agent's folder

### Step 5: Generate and Save

- [ ] Create `teams/{team-name}/`
- [ ] Create `agents/{slug}/` for each agent (manager + workers)
- [ ] Write `TEAM.md`
- [ ] For each agent write `IDENTITY.md` + `SOUL.md` + `skills.json`
- [ ] Verify with `find` tree listing

### Step 6: Summary

```
Team created successfully!
━━━━━━━━━━━━━━━━━━━━━━━━━

📁 teams/{team-name}/
├── TEAM.md — {description}
└── agents/
    ├── manager/
    │   ├── IDENTITY.md — Coordinator
    │   ├── SOUL.md
    │   └── skills.json — 0 skills
    ├── {agent-1}/
    │   ├── IDENTITY.md — {role}
    │   ├── SOUL.md
    │   └── skills.json — {N} skills
    └── ...

Total: {N} agents (1 manager + {N-1} workers)

Per-agent skills:
  • manager: (coordinator — no skills)
  • {agent-1}: {skill-1}, {skill-2}, ...
  • {agent-2}: {skill-1}, {skill-3}, ...

Merged skill manifest ({N} unique):
  • {skill-1} — {sourceType}: {source}
  • {skill-2} — {sourceType}: {source}
  ...
```

## Rules

- Every team MUST have a `manager` agent — it is the coordinator entry point
- All generated content in the language the user uses
- Each agent folder is self-contained: IDENTITY.md + SOUL.md + skills.json
- skills.json MUST include source info for every skill — no orphan references
- Do not invent skills — verify existence via lock files or web search
- Agent slugs must be unique within a team
- SOUL.md should feel human — avoid generic corporate language
- The team folder must be self-contained and portable
