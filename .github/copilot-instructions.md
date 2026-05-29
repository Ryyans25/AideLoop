# AideLoop for VS Code + Copilot

Use AideLoop for non-trivial tasks.

Core loop:

1. Define done before doing.
2. Let the worker work.
3. Hand off to the evaluator to check evidence.
4. Only verified facts become memory.

For full tasks, use the AideLoop worker agent and episode files:

```bash
scripts/aideloop episode new --level full "user request"
```

Then hand off to:

- `aideloop-evaluator` to verify `criteria.yaml`, `worker_completion.yaml`, and evidence.
- `aideloop-memory-maintainer` only after evaluator passes.

Keep `.aideloop/memory/`, `.aideloop/episodes/`, and `.aideloop/state/` private and uncommitted.
