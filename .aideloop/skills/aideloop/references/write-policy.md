# Write Policy

Memory writes should be useful, quiet, and reversible.

## Rules

- Write memory only after successful evaluation.
- Do not ask for confirmation by default.
- Keep a revision patch for every memory change.
- Never store secrets, tokens, private keys, or failed attempts as success facts.
- Put uncertain memories in `inbox/`.

## Write Classes

| Class | Use for | Destination |
| --- | --- | --- |
| `auto` | Verified project facts, non-sensitive preferences, worklog entries | Typed memory file |
| `inbox` | Low confidence, incomplete source, needs future confirmation | `.aideloop/memory/inbox/` |
| `never` | Secrets, one-off temporary facts, failed attempts | Do not write |

## Revision Patch

Every memory write records a patch:

```text
.aideloop/memory/revisions/YYYY-MM-DD-{episode_id}.patch
```

The patch should be enough to manually undo the memory write.

## Single Writer Rule

Only the main workflow writes to `.aideloop/memory/`.

`memory-maintainer` may propose changes, but the main workflow applies them and records rollback evidence.
