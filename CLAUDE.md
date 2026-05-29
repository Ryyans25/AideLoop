# AideLoop

This project uses AideLoop.

AideLoop is a small, file-based loop for reliable agent work:

1. Define done before doing.
2. Let the worker work.
3. Make the evaluator check evidence.
4. Only verified facts become memory.

For non-trivial tasks, use the project subagents in `.claude/agents/`:

- `aideloop-worker`: implements scoped work and records completion evidence.
- `aideloop-evaluator`: verifies criteria against evidence before success is claimed.
- `aideloop-memory-maintainer`: writes durable memory only after evaluation passes.

Shared protocol files live under `.aideloop/`. Keep `.aideloop/memory/`,
`.aideloop/episodes/`, and `.aideloop/state/` private and uncommitted.

Evaluation levels:

- `off`: only for tiny wording or cleanup tasks.
- `light`: default for ordinary questions and explanations.
- `full`: required for file changes, multi-step work, verification requests, and memory writes.
