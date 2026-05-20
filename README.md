# Project Skill Autolearn

`project-skill-autolearn` is a global Claude Code skill for preserving reusable project-specific know-how.

Install it globally, then use Claude Code normally inside any repository. After non-trivial work, the skill reviews what was learned and, only when it passes a strict gate, writes a project-local skill into that current repository.

## Install from GitHub

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

## What it creates in each project

By default, reusable project strategies are written to:

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

The root `skills/project-skill-autolearn/` copy is kept for agents that use a plain `skills/` directory. For Claude Code distribution, prefer `.claude/skills/project-skill-autolearn/`.

## License

MIT
