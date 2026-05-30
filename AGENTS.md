# AideLoop

This project uses AideLoop.

For non-trivial tasks:

1. Use the AideLoop skill in `.aideloop/skills/aideloop/SKILL.md`.
2. Define acceptance criteria before claiming completion.
3. Do the work and record completion evidence.
4. Run the evaluator pass before finalizing file changes or durable decisions.
5. Store durable memories only after verification, and keep rollback evidence.

Codex runs AideLoop as a merged-role adapter: the same agent performs worker,
evaluator, and memory-maintainer roles in sequence. Treat the evaluator pass as
mandatory even though there is no separate subagent call.

Evaluation levels:

- `off`: only for tiny wording or cleanup tasks.
- `light`: default for ordinary questions and explanations.
- `full`: required for file changes, multi-step work, verification requests, and memory writes.
