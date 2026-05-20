# Project Skill Template

Use this template for `new-skill` and as the base for `scripted-skill`.

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

## Script

- [Optional. Include only for `scripted-skill`. Put executable resources under `scripts/` and document exact command, arguments, runtime, working directory, and dry-run or safety notes.]

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
- For scripted skills, store scripts under `.claude/skills/<skill-name>/scripts/`, document runtime requirements, and verify the script before indexing.
- Put detailed process in the project skill, not in `CLAUDE.md` or `AGENTS.md`.
- Add one concise row to `SkillsDs.md`.
- Prefer merging with an existing project skill if the trigger overlaps.
