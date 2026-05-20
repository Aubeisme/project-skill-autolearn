# Project Index Template

Create this file at project root as `SkillsDs.md` when missing.

```markdown
# SkillsDs.md

Project-local skill index. These skills are intentionally scoped to this repository.

## Load policy

- Do not bulk-load every project skill at startup.
- When blocked and no directly applicable method is obvious, scan this file once.
- If a row matches the current problem, read only the referenced `SKILL.md` and apply it.
- If no row matches, skip the project-local skill library.

## Index

| Skill | Use when | Signals | File |
| --- | --- | --- | --- |

## Maintenance rules

- Treat `Signals` as concrete matching clues: error text, command failure mode, path pattern, task symptom, or user-request keyword.
- Add or update index rows only after the skill passes the verification gate.
- Prefer updating an existing skill over creating overlapping skills.
- Never record secrets, private logs, one-off task details, or generic advice.
```
