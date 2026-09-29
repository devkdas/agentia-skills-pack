---
name: router
description: Route each request to the right specialist agent
---

# Agent Router

Send every request to the specialist that owns its lifecycle stage. Wrong
agent means wrong vocabulary and wasted turns.

## Prerequisites

- AI credentials stored. Verify with `agentia auth get --json`.

## Routing table

| Developer says | Route to |
|---|---|
| Write or refine a story, plan a feature, check conflicts, sprint planning | `plan` |
| Write code, generate Apex, review a class, fix a bug, analyze metadata | `build` |
| Write a test, generate a test script, review test approach | `test` |
| Deploy this, promote to UAT, why did it fail, release notes, blockers | `release` |
| Write docs, training material, change notes, troubleshooting guides | `operate` |
| Ship a story end to end, full delivery | story delivery skill |
| Something broke in a pipeline or test run | test triage skill |
| Is everything ready, status check | `agentia doctor` |

## Usage

`agentia ai agent ask --agent <name> "<prompt>" --json`

Add `--json` when the answer feeds another agent through the handoff
skill. Keep prompts scoped to one story ID so agents share context.

## Triage shortcut

- Deployment or promotion failure goes to `release` first, then the fix
  goes to `build` through the handoff skill.
- Test failure goes to `test` first with the execution ID attached.
- Anything unclear goes to `operate` for a troubleshooting guide, then to
  the human.

## Guardrails

Team guardrails apply, especially never deploying on a failing signal. See
`guardrails.md`.
