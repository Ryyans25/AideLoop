# Episode Template

Use this shape for `.aideloop/episodes/{episode_id}/`.

## request.md

```md
# Request

{user_request}
```

## criteria.yaml

```yaml
episode_id: al_YYYYMMDD_001
level: light|full
criteria:
  - id: C1
    description: ""
    source: user_request
    weight: must
    verification_method: file_inspection|command|reasoning
    evidence_required: ""
```

## worker_completion.yaml

```yaml
episode_id: al_YYYYMMDD_001
summary: ""
artifacts:
  files_changed: []
  commands_run: []
  evidence: []
known_risks: []
```

## evaluator_verdict.yaml

```yaml
episode_id: al_YYYYMMDD_001
verdict: pass|fail
checked: []
failed_criteria: []
repair_instructions: []
memory_candidates: []
```

## final.md

```md
# Final

{final_response}
```
