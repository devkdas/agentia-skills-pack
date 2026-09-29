# Agentia Skills Pack for Guardrailed Team Delivery

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agentia 0.122](https://img.shields.io/badge/agentia-0.122.0--alpha.1-blue.svg)](https://developer.copado.com/docs)
[![Skills 9](https://img.shields.io/badge/skills-9-blue.svg)](#skill-catalog)

**Skills Pack** standardizes how humans and agents deliver together. Eight
portable Agent Skills plus a nine rule guardrails file plus reusable team
templates, all written for real `agentia` commands and four companion
plugins.

Copy a folder, get the standard. Built for the **Agentia Headless Virtual
Hackathon**.

---

## Table of Contents

- [The Problem](#the-problem)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Live Demo Workflow](#live-demo-workflow)
- [Skill Catalog](#skill-catalog)
- [Templates](#templates)
- [Guardrails](#guardrails)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [How It Works](#how-it-works)
- [Security](#security)
- [Contents](#contents)
- [Hackathon Fit](#hackathon-fit)
- [License](#license)

---

## The Problem

Plugins add commands, but teams lack shared ways of working. Every
developer prompts their AI agent differently, repeats the same setup
debugging, and promotes with no standard checklist. The CLI ships managed
skills for broad areas, yet no team level pack encodes governance gates,
test triage, data safety and full story delivery as one consistent
standard. Inconsistent agent usage means inconsistent delivery quality.

## Features

- **Nine skills** — governed releases, test triage, full story delivery,
  onboarding, data safety, multi agent handoffs, sprint cycles, agent
  routing and story narration.
- **Exact command sequences** — every step names the real command with
  flags, never pseudocode.
- **Output parsing rules** — what each status means and what the agent
  does next, per skill.
- **Nine team guardrails** — production safety, data integrity and
  security rules that sit under every skill.
- **Four reusable templates** — story, data standards, pre promote
  checklist JSON and release notes.
- **Host agnostic** — works in Cursor, Claude or any skills compatible
  host that can run the CLI.

## Installation

### Prerequisites

- Agentia CLI beta with an authenticated machine.
- The companion plugins for the skills you use: Gov Guard, Doctor DX,
  Auto Poll, Data Vault.

### Install a skill

Copy any skill folder into the project's skills directory, keeping the
`SKILL.md` filename. For the portable layout created by `agentia setup`:

```sh
cp -r skills/gov-release /path/to/project/.agents/skills/
cp -r skills/test-triage /path/to/project/.agents/skills/
cp guardrails.md /path/to/project/.agents/skills/agentia-team-guardrails.md
cp templates/story-template.md /path/to/project/docs/
```

Then point the coding agent at the skills directory before it runs any
`agentia` command. Refresh these files after every CLI upgrade, since
Agent Skills are versioned with the CLI.

## Quick Start

### 1. Onboard a machine through the skill

Load `skills/onboarding/SKILL.md` and follow it: run `agentia doctor`,
fix every block with its printed command, confirm healthy.

### 2. Deliver one story through the skill

Load `skills/story-delivery/SKILL.md` and follow the checkpoints from
context to production approval to release notes.

### 3. Triage a red build through the skill

Load `skills/test-triage/SKILL.md`: rerun headlessly with Auto Poll,
ask the test agent with the execution ID, present the fix, never deploy
red.

## Live Demo Workflow

The repeatability proof, run twice on camera with identical steps:

```text
1. Load skills/onboarding/SKILL.md -> agentia doctor to green
2. Load skills/story-delivery/SKILL.md -> gov check plus diff as written
3. Reset, repeat both flows -> same steps, same order, same gates
4. Show the guardrails plus templates backing every decision
```

## Skill Catalog

| Skill | Covers | Key commands |
|---|---|---|
| `gov-release` | Pre-promotion gates | `gov check`, `gov approve`, Operate ask |
| `test-triage` | Failure diagnosis | `test auto`, test plus release ask |
| `story-delivery` | Commit to deploy runbook | Full checkpoint chain |
| `onboarding` | Setup health plus first story | `doctor`, `cicd work list` |
| `data-safety` | Snapshot discipline | `vault snapshot`, `diff`, `restore` |
| `handoff` | Chain agents via JSON | `ai agent ask --json` plus extraction |
| `sprint` | Plan to docs 12 step cycle | All five specialist agents |
| `router` | Request to agent mapping | Routing table plus triage shortcuts |
| `narrator` | Story docs from diffs | `git diff`, release ask, `work update` |

## Templates

| Template | Purpose |
|---|---|
| `story-template.md` | Consistent story context for agents and reviewers |
| `data-template-standards.md` | Seven rules for snapshot worthy templates |
| `pre-promote-checklist.json` | Seven machine readable gates with commands |
| `release-notes-template.md` | Release agent generated notes structure |

## Guardrails

Nine non negotiable rules in `guardrails.md`: explicit human production
confirmation, no force flags for production, checkpoints between stages,
no fabricated IDs, no deploys on failing tests, no silent retries, no
token logging, JSON for programmatic parsing, and no secret bearing files
in public repos.

## Configuration

No build step and no dependencies. Skills are markdown, templates are
markdown plus JSON. The pre promote checklist validates as JSON and its
seven gates each carry the exact command plus the expected result.

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| Agent ignores the skill | Skills directory not in context | Point the agent at the skills path first |
| Commands in skill fail | CLI upgraded without skill refresh | Refresh skills after every CLI upgrade |
| Skill references missing plugin | Companion plugin not installed | Install from its public repo, then link |
| Checklist gate fails | Real environment gap | Follow the gate's expected result line |

## How It Works

```text
Agent loads SKILL.md
  -> prerequisites verified with real commands
  -> playbook steps executed in order
  -> outputs parsed by the skill's rules
  -> guardrails veto unsafe actions
  -> human checkpoints gate every stage
```

## Security

Skills never contain tokens. Templates never contain org IDs. The
checklist runs read operations first and gates destructive ones behind
human approval, matching the companion plugins.

## Contents

```text
skills-pack/
├── skills/
│   ├── gov-release/SKILL.md
│   ├── test-triage/SKILL.md
│   ├── story-delivery/SKILL.md
│   ├── onboarding/SKILL.md
│   ├── data-safety/SKILL.md
│   ├── handoff/SKILL.md
│   ├── sprint/SKILL.md
│   ├── router/SKILL.md
│   └── narrator/SKILL.md
├── templates/
│   ├── story-template.md
│   ├── data-template-standards.md
│   ├── pre-promote-checklist.json
│   └── release-notes-template.md
├── guardrails.md
└── README.md
```

## Hackathon Fit

Covers reusable templates and guided workflows head on, simplifies
onboarding, and answers the skills third of the extensibility rubric that
pure plugins cannot reach. Combines all four companion plugins into one
team standard.

## License

MIT License — see [LICENSE](LICENSE) for details.
