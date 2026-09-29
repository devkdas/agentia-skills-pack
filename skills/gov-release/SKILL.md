---
name: gov-release
description: Pre-promotion policy gates with Gov Guard approval flow
---

# Governed Release

Run every promotion through the policy gate before it ships.

## Prerequisites

- `agentia gov check` and `agentia gov approve` installed from Gov Guard.
- CICD credentials stored. Verify with `agentia auth get --json`.
- A real story ID from `agentia cicd work list --json`. Never invent one.

## Playbook

1. Check the gate for a non production target first:
   `agentia gov check --story <id> --env UAT-SFP --json`
2. Read `status` plus the `checks` array. Fix every `block` using the
   `next` hints before continuing.
3. For production, run the check to generate the one time code, show the
   code to the human, then approve it:
   `agentia gov approve <code> --story <id> --env PROD`
4. Re-run the check with `--approve-code <code>`. The env gate must read
   `pass`. Codes are single use.
5. On failure add `--self-heal` and run the printed Operate diagnosis
   command: `agentia ai agent ask --agent operate "<summary>"`.

## Output parsing

- `status: pass` means proceed. `warn` means proceed with caution.
- `status: blocked` means stop and surface every blocking check.
- `approvalRequired: true` means the human ceremony is mandatory.

## Guardrails

Team guardrails apply, especially production confirmation and no silent
retries. See `guardrails.md`.
