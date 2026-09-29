---
name: test-triage
description: Test failure triage with AI agents plus headless reruns
---

# Test Triage

Turn red builds into diagnosed, rerunnable work without guessing.

## Prerequisites

- CRT `ready:true` from `agentia auth get --crt --json`.
- Auto Poll installed for headless runs.
- A real job ID from `agentia testing job list -p <project-id> --json`.

## Playbook

1. Run headlessly so evidence is captured:
   `agentia test auto --job <id> --project <pid> --output-dir ./test-results --json`
2. If the terminal status is not succeeded, fetch the saved log and full
   result JSON from the output directory.
3. Ask the test agent to explain the failure:
   `agentia ai agent ask --agent test "Why did build <exec-id> fail: <one line summary>"`
4. Ask the release agent whether the story is still shippable:
   `agentia ai agent ask --agent release "Is <story-id> safe to promote after build <exec-id> failed"`
5. Present the root cause plus the suggested fix to the human. Never deploy
   with failing tests and never auto retry without approval.

## Output parsing

- `terminal: true` with `logsSaved` and `resultSaved` means evidence exists.
- `status: timeout` means the job outlived the polling window, not that it
  failed. Extend `--timeout-sec` and rerun.

## Guardrails

Team guardrails apply, especially surfacing failures and confirming before
any rerun. See `guardrails.md`.
