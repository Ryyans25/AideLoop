# AideLoop

Use this skill when a task needs reliable completion, durable memory, or project-aware context.

## Goal

AideLoop keeps personal agent work simple:

1. Load only the memory needed for the current task.
2. Pick an evaluation level.
3. Define criteria before claiming completion.
4. Verify evidence.
5. Write useful memories with rollback evidence.

The worker controls the evaluation loop. If the host has a subagent tool,
the worker invokes the evaluator with that tool. If the host does not expose
subagents, the same agent performs the evaluator pass in-thread using the
same criteria and evidence.

## Evaluation Levels

- `off`: only for tiny wording or cleanup tasks.
- `light`: default for ordinary questions, explanations, and simple lookups.
- `full`: required for file changes, multi-step work, verification requests, and memory writes.

The worker should not self-select a lower level to save time. Apply the policy in `references/criteria.md`.

## Workflow

### 1. Load Context

Build a small context pack using `references/retrieval.md`.

At minimum:

- Read the available host entry file: `CLAUDE.md`, `AGENTS.md`, or `.github/copilot-instructions.md`.
- Read `.aideloop/memory/profile.md` if it exists.
- Read `.aideloop/memory/index.md` if it exists.
- Select only the memory files relevant to the task.

If no memory exists yet, continue normally and record `memory_context: none`.

### 2. Choose Evaluation Level

Use `off` only for tiny tasks.

Use `light` for ordinary questions and explanations.

Use `full` when the task changes files, has multiple steps, writes memory, or the user asks for verification, review, or acceptance.

### 3. Define Criteria

For `light`, write a short checklist.

For `full`, write explicit criteria before finalizing the work. Criteria must be specific, testable, and traceable to the user request.

Use `references/criteria.md`.

When an episode is needed, create one with:

```bash
scripts/aideloop episode new --level full "user request"
```

### 4. Do The Work

Complete the task as directly as possible. Keep edits scoped.

For `full`, produce a completion packet:

```yaml
summary: ""
artifacts:
  files_changed: []
  commands_run: []
  evidence: []
known_risks: []
```

If using an episode, write this packet to `worker_completion.yaml`.

### 5. Evaluate

For `light`, run the checklist yourself and report any uncertainty.

For `full`, run an evaluator pass using `references/evaluator.md`. The evaluator verifies evidence, not the worker's confidence.

- Claude Code: the worker uses `Task` to invoke `aideloop-evaluator`.
- VS Code Copilot: the worker uses `agent` to invoke `aideloop-evaluator`.
- Codex or other single-agent hosts: run the evaluator pass in the current thread.

If evaluation fails, repair the failed criteria before finalizing.

If using an episode, write the evaluator result to `evaluator_verdict.yaml`.

### 6. Write Memory

After successful evaluation, extract durable memory candidates and apply `references/write-policy.md`.

Write only verified, useful memories. Record a revision patch in `.aideloop/memory/revisions/` when memory changes.

Use `references/memory-format.md`.

## Do Not

- Do not run full evaluation for tiny tasks.
- Do not store secrets, tokens, private keys, or failed attempts as durable facts.
- Do not copy full transcripts into memory articles.
- Do not write directly to `.aideloop/memory/` from multiple parallel agents.
- Do not assume all host adapters have identical multi-agent behavior; use the file protocol as the source of truth.
