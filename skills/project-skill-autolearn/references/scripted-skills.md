# Scripted Skills

Some project skills should include code. If a reusable workflow is mechanical enough, package it as an executable helper instead of leaving every step as prose.

Use this layout:

```text
.claude/skills/<skill-name>/
  SKILL.md
  scripts/
    <script-file>
```

Package a workflow as a script only when all are true:

- The steps are stable, repeated, mechanical, and easy to run incorrectly by hand.
- Inputs and outputs can be described clearly.
- The script can be verified with a command, dry run, fixture, or observable result.
- The repository already has a suitable runtime, or the runtime is standard for the project.
- The script will not hide judgment-heavy decisions that an agent should still make explicitly.
- The script is small and purpose-built; it automates the brittle part, not the agent's reasoning.

Do not script:

- One-off migrations, exploratory debugging, or workflows with many human judgment points.
- Commands that mutate important state without a dry-run or clear verification path.
- Shell-specific snippets that do not match the current project environment.
- Bash scripts for Windows-first projects unless the repository already depends on Bash, WSL, Git Bash, or Unix-like CI.

Runtime choice:

- Prefer an existing project runtime: `package.json` suggests Node/TypeScript; Python projects can use Python; Windows-first automation can use PowerShell.
- For cross-platform scripts, prefer Python or Node over Bash when the repository does not already require a POSIX shell.
- On Windows-first projects, use `.ps1`, Python, or Node. Avoid `.sh` unless Bash support is verified.
- Document the exact command to run the script from repository root.

Script rules:

- Keep scripts under `.claude/skills/<skill-name>/scripts/`.
- Include required arguments, environment variables, and working directory in `SKILL.md`.
- Prefer dry-run, read-only, or explicit confirmation modes for risky operations.
- Verify the script before indexing the skill.
- Never store secrets or machine-local absolute paths inside the script.
