# Agentia Skills Pack for Guardrailed Team Delivery

Portable Agent Skills plus reusable team templates for the Agentia CLI,
built for the Agentia Headless Virtual Hackathon.

Plugins add commands. This pack adds the shared ways of working: eight skills
covering governed releases, test triage, full story delivery, onboarding,
data safety, multi agent handoffs, sprint cycles and agent routing, plus a team guardrails file and ready to copy templates.

## Contents

```text
skills-pack/
├── skills/
│   ├── gov-release/SKILL.md      Pre-promotion gates with Gov Guard
│   ├── test-triage/SKILL.md      Test failure triage with AI agents
│   ├── story-delivery/SKILL.md   Full commit to deploy runbook
│   ├── onboarding/SKILL.md       Setup health plus first story
│   ├── data-safety/SKILL.md      Snapshot, diff and restore with Data Vault
│   ├── handoff/SKILL.md          Chain agents via JSON context passing
│   ├── sprint/SKILL.md           Full plan to docs sprint cycle
│   └── router/SKILL.md           Route each request to the right agent
├── templates/
│   ├── story-template.md
│   ├── data-template-standards.md
│   ├── pre-promote-checklist.json
│   └── release-notes-template.md
├── guardrails.md
└── README.md
```

## Install

Copy any skill folder into your project's skills directory, keeping the
`SKILL.md` filename. For the portable layout used by `agentia setup`:

```sh
cp -r skills/gov-release /path/to/project/.agents/skills/
cp guardrails.md /path/to/project/.agents/skills/agentia-team-guardrails.md
cp templates/story-template.md /path/to/project/docs/
```

Then point your coding agent at the skills directory before it runs any
`agentia` command. Refresh these files after every CLI upgrade, since Agent
Skills are versioned with the CLI.

Companion plugins used by these playbooks: Gov Guard (`agentia gov`),
Doctor DX (`agentia doctor`), Auto Poll (`agentia test auto`) and Data Vault
(`agentia vault`). Install each with `agentia plugins install` from its
public repo, or link locally with `agentia plugins link .` after
`npm run build`.

## License

MIT
