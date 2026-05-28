# Retrieval

AideLoop memory is useful only when the task receives the right context.

## Context Pack

For every non-`off` task:

1. Read `AGENTS.md`.
2. Read `.aideloop/memory/profile.md` if it exists.
3. Read `.aideloop/memory/index.md` if it exists.
4. Read the current project memory from `.aideloop/memory/projects/` if it exists.
5. Select 3-7 relevant memory files.
6. Prefer decisions, preferences, and current-project memory.
7. If no memory is relevant, record `memory_context: none`.

## Selection Heuristics

Prefer memory files whose slug, title, tags, or summary match:

- The user's task.
- Files being edited.
- Project name.
- Tools or libraries mentioned.
- Existing decisions or preferences.

Avoid loading memory just because it is recent.

## Context Pack Shape

```yaml
memory_context:
  profile: .aideloop/memory/profile.md
  project: .aideloop/memory/projects/aideloop.md
  selected:
    - .aideloop/memory/decisions/lightweight-skill-first.md
  excluded:
    - path: .aideloop/memory/concepts/vector-search.md
      reason: "Not relevant to this task."
```
