---
name: project-skill-autolearn
description: Use when invoked directly or when completing a non-trivial task in any repository to bootstrap project skill storage and preserve verified reusable project-specific strategies, commands, conventions, debugging paths, validation steps, or scriptable workflows as local project skills.
---

# Project Skill Autolearn

## Core principle

This global skill is a pressure valve for `CLAUDE.md`: keep always-on rules in `CLAUDE.md`, and preserve conditional project workflows as on-demand local skills.

When invoked directly, activate this skill for the rest of the current conversation. Before each later final response for non-trivial work, run the review below.

Default project output:

```text
<project>/
  .claude/skills/<project-skill-name>/SKILL.md
  SkillsDs.md
```

For scripted skills, add `.claude/skills/<project-skill-name>/scripts/`.

## Direct invocation bootstrap

When invoked directly by name or slash command:

1. If `SkillsDs.md` is missing, create it from `references/project-index-template.md`.
2. If `.claude/skills/` is missing, create the directory.
3. Do not create a project skill file unless a candidate later passes the gate.
4. Capture candidates from the current session and run the closed-loop review.

## Closed-loop review

1. **Candidate capture**: list only corrected assumptions, repeated pitfalls, debugging paths, validation steps, generated-file rules, architecture boundaries, local conventions, and repeatable manual procedures discovered in the completed task.
2. **Gate**: keep a candidate only if it passes every hard filter and matches at least one signal below.
3. **Route**: classify each survivor as `skip`, `merge`, `new-skill`, `scripted-skill`, or `instruction-rule`.
4. **Merge/New**: update an existing project skill when triggers overlap; otherwise create `.claude/skills/<hyphen-name>/SKILL.md`.
5. **Script decision**: if the workflow is stable, repeated, mechanical, and easy to run incorrectly by hand, read `references/scripted-skills.md` and create a scripted skill.
6. **Verify**: require evidence before indexing: command output, source/config file, reproduced fix, dry run, or successful validation.
7. **Index**: update `SkillsDs.md` only after the skill is valid, focused, verified, and useful.
8. **Future load**: keep default loading off; when blocked, scan `SkillsDs.md` once and load only the matching project skill.

## Gate

Hard filters:

- Project-local, not global advice.
- Verified by command result, source file, config, test, user correction, or repeated observation.
- Reusable beyond the current task.
- Specific about command, path, failure mode, convention, or decision point.
- Actionable for a future agent.
- Safe to record: no secrets, private logs, customer data, sensitive incidents, or machine-local absolute paths.
- Non-duplicative with `CLAUDE.md`, `SkillsDs.md`, and existing project skills.
- Portable enough for the project's OS and runtimes.

Signals:

- Repeated failure or repeated wrong assumption.
- Corrected assumption likely to recur.
- Non-obvious command, setup step, validation rule, or generated-file source of truth.
- Hidden local workflow, path convention, architecture boundary, debugging path, or decision procedure.
- Stable manual procedure that can become a small executable helper.

Always skip one-off task details, raw logs, stack traces, generic advice, unverified guesses, temporary workaround notes, and current-task-only fixes.

## Routing

| Outcome | Action |
| --- | --- |
| `skip` | Do not record it. |
| `merge` | Make the smallest useful edit to an existing project skill and refresh its index row if needed. |
| `new-skill` | Create a focused project skill using `references/project-skill-template.md`, then index it after verification. |
| `scripted-skill` | Read `references/scripted-skills.md`; create a project skill with a `scripts/` resource and verification command. |
| `instruction-rule` | Add one compact rule to project `CLAUDE.md` or `AGENTS.md`; keep detailed strategy in a project skill. |

## Project index

`SkillsDs.md` is the lightweight index. Treat `Signals` as concrete matching clues: error text, command failure mode, path pattern, task symptom, or user-request keyword.

Add or update index rows only after the skill passes the gate. Prefer updating existing skills over creating overlapping skills.

## Final response note

Before answering the user, state one concise outcome:

- `Project skills updated: ...`
- `Project skills not updated: no durable reusable strategy was found.`

Do not include a long retrospective unless asked.
