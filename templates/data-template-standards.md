# Data Template Standards

Apply these rules before any data deployment so snapshots stay meaningful
and restores stay possible.

1. One template per main object and purpose. Name it `<Object> <Purpose>`,
   for example `Account Seed`.
2. Select only the columns the deployment needs. Extra columns slow down
   snapshots and widen blast radius.
3. Record the source credential ID and target environments in the template
   description so agents can resolve them without guessing.
4. Snapshot with Data Vault before every promotion. No snapshot, no deploy.
5. Diff the snapshot against live state and attach the summary to the story.
6. Convert legacy templates to v2 detail before snapshotting, since the CLI
   cannot read legacy detail.
7. Verify applied sync entries match the deployed metadata commit by hand,
   since the CLI does not verify this for you.
