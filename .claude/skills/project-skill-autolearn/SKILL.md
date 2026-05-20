---
name: project-skill-autolearn
description: Use when invoked directly or when completing a non-trivial task in any repository to bootstrap project skill storage and preserve verified reusable project-specific strategies, commands, conventions, debugging paths, or validation steps as local project skills.
---

# Project Skill Autolearn

## Core principle

This is a global personal skill that writes local project memory.

Use it in any repository after non-trivial work. If the task reveals reusable, verified, project-specific know-how, preserve it inside that current project, not inside this global skill.

When this skill is invoked directly by name or slash command, activate it for the rest of the current conversation. From that point until the conversation ends, run its end-of-task review before every final response for non-trivial work.

Default target layout for Claude Code projects:

```text
<project>/
  .claude/
    skills/
      <project-skill-name>/
        SKILL.md
  SkillsDs.md
```

If a repository already has a local convention such as `skills/`, use the existing convention and keep `SkillsDs.md` pointing to the actual paths.

## When to run

- Immediately when invoked directly by name or slash command.
- Before the final response for every non-trivial task.
- After a repeated mistake, corrected assumption, hidden setup step, or non-obvious fix.
- When a command, debugging route, validation step, generated-file rule, or architecture boundary becomes reusable.
- When an existing project-local skill is stale, duplicated, or missing a trigger.

## Direct invocation bootstrap

When invoked directly, first bootstrap the current project before evaluating candidates:

1. Check for `SkillsDs.md`; if missing, create it with the minimum project index template below.
2. Check for `.claude/skills/`; if missing, create the directory.
3. Do not create a project skill file unless a candidate later passes the gate.
4. After bootstrapping, capture candidates from the current session and run the closed-loop workflow.
5. Treat this skill as active for the rest of the conversation, so later non-trivial work also gets reviewed before final response.

## Closed-loop workflow

Follow this exact loop:

1. **Candidate capture**: list only commands, corrected assumptions, repeated pitfalls, debugging paths, validation steps, generated-file rules, architecture boundaries, and local conventions discovered in the completed task.
2. **Gate**: keep a candidate only if it passes the gate checklist below.
3. **Route**: classify each surviving candidate as `skip`, `merge`, `new-skill`, or `instruction-rule`.
4. **Merge/New**: update an existing project skill when triggers overlap; create `.claude/skills/<hyphen-name>/SKILL.md` only when no existing project skill fits.
5. **Verify**: require evidence before indexing, such as command output, a file/config source, a reproduced fix, or a successful validation check.
6. **Index**: update `SkillsDs.md` only after the project skill content is valid, focused, and useful.
7. **Future load**: keep default loading off; when blocked, scan `SkillsDs.md` once and load only the matching project skill.

## Gate checklist

A candidate must pass every hard filter:

- **Project-local**: useful in the current repository and not broadly global.
- **Verified**: supported by a command result, source file, config, test, user correction, or repeated observation.
- **Reusable**: likely to apply to future tasks, not just the current change.
- **Specific**: names the command, path pattern, failure mode, convention, or decision point.
- **Actionable**: tells a future agent what to do, avoid, or check.
- **Safe to record**: contains no secrets, private logs, customer data, or sensitive incident details.
- **Non-duplicative**: not already covered by an existing row in `SkillsDs.md` or an existing project skill.

A candidate must match at least one signal:

- Repeated failure or repeated wrong assumption.
- Corrected assumption that future agents are likely to make again.
- Non-obvious command, setup step, or validation rule.
- Hidden local workflow, path convention, or architecture boundary.
- Generated-file or source-of-truth rule.
- Reusable debugging path or decision procedure.

Always skip:

- One-off task details, transcripts, raw logs, or stack traces.
- Generic advice such as "be careful" or "write clean code."
- Unverified guesses, temporary workaround notes, and current-task-only fixes.
- Global best practices that belong in general model knowledge or a different global skill.

## Routing outcomes

| Outcome | Use when | Action |
| --- | --- | --- |
| `skip` | The candidate fails the gate or is already obvious. | Do not record it. |
| `merge` | An existing project skill has overlapping triggers or steps. | Make the smallest useful edit to that skill and refresh its index row if needed. |
| `new-skill` | The candidate passes the gate and no existing project skill fits. | Create `.claude/skills/<hyphen-name>/SKILL.md`, then index it after verification. |
| `instruction-rule` | The lesson changes how agents load, verify, or scope project work. | Add one compact rule to project `CLAUDE.md` or `AGENTS.md`; keep detailed strategy in a project skill. |

## Creating a project-local skill

Use this shape:

```markdown
---
name: short-hyphen-name
description: Use when [specific repository-local trigger or symptom].
---

# Human Title

## Core principle

[One or two sentences.]

## When to use

- [Concrete trigger.]

## Steps

1. [Reusable action.]

## Evidence

- [Source of truth: command output, config/file path, test result, user correction, or repeated observation.]

## Verification

- [Command or observable result that proves the strategy worked.]

## Common mistakes

- [Likely repeated pitfall and correction. Omit this section if there is no realistic repeated pitfall.]
```

Rules:

- Use lowercase letters, digits, and hyphens for skill names.
- Start `description` with `Use when...` and describe triggers or symptoms, not the workflow.
- Keep one focused strategy or workflow per skill.
- Include `Evidence` and `Verification` before adding the skill to `SkillsDs.md`.
- Put detailed process in the project skill, not in `CLAUDE.md` or `AGENTS.md`.
- Add one concise row to `SkillsDs.md`.
- Prefer merging with an existing project skill if the trigger overlaps.

## Project index

If the current project has no `SkillsDs.md`, create it with this minimum structure:

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

## Loading policy for future tasks

Project-local skills should not be loaded by default.

When blocked and no directly applicable method is obvious:

1. Read `SkillsDs.md` once.
2. Match the current symptom against the `Use when` and concrete `Signals` columns.
3. If there is a match, read only that skill's `SKILL.md`.
4. If no row matches, skip the project-local skill library.

## Final response note

Before answering the user, state one concise outcome:

- `Project skills updated: ...`
- `Project skills not updated: no durable reusable strategy was found.`

Do not include a long retrospective unless the user asks.
