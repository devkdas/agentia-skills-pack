---
name: autonomous-sprint
description: Zero human operation delivery loop with a single PROD gate
---

# Autonomous Sprint

Run a full story from refinement to production docs with the human
acting only as the production gate. Everything else executes
autonomously, and any failure halts the loop and pages the human
instead of improvising around it.

Use this when the team explicitly delegates a well understood story.
Use the guided story delivery skill instead whenever the story is novel,
risky, or touching production data.

## Prerequisites

- Story ID from `agentia cicd work list --json`, already refined and
  estimated. Never start autonomous mode on a vague story.
- Gov Guard, Auto Poll, Data Vault and a green `agentia doctor` run.
- CRT `ready:true` from `agentia auth get --crt --json`.

## Playbook

1. Snapshot data first when the story touches records:
   `agentia vault snapshot --template <name> --credential-id <id> --story <story-id>`
2. Gate UAT without asking:
   `agentia gov check --story <id> --env UAT-SFP --json`
   Halt on anything but pass. Page the human with the blocking checks.
3. Promote through the normal workflow, then run the suite headlessly:
   `agentia test auto --job <id> --project <pid> --json`
   Halt on anything but a succeeded terminal status. Page the human with
   the log file path plus the build ID.
4. Hand build output to test generation through the handoff skill, then
   rerun the suite once. Halt on the second failure and page the human.
5. Ask the release agent for production readiness:
   `agentia ai agent ask --agent release "Is <story-id> safe for PROD, and what blocks it" --json`
6. Stop. Present the evidence bundle: gate JSON, green test summary,
   snapshot ID. Ask verbatim for production approval and wait.
7. Only on explicit yes, run the PROD gov check, approve the code, and
   recheck with the code, then deploy.
8. Generate release notes plus operate docs, then close the story.

## Halt conditions

Halt the loop and page the human when any of these occur. Never retry
autonomously, never skip forward, never downgrade a gate.

- Any gov check reading blocked.
- Any test run ending outside succeeded.
- Any approval code expired, consumed or mismatched.
- Any AI call returning nothing when its output gates the next step.
- Any command failing twice in a row on retryable errors.

## Output parsing

- The loop state is the evidence bundle: gate JSON, test summary,
  snapshot ID, approval code. Carry it forward intact between stages.
- `status: blocked` or a failed terminal state ends autonomous mode
  immediately. The human resumes in guided mode.

## Guardrails

Team guardrails apply in full, plus one autonomous rule: the loop may
spend machine time freely but never spends trust. Every irreversible
action waits for the single human gate. See `guardrails.md`.
