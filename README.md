# AideLoop

A tiny loop for personal coding agents that should remember, verify, and stop pretending "done" is a feeling.

Inspired by Karpathy-style coding-agent discipline and Anthropic-style evaluator harnesses, packaged as a few files you can drop into a project.

## The Four Rules

1. **Define done before doing.**
2. **Let the worker work.**
3. **Make the evaluator check evidence.**
4. **Only verified facts become memory.**

That's it.

No daemon. No database. No dashboard. Just a small file protocol that makes coding agents behave more like dependable assistants.

## Why This Exists

Most agent failures are boring:

- It starts before defining success.
- It checks its own homework.
- It forgets what you already decided.
- It stores noisy context instead of useful memory.

AideLoop keeps the loop small enough to actually use.

## Default Shape

The repository is directly usable as a Claude Code setup:

```text
CLAUDE.md
.claude/
  agents/
    aideloop-worker.md
    aideloop-evaluator.md
    aideloop-memory-maintainer.md
scripts/
  aideloop
  init-claude
  init-codex
  init-copilot
.aideloop/
  skills/aideloop/
  memory/      # ignored by git
  episodes/    # ignored by git
  state/       # ignored by git
```

Claude Code gets the native multi-agent shape: worker, evaluator, and memory maintainer are separate project agents.

## Quick Start

Install AideLoop into another Claude Code project:

```bash
scripts/init-claude /path/to/project
```

Install the Codex adapter:

```bash
scripts/init-codex /path/to/project
```

Install the VS Code Copilot adapter:

```bash
scripts/init-copilot /path/to/project
```

Then open the target project in your agent host and say:

```text
Use AideLoop for this task.
```

## Adapter Model

AideLoop core is file-based and host-agnostic. The control model is always:

```text
worker -> evaluator -> pass/fail -> repair or memory -> done
```

Each adapter chooses how to execute that same loop:

- Claude Code uses `Task` to invoke project agents under `.claude/agents/`.
- VS Code Copilot uses `agent` with `.github/agents/`.
- Codex uses `AGENTS.md` plus the shared AideLoop skill as a merged role-switching entry in one agent.

The shared protocol is always:

```text
scripts/aideloop
.aideloop/
  skills/aideloop/
  memory/      # ignored by git
  episodes/    # ignored by git
  state/       # ignored by git
```

Create a worker/evaluator episode:

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
