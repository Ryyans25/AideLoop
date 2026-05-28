# AideLoop

A tiny loop for personal coding agents that should remember, verify, and stop pretending "done" is a feeling.

Inspired by Karpathy-style coding-agent discipline and Anthropic-style evaluator harnesses, packaged as a few files you can drop into a Codex project.

## The Four Rules

1. **Define done before doing.**
2. **Let the worker work.**
3. **Make the evaluator check evidence.**
4. **Only verified facts become memory.**

That's it.

No daemon. No database. No dashboard. Just a small loop that makes Codex behave more like a dependable assistant.

## Why This Exists

Most agent failures are boring:

- It starts before defining success.
- It checks its own homework.
- It forgets what you already decided.
- It stores noisy context instead of useful memory.

AideLoop keeps the loop small enough to actually use.

## Quick Start

Initialize AideLoop in this project:

```bash
scripts/init-aideloop
```

Initialize another project:

```bash
scripts/init-aideloop /path/to/project
```

Then open the project in Codex and say:

```text
Use AideLoop for this task.
```

## What It Adds

```text
AGENTS.md
scripts/aideloop
.aideloop/
  skills/aideloop/
  memory/      # ignored by git
  episodes/    # ignored by git
  state/       # ignored by git
```

Create a worker/evaluator handoff episode:

```bash
scripts/aideloop episode new --level full "Implement the task"
```

This creates:

```text
.aideloop/episodes/al_YYYYMMDD_001/
  request.md
  criteria.yaml
  worker_completion.yaml
  evaluator_verdict.yaml
  final.md
  raw_log.md
```

## Evaluation Levels

- `off`: tiny wording or cleanup tasks.
- `light`: ordinary questions and explanations.
- `full`: file changes, multi-step work, verification requests, and memory writes.

## Inspired By

AideLoop is an independent project inspired by public work and ideas from:

- [Andrej Karpathy's observations on LLM coding pitfalls](https://github.com/multica-ai/andrej-karpathy-skills)
- [Anthropic's harness design for long-running agents](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [claude-memory-compiler](https://github.com/coleam00/claude-memory-compiler)
- [gbrain](https://github.com/garrytan/gbrain)

AideLoop is not affiliated with, endorsed by, or sponsored by those people, companies, or projects.
