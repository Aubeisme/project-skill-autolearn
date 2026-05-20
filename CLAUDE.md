# CLAUDE.md

## Global skill distribution

- This repository packages `project-skill-autolearn` for global Claude Code installation from `.claude/skills/project-skill-autolearn/`.
- Keep the root `skills/project-skill-autolearn/` copy in sync as a compatibility copy for agents that use a plain `skills/` directory.
- The global skill must write learned strategies into the current target project, usually `.claude/skills/<project-skill-name>/SKILL.md` plus `SkillsDs.md`; do not write target-project lessons back into this distribution repo.
- Before the final response for a non-trivial task in this repository, run the closed-loop review in `project-skill-autolearn`: candidate capture, gate, merge/new, verify, index, future load.
