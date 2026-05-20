# Project Skill Autolearn

[English](README.md) | [Chinese](README.zh-CN.md)

`project-skill-autolearn` is a global Claude Code skill for turning reusable project workflows into local, indexed, on-demand skills.

Use it when you want project-specific debugging paths, validation routines, recovery steps, or small helper scripts to be durable and shareable without loading them on every request.

## Why

Project work often reveals useful procedures that are too specific to become global skills:

- debugging a flaky subsystem
- recovering from a known codegen failure
- validating a risky change type
- checking where generated files really come from
- wrapping a repeated manual check as a script

This skill stores those procedures inside the current repository and indexes them with `SkillsDs.md`. Future agents scan the index only when needed, then load one matching `SKILL.md`.

## What it creates

When invoked directly, it bootstraps the current project:

```text
<project>/
  .claude/
    skills/
  SkillsDs.md
```

Accepted workflows become local project skills:

```text
<project>/
  .claude/
    skills/
      <project-skill-name>/
        SKILL.md
        scripts/        # optional, only for scripted skills
  SkillsDs.md
```

The global skill provides the learning process. The learned workflows stay inside each project.

## What gets saved

A candidate must be project-local, conditional, verified by evidence, reusable beyond the current task, specific and actionable, safe to record, and not already covered by project instructions, `SkillsDs.md`, or an existing skill.

Good candidates:

- a debugging playbook for a project-specific subsystem
- a validation workflow for a risky change type
- a codegen recovery workflow tied to this repository
- a small script that checks a repeated mechanical invariant
- a corrected assumption future agents are likely to repeat

Bad candidates:

- one-off task results
- raw logs or stack traces
- generic engineering advice
- broad project rules that should live in project instructions
- secrets, private logs, customer data, or credentials

## Scripted skills

Some skills should include code. If a workflow is stable, repeated, mechanical, and easy to run incorrectly by hand, `project-skill-autolearn` can package it as:

```text
.claude/skills/<skill-name>/
  SKILL.md
  scripts/
    <script-file>
```

The script automates the brittle part. `SKILL.md` still explains when to use it, how to run it, what it verifies, and how to interpret results.

## Token model

The skill uses progressive disclosure:

- frontmatter is used for discovery
- the main `SKILL.md` contains only the core review loop
- templates and scripted-skill rules live in `references/`
- references are read only when needed

Current approximate sizes:

| File | Words |
| --- | ---: |
| `SKILL.md` | ~640 |
| `references/project-index-template.md` | ~160 |
| `references/project-skill-template.md` | ~220 |
| `references/scripted-skills.md` | ~310 |

Direct invocation loads the main skill. Creating indexes, new skills, or scripted skills loads only the matching reference.

## Install as a Claude Code marketplace

Add the marketplace in Claude Code:

```text
/plugin marketplace add YOUR_NAME/project-skill-autolearn
```

Install the plugin:

```text
/plugin install project-skill-autolearn@project-skill-autolearn
```

Check availability:

```text
/skills
```

Marketplace-installed plugin skills are namespaced. Direct invocation usually uses:

```text
/project-skill-autolearn:project-skill-autolearn
```

## Manual install

Clone the repository:

```bash
git clone https://github.com/YOUR_NAME/project-skill-autolearn.git
```

Copy the standalone skill:

```bash
mkdir -p ~/.claude/skills
cp -R project-skill-autolearn/.claude/skills/project-skill-autolearn ~/.claude/skills/
```

Windows PowerShell:

```powershell
git clone https://github.com/YOUR_NAME/project-skill-autolearn.git
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse ".\project-skill-autolearn\.claude\skills\project-skill-autolearn" "$HOME\.claude\skills\project-skill-autolearn"
```

Restart Claude Code or run `/skills`.

## Usage

Invoke directly:

```text
/project-skill-autolearn:project-skill-autolearn
```

Or ask naturally:

```text
Use project-skill-autolearn to review this session and preserve any reusable conditional workflow.
```

After direct invocation, it should stay active for the current conversation and review non-trivial work before final responses.

## Repository layout

```text
.claude-plugin/marketplace.json
plugins/project-skill-autolearn/
  .claude-plugin/plugin.json
  skills/project-skill-autolearn/
    SKILL.md
    references/
.claude/skills/project-skill-autolearn/
  SKILL.md
  references/
skills/project-skill-autolearn/
  SKILL.md
  references/
```

- `plugins/project-skill-autolearn/` is used by marketplace installation.
- `.claude/skills/project-skill-autolearn/` is the standalone manual-install copy.
- `skills/project-skill-autolearn/` is kept for compatibility with agents that use a plain `skills/` directory.

Keep all three skill directories in sync when editing.

## Validation

Validate the marketplace structure:

```text
/plugin validate .
```

Or from a shell with Claude Code available:

```bash
claude plugin validate .
```

## References

- [Claude Code plugin marketplaces](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)
- [Claude Code skills](https://docs.claude.com/en/docs/claude-code/skills)

## License

MIT
