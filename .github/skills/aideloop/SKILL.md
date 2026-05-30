# AideLoop

Use this skill when a task needs reliable completion, automated evaluator review, or durable memory.

This Copilot skill is a thin adapter over the canonical AideLoop workflow in `.aideloop/skills/aideloop/SKILL.md`.

## VS Code + Copilot Flow

If the active agent is not `aideloop-worker`, it must not perform non-trivial work directly.
It should call `agent` with `agentName: "aideloop-worker"` and pass the user's request.
If the `agent` tool is unavailable, report an AideLoop routing blocker instead of changing files.

For non-trivial tasks:

1. Create or use an episode with `scripts/aideloop episode new --level full "user request"`.
2. Define criteria in `criteria.yaml` before claiming completion.
3. Do the work and update `worker_completion.yaml` with changed files, commands, evidence, and risks.
4. Call `agent` with `agentName: "aideloop-evaluator"` and pass the current episode for evidence review.
5. If evaluation fails, repair the failed criteria and call evaluator again.
6. If evaluation passes and memory candidates exist, call `agent` with `agentName: "aideloop-memory-maintainer"`.
7. If evaluation passes and there are no memory candidates, finish.

The task is incomplete until evaluator returns `pass`.

## Evaluation Levels

- `off`: tiny wording or cleanup tasks.
- `light`: ordinary questions and explanations.
- `full`: file changes, multi-step work, verification requests, and memory writes.

## References

- Canonical skill: `.aideloop/skills/aideloop/SKILL.md`
- Criteria: `.aideloop/skills/aideloop/references/criteria.md`
- Evaluator: `.aideloop/skills/aideloop/references/evaluator.md`
- Memory format: `.aideloop/skills/aideloop/references/memory-format.md`
- Write policy: `.aideloop/skills/aideloop/references/write-policy.md`
