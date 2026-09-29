---
name: narrator
description: Draft story documentation from code diffs for human approval
---

# Story Narrator

Turn code diffs into product readable story documentation without
touching the story until a human approves every word.

## Prerequisites

- A git checkout with staged or committed changes to narrate.
- AI credentials stored. Verify with `agentia auth get --json`.
- A real story ID from `agentia cicd work list --json`. Never invent one.

## Playbook

1. Collect the diff. Staged work is safest:
   `git diff --staged`
   For a whole branch against main:
   `git diff main...HEAD --stat` first, then the full diff only if it is
   small enough to read. Cap what you send near 12KB like any AI prompt.
2. Ask the release agent for a product readable draft:
   `agentia ai agent ask --agent release "Explain these Salesforce changes in plain English for a product manager: <diff>" --json`
3. Present the draft plus the raw diff stat to the human. Nothing is
   written yet.
4. Only on explicit approval, write the narrative to the story. Use the
   long fields since acceptance criteria caps at 255 characters:
   `agentia cicd work update <story-id> --functional-requirements "<approved text>" --json`
5. Confirm with `agentia cicd work get <story-id> --json` that the text
   landed, then stop.

## Output parsing

- The `--json` envelope carries the draft for programmatic handling.
- A missing or expired AI configuration means stop and report, never
  fabricate documentation.
- The story write is the only mutation in this skill and always needs
  the human's explicit yes first.

## Guardrails

Team guardrails apply, especially human approval before any write and
never logging tokens. See `guardrails.md`.
