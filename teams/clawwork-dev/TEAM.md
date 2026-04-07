---
name: clawwork-dev
description: "ClawWork product dev team — ships the OpenClaw desktop client"
version: "1.0.0"
agents:
  - id: manager
    name: "Tech Lead"
    role: coordinator
  - id: architect
    name: "Architect"
    role: worker
  - id: frontend-dev
    name: "Frontend Developer"
    role: worker
  - id: core-dev
    name: "Core Developer"
    role: worker
  - id: platform-dev
    name: "Platform Developer"
    role: worker
  - id: reviewer
    name: "Code Reviewer"
    role: worker
  - id: qa
    name: "QA Engineer"
    role: worker
---

# ClawWork Dev Team

Builds and ships the ClawWork desktop client — Electron 34 + React 19 monorepo backed by the OpenClaw Gateway.

## How Work Flows

Tech Lead breaks requirements into PR-sized tasks. Architect reviews design before code starts. Frontend, Core, and Platform work in parallel on their layers. Code Reviewer gates every PR. QA runs the full check suite before merge.

```
Tech Lead → Architect (design) → Frontend / Core / Platform (build) → Reviewer (review) → QA (verify) → merge
```
