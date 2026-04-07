# ClawWork TeamsHub

Community-contributed Teams for [ClawWork](https://github.com/clawwork-ai/ClawWork).

## What is a Team?

A Team is a self-contained multi-agent unit — roles, personalities, skills, tools, and workflow, all packaged together. ClawWork provides the execution engine, Teams provide the pre-defined configuration. Install a team, assign models, start working.

```
skill → agent → team
```

Every team includes a **coordinator** agent that orchestrates task delegation and delivery.

## Registry Format

The `teamshub.json` file at the repository root serves as the registry index. ClawWork clients fetch this file to discover available teams.

```json
{
  "version": 1,
  "name": "ClawWork Community Teams",
  "description": "Community-contributed team templates for ClawWork",
  "teams": [
    {
      "slug": "example-team",
      "name": "Example Team",
      "emoji": "🚀",
      "description": "Short description of what this team does",
      "version": "1.0.0",
      "agentCount": 2,
      "category": "development",
      "tags": ["example"],
      "author": "your-github-handle"
    }
  ]
}
```

## Team Structure

Each team lives in its own directory under `teams/`:

```
teams/<team-slug>/
├── TEAM.md
└── agents/
    ├── <coordinator>/
    │   ├── IDENTITY.md
    │   ├── SOUL.md
    │   └── skills.json
    ├── <worker>/
    │   ├── IDENTITY.md
    │   ├── SOUL.md
    │   └── skills.json
    └── ...
```

- **TEAM.md** — team metadata (YAML frontmatter) and workflow definition
- **IDENTITY.md** — agent role description and prompt
- **SOUL.md** — agent personality and communication style
- **skills.json** — agent skill dependencies from ClawHub:
  ```json
  {
    "version": 1,
    "skills": {
      "web-search": { "source": "web-search", "sourceType": "clawhub" }
    }
  }
  ```

## Contributing

1. Fork this repo
2. Create your team directory under `teams/<your-team-slug>/`
3. Add the corresponding entry to `teamshub.json`
4. Must include a coordinator agent and at least one worker agent
5. Submit a PR

## License

Apache-2.0
