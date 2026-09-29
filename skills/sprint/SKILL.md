---
name: sprint
description: Full AI assisted sprint cycle from refinement to docs
---

# Sprint Cycle

Run one story through every agent in order: plan, build, test, release,
operate. Use it when starting a fresh sprint task.

## Prerequisites

- Story ID from `agentia cicd work list --json`.
- Gov Guard, Auto Poll and Data Vault installed.
- CRT `ready:true` before the test stage.

## Playbook

1. Ask the plan agent to refine:
   `agentia ai agent ask --agent plan "Refine <story-id> and check for metadata conflicts"`
2. Present the refined story to the human.
3. Ask the build agent how to implement:
   `agentia ai agent ask --agent build "How should I implement <story-id>"`
4. Wait for the human to write the code.
5. Ask the build agent to review the diff:
   `agentia ai agent ask --agent build "Review these changes for <story-id>: <summary>"`
6. Commit through the normal workflow, then gate UAT:
   `agentia gov check --story <id> --env UAT-SFP --json`
7. Ask the test agent for coverage:
   `agentia ai agent ask --agent test "Generate tests for the changes in <story-id>"`
8. Promote to UAT, then run the suite headlessly:
   `agentia test auto --job <id> --project <pid> --json`
9. Ask the release agent whether production is safe:
   `agentia ai agent ask --agent release "Is <story-id> ready for PROD, and what blocks it"`
10. Stop and ask the human for deploy approval. Then run the PROD gov
    check, approve the code, and recheck with the code.
11. Deploy, then generate release notes:
    `agentia ai agent ask --agent release "Generate release notes for <story-id>"`
12. Close with operate docs:
    `agentia ai agent ask --agent operate "Create training and change notes for this release"`

## Output parsing

- A `blocked` gate or failed test ends the run at that stage. Surface it
  and wait for the human.
- Production needs both the release agent's blessing and the human's code.

## Guardrails

Team guardrails apply in full. See `guardrails.md`.
