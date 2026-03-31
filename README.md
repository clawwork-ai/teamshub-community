# ClawWork Teams

Community-contributed Teams for [ClawWork](https://github.com/clawwork-ai/clawwork).

## What is a Team?

A Team is a productized packaging of ClawWork's multi-agent runtime — ClawWork provides the execution engine, Teams provide the pre-defined configuration. Each team is a group of AI agents with predefined roles, personalities, skills, and tools. Install a team, assign models, start working.

```
skill → agent → team
```

Every team includes a **Manager** agent that coordinates task delegation and delivery.

## Team Structure

```
<team-name>/
├── TEAM.md
└── agents/
    ├── manager/
    │   ├── AGENT.md
    │   └── SOUL.md
    ├── <role>/
    │   ├── AGENT.md
    │   └── SOUL.md
    └── ...
```

- **TEAM.md** — team metadata and workflow definition
- **AGENT.md** — agent role, skills, and tools
- **SOUL.md** — agent personality and communication style

## Available Teams

| Team | Description | Agents | Author |
|------|-------------|--------|--------|

## Contributing

1. Fork this repo
2. Create your team directory under `teams/`
3. Must include a `manager` agent and at least one specialist agent
4. Submit a PR

## License

Apache-2.0
