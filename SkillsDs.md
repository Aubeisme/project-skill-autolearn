# SkillsDs.md

Project-local skill index for this distribution repository. The primary global Claude Code skill lives at `.claude/skills/project-skill-autolearn/SKILL.md`; the root `skills/` copy is kept for compatibility.

## Load policy

- Do not bulk-load every project skill at startup.
- When blocked and no directly applicable method is obvious, scan this file once.
- If a row matches the current problem, read only the referenced `SKILL.md` and apply it.
- If no row matches, skip the project-local skill library and continue with normal investigation.
- At the end of a non-trivial task, run the closed-loop review in `.claude/skills/project-skill-autolearn/SKILL.md` before the final response.

## Index

| Skill | Use when | Signals | File |
| --- | --- | --- | --- |
| project-skill-autolearn | Completing a non-trivial task in any repository and preserving verified reusable project-specific strategy in that current project. | repeated fix, corrected assumption, non-obvious command, local workflow, reusable debugging path, end-of-task review | `.claude/skills/project-skill-autolearn/SKILL.md` |

## Maintenance rules

- Add or update an index row whenever a project-local skill is created, renamed, merged, or deleted.
- Treat `Signals` as concrete matching clues: error text, command failure mode, path pattern, task symptom, or user-request keyword.
- Add or update index rows only after the skill passes the verification gate.
- Keep each row short enough to scan quickly; put detailed steps, evidence, and verification inside the skill file.
- Prefer updating an existing skill over creating overlapping skills.
- Never record secrets, private logs, one-off task details, or generic advice.
