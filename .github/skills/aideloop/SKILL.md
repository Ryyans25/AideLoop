# AideLoop

Use this skill when a task needs reliable completion, evaluator handoff, or durable memory.

This Copilot skill is a thin adapter over the canonical AideLoop workflow in `.aideloop/skills/aideloop/SKILL.md`.

## VS Code + Copilot Flow

For non-trivial tasks:

1. Create or use an episode with `scripts/aideloop episode new --level full "user request"`.
2. Define criteria in `criteria.yaml` before claiming completion.
3. Do the work and update `worker_completion.yaml` with changed files, commands, evidence, and risks.
4. Hand off to `aideloop-evaluator`.
5. If evaluation fails, repair the failed criteria and hand off again.
6. If evaluation passes and memory candidates exist, hand off to `aideloop-memory-maintainer`.

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
