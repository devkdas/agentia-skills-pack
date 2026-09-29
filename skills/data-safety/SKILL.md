---
name: data-safety
description: Snapshot, diff and restore discipline for data deployments
---

# Data Safety

Make every data deployment previewable and recoverable.

## Prerequisites

- Data Vault installed.
- Templates follow `templates/data-template-standards.md`.
- A credential ID for record search and a story ID for ownership.

## Playbook

1. Snapshot before promotion:
   `agentia vault snapshot --template <name> --credential-id <id> --story <story-id>`
2. Diff the new snapshot against the previous one:
   `agentia vault diff --from <old> --to <new> --json`
3. Attach the added, removed and changed counts to the story. Stop and ask
   the human if anything unexpected appears.
4. Promote only after the preview is approved.
5. If records corrupt, issue a restore code:
   `agentia vault restore --snapshot <file> --story <story-id>`
   then approve and confirm explicitly before sending:
   `agentia vault restore --snapshot <file> --story <story-id> --approve-code <code> --yes`
6. Without `--yes` the command only previews the commit body and changes
   nothing.

## Output parsing

- `status: captured` with a file path means the safety net exists.
- `identical: false` in a diff means a human must review before promoting.
- `status: approval-required` means stop until the ceremony completes.

## Guardrails

Team guardrails apply, especially explicit confirmation for destructive
restores. See `guardrails.md`.
