# Project Skill Autolearn

`project-skill-autolearn` is a global Claude Code skill for preserving reusable project-specific know-how.

Install it globally, then use Claude Code normally inside any repository. After non-trivial work, the skill reviews what was learned and, only when it passes a strict gate, writes a project-local skill into that current repository.

When invoked directly, it bootstraps the current project by creating `SkillsDs.md` and `.claude/skills/` if they are missing, then keeps the autolearn responsibility active for the rest of the current conversation.

## Install as a Claude Code marketplace

This repository includes Claude Code plugin marketplace metadata.

After publishing this repository to GitHub, install it in Claude Code with:

```text
/plugin marketplace add YOUR_NAME/project-skill-autolearn
```

Then install the plugin from that marketplace:

```text
/plugin install project-skill-autolearn@project-skill-autolearn
```

Run `/skills` to confirm `project-skill-autolearn` appears.

## Install manually from GitHub

Clone the repository:

```bash
git clone https://github.com/YOUR_NAME/project-skill-autolearn.git
```

Copy the Claude Code skill into your personal skills directory:

```bash
mkdir -p ~/.claude/skills
cp -R project-skill-autolearn/.claude/skills/project-skill-autolearn ~/.claude/skills/
```

On Windows PowerShell:

```powershell
git clone https://github.com/YOUR_NAME/project-skill-autolearn.git
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse ".\project-skill-autolearn\.claude\skills\project-skill-autolearn" "$HOME\.claude\skills\project-skill-autolearn"
```

Then restart Claude Code or run `/skills` to confirm `project-skill-autolearn` appears.

## Manual install for Claude Code

Copy this folder into your personal Claude Code skills directory:

```text
.claude/skills/project-skill-autolearn/
```

to:

```text
~/.claude/skills/project-skill-autolearn/
```

Then restart Claude Code or run `/skills` to confirm `project-skill-autolearn` appears.

## Publish this repository

From this directory:

```bash
git init
git add .
git commit -m "Add project skill autolearn"
git branch -M main
git remote add origin https://github.com/YOUR_NAME/project-skill-autolearn.git
git push -u origin main
```

Create the GitHub repository first at `https://github.com/new`, make it public, and do not add another README there.

The marketplace entry point is:

```text
.claude-plugin/marketplace.json
```

The packaged plugin is:

```text
plugins/project-skill-autolearn/
```

## What it creates in each project

On direct invocation, the project gets the lightweight storage structure:

```text
<project>/
  .claude/
    skills/
  SkillsDs.md
```

Reusable project strategies are then written to:

```text
<project>/
  .claude/
    skills/
      <project-skill-name>/
        SKILL.md
  SkillsDs.md
```

`SkillsDs.md` is the lightweight index. Future agents should scan it only when blocked and load only the one matching project skill.

## Compatibility

The standalone `.claude/skills/project-skill-autolearn/` and root `skills/project-skill-autolearn/` copies are kept for manual installation and agents that use a plain `skills/` directory. For marketplace installation, Claude Code uses `plugins/project-skill-autolearn/`.

## License

MIT
