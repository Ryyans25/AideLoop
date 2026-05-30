# AideLoop for VS Code + Copilot

Use AideLoop for non-trivial tasks.

Routing rule:

- If you are not already the `aideloop-worker` agent, do not implement a non-trivial task directly.
- First call `agent` with `agentName: "aideloop-worker"` and pass the user's request plus any relevant context.
- If the `agent` tool is unavailable, report that AideLoop evaluation is blocked and ask the user to switch to the `aideloop-worker` agent. Do not make file changes in the default agent.

Core loop:

1. Define done before doing.
2. Let the worker work.
3. The worker calls the evaluator with `agent` to check evidence.
4. Only verified facts become memory.

For full tasks, use the AideLoop worker agent and episode files:

```bash
scripts/aideloop episode new --level full "user request"
```

The worker must then run the automated AideLoop loop:

1. Complete the work and update `worker_completion.yaml`.
2. Call `agent` with `agentName: "aideloop-evaluator"` to verify `criteria.yaml`, `worker_completion.yaml`, and evidence.
3. If evaluator returns `fail`, repair the failed criteria and call evaluator again.
4. If evaluator returns `pass` and memory candidates exist, call `agent` with `agentName: "aideloop-memory-maintainer"`.
5. If evaluator returns `pass` and there are no memory candidates, finish.

Do not rely on handoff buttons for evaluation; evaluator review is mandatory before completion.
Do not ask whether to run evaluation after making changes; evaluation is part of the task.

Keep `.aideloop/memory/`, `.aideloop/episodes/`, and `.aideloop/state/` private and uncommitted.
