---
name: onboarding
description: Setup health plus first story for new team members
---

# Onboarding

Take a new machine from zero to first story without forum diving.

## Prerequisites

- Agentia CLI beta installed.
- A Copado playground or trial org plus a CRT project for testers.

## Playbook

1. Run the health check: `agentia doctor`
2. Fix every `BLOCK` line with its printed `Fix` command, starting with
   `agentia setup` for authentication.
3. Fix `WARN` lines next, especially CRT readiness and project config.
4. Confirm `agentia doctor --json` reads `healthy` or `attention` with no
   blocks.
5. List stories with `agentia cicd work list --json`, pick one, and run
   `agentia doctor --story <id>` to confirm flow consistency.
6. Hand the story to the story delivery skill for the first guided run.

## Output parsing

- `status: blocked` means stop. Nothing downstream works until auth lands.
- `status: attention` means usable with the listed warnings in mind.
- `status: healthy` means fully ready.

## Guardrails

Team guardrails apply, especially never storing tokens in files. See
`guardrails.md`.
