# DevelopKerr Skills

A fresh collection of portable skills for agents, authored in this repository. Earlier Launch AI notes in Notion can inform new skills; each skill's requirements are established independently.

## Skills

| Skill | Category | Purpose | Example |
| --- | --- | --- | --- |
| [add-skill](misc/add-skill/SKILL.md) | Misc | Establish intent through probing questions, gather requirements, confirm a brief, and author a new skill with a README entry. | "Use add-skill to create a skill for reviewing API designs." |

## Adding a skill

Use `add-skill` to work through the idea in small themed question batches. It challenges assumptions and resolves material gaps before presenting a brief for confirmation. Once confirmed, it authors the skill under `<category>/<skill-name>/SKILL.md` and updates this catalogue.

Acceptance criteria and validation are used where they provide a meaningful check. Qualitative skills can be reviewed against their intent without artificial tests. Completion means a fully authored skill in the repository; installation is a separate, explicit request.

## Using skills

Each skill has a `SKILL.md` entrypoint with its name, description, and instructions. Supporting resources are included only where useful. Use the installation and invocation mechanism supported by your agent.

For Codex, copy an individual skill directory (for example, `misc/add-skill`) into `$CODEX_HOME/skills/`, or `~/.codex/skills/` when `CODEX_HOME` is unset. The installed directory is named after the skill, without the category directory. Invoke this skill with `$add-skill` once it is available. After repository changes, refresh the installed copy explicitly; the repository remains the source of truth.
