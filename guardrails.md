# Team Guardrails for Agentia Delivery

Every agent and human on the team follows these nine rules. They are the
non negotiable layer under all five skills in this pack.

## Production safety

1. Never deploy to PROD or production without explicit human confirmation.
   Ask verbatim for yes or no and wait for the answer.
2. Never use `--yes` or force flags for production deployments. Gates exist
   to be approved, not bypassed.
3. Never chain commit, promote and deploy without a human checkpoint between
   each stage. Present each result and ask whether to proceed.

## Data integrity

4. Never fabricate IDs for stories, pipelines, environments, jobs or suites.
   Always retrieve them first with list commands.
5. Never deploy with failing tests. Surface failures to the human and triage
   before any promotion.
6. Never retry a failed deployment automatically. Investigate the cause with
   the release or operate agent, then ask before retrying.

## Security and parsing

7. Never store or log API tokens in output, files or messages. Secrets live
   in the keychain and explicit env values only.
8. Always use `--json` output when parsing CLI results programmatically.
   Never parse human readable tables.
9. Never commit snapshots, logs, xunit files or reports containing org
   secrets to a public repo. Check `git status` and `git diff` before every
   commit.
