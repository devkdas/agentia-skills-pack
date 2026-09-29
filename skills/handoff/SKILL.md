---
name: handoff
description: Chain AI agents by passing JSON context between them
---

# Multi Agent Handoff

Let agents build on each other's output instead of starting cold. The
pattern is always the same: ask one agent with `--json`, extract the
structured answer, and inject it into the next agent's prompt.

## Prerequisites

- AI credentials stored. Verify with `agentia auth get --json`.
- A story ID giving both agents shared scope.

## Playbook

1. Ask the first agent with `--json` for machine readable output:
   `agentia ai agent ask --agent build "What Apex classes do I need for lead scoring in <story-id>" --json`
2. Extract the answer with python3 so no extra tools are needed:
   `agentia ai agent ask --agent build "List only the class names" --json | python3 -c "import json,sys; print(json.load(sys.stdin)['response'])"`
3. Inject that context into the second agent's prompt:
   `agentia ai agent ask --agent test "Generate CRT test scripts for these classes from the build agent: <names>"`
4. Present the second agent's output to the human for review.
5. Stop and ask before any execution. Then trigger with Auto Poll:
   `agentia test auto --job <id> --project <pid> --json`

## Proven handoffs

- Build output into test prompts for targeted test generation.
- Release error analysis into build prompts for guided fixes:
  `agentia ai agent ask --agent release "Analyze this error: <message>"`
  then `agentia ai agent ask --agent build "Fix the issue: <summary>"`
- Release readiness into operate prompts for docs:
  `agentia ai agent ask --agent operate "Write change notes for <story-id>"`

## Output parsing

- The `--json` envelope carries the agent text under `response`. Extract
  it programmatically, never retype it.
- The developer is the approval gate between every handoff. No agent calls
  the next agent directly.

## Guardrails

Team guardrails apply, especially human checkpoints between stages. See
`guardrails.md`.
