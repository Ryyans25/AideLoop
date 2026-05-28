# Criteria

Criteria decide what "done" means before completion is claimed.

## Evaluation Level Policy

| Task type | Level | Required evidence |
| --- | --- | --- |
| Tiny wording or cleanup task | `off` | None |
| Ordinary question, explanation, lookup | `light` | Short checklist |
| File changes, docs, code | `full` | File references, diff summary, checks |
| Memory write | `full` | Evaluator verdict and memory patch |
| User asks for review, verification, acceptance | `full` | Criteria and evidence |
| Destructive or risky action | `full` plus user approval when needed | Before/after evidence |

## Good Criteria

Good criteria are:

- Specific.
- Testable.
- Traceable to the user request.
- Small enough to verify independently.

Example:

```yaml
criteria:
  - id: C1
    description: "The AideLoop MVP only targets Codex."
    source: "user_request"
    weight: must
    verification_method: "file_inspection"
    evidence_required: "HLD and AGENTS.md do not require Claude or Copilot files."
```

## Light Checklist

For `light`, use 2-4 checklist items:

```yaml
level: light
checklist:
  - "Answer directly addresses the user's question."
  - "Any uncertainty is called out."
  - "No durable memory is written."
```

## Full Criteria

For `full`, create explicit criteria:

```yaml
level: full
criteria:
  - id: C1
    description: ""
    source: "user_request|repo_context|memory"
    weight: must
    verification_method: "file_inspection|command|reasoning"
    evidence_required: ""
```
