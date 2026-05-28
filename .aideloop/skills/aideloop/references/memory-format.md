# Memory Format

Memory uses Markdown files with YAML frontmatter.

Complete transcripts belong in `.aideloop/episodes/`, not in long-term memory articles.

## Directories

```text
.aideloop/memory/
  index.md
  profile.md
  worklog.md
  revisions/
  inbox/
  concepts/
  projects/
  preferences/
  decisions/
```

## Slug Rules

- Use lower-kebab-case.
- Use human-readable slugs for durable memory.
- Use `YYYY-MM-DD-short_hash.md` for inbox entries.
- Add a short hash if there is a collision.
- Avoid renaming slugs once linked.

## Record

```md
---
id: mem_YYYYMMDD_shortid
slug: lightweight-skill-first
type: decision
title: "AideLoop uses Agent Skill as primary form"
confidence: high
source_episodes:
  - al_YYYYMMDD_001
verified: true
created: YYYY-MM-DD
updated: YYYY-MM-DD
links: []
---

## Summary

One sentence summary.

## Facts

- Verified facts.

## Updates

- YYYY-MM-DD: Initial entry.

## Gaps

- Unknowns or future checks.

## Sources

- `.aideloop/episodes/al_YYYYMMDD_001/`
```

## Index

`.aideloop/memory/index.md` is the primary lookup map:

```md
# AideLoop Memory Index

## Decisions

| Slug | Title | Summary | Updated |
| --- | --- | --- | --- |
```
