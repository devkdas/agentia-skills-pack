---
name: story-delivery
description: Full commit to deploy runbook for one user story
---

# Story Delivery

Deliver one story from code to production with a checkpoint at every stage.

## Prerequisites

- Story created from `templates/story-template.md` with an ID from
  `agentia cicd work create` or the existing backlog.
- Gov Guard, Auto Poll and Data Vault installed.

## Playbook

1. Set context and confirm the flow for this story. Local and cloud flows
   cannot be mixed, so pick one and keep it.
2. Ask the build agent for implementation guidance:
   `agentia ai agent ask --agent build "How should I implement <story-id>"`
3. Wait for the human to implement. Then run the gov check for UAT:
   `agentia gov check --story <id> --env UAT-SFP --json`
4. Promote through the normal workflow only after the gate passes.
5. Run the test job headlessly:
   `agentia test auto --job <id> --project <pid> --json`
6. Stop and ask the human before production. On explicit approval, run the
   PROD gov check, approve the code, and recheck with the code.
7. Generate release notes from `templates/release-notes-template.md` with
   the release agent.

## Output parsing

Stop the line at the first `blocked` status anywhere and surface it. Each
stage needs its own human checkpoint before the next begins.

## Guardrails

Team guardrails apply in full. See `guardrails.md`.
