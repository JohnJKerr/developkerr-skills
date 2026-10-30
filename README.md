# DevelopKerr Skills

A fresh collection of portable skills for agents, authored in this repository. Earlier Launch AI notes in Notion can inform new skills; each skill's requirements are established independently.

## Skills

| Skill | Category | Purpose | Example |
| --- | --- | --- | --- |
| [add-skill](misc/add-skill/SKILL.md) | Misc | Establish intent through probing questions, gather requirements, confirm a brief, and author a new skill with a README entry. | "Use add-skill to create a skill for reviewing API designs." |
| [tdd](engineering/tdd/SKILL.md) | Engineering | Agree test seams, then develop back-end behaviours with strict red-green-refactor, scenario-based tests, and preferred .NET/xUnit conventions. | "Use tdd to add account licence checks before adding a user." |
| [ddd](engineering/ddd/SKILL.md) | Engineering | Confirm aggregate boundaries and model business behaviour with protected invariants, inward dependencies, and preferred .NET/MongoDB conventions. | "Use ddd to model account licences and user allocation." |
| [pull-request](engineering/pull-request/SKILL.md) | Engineering | Write succinct PR descriptions explaining decisions, pattern departures, new abstractions, blast radius, agreed criteria and validation. | "Use pull-request to create a PR for the completed account licence changes." |
| [code-review](engineering/code-review/SKILL.md) | Engineering | Review PRs, local changes or codebases for simplicity, correctness, performance, maintainability, security and engineering conventions; present findings before publishing. | "Use code-review to review these changes and highlight new conventions." |
| [add-endpoints](engineering/add-endpoints/SKILL.md) | Engineering | Add ASP.NET endpoints through staged TDD: a success-status smoke test, separate domain/storage prerequisites, controller hand-off and mapping, and handler orchestration. | "Use add-endpoints to add an endpoint for allocating an account licence." |
| [pair-programming](engineering/pair-programming/SKILL.md) | Engineering | Let the agent drive while you steer, using interactive implementation slices, concise reasoning, alternatives and senior engineering judgement. | "Use pair-programming to work through this licence allocation problem with me." |
| [hand-off](engineering/hand-off/SKILL.md) | Engineering | Prepare a destination-specific inline hand-off, including endpoint contracts and known errors for front-end consumers, for you to send. | "Use hand-off to prepare the completed licence endpoint details for the front-end agent." |
| [bug-fixing](engineering/bug-fixing/SKILL.md) | Engineering | Form a hypothesis, reproduce the issue in a behaviour test or Storybook story, then fix and verify it; discuss failed reproduction before proceeding. | "Use bug-fixing to investigate why licence allocation fails for this account." |

## Roadmap

These skills are planned; their requirements and briefs will be established before authoring.

### Misc

- **Revise Skill** (`revise-skill`): Improve an existing skill after experience using it. First capture what is wrong with the current skill, then follow a process similar to `add-skill`: probe the required changes, confirm a revised brief, and update the skill and its documentation. Use acceptance criteria and validation where meaningful.

### Engineering

- Front-End — discovery in progress. React Query for data retrieval and mutations, owned by the components that need them; avoid prop drilling. Use `useEffect` or `useState` only with explicit user permission.
- Document
- Feature Map
- Explain
- Self-Host
- Refactor
- New Project
- Delivery
- Start Task

## Adding a skill

Use `add-skill` to work through the idea in small themed question batches. It challenges assumptions and resolves material gaps before presenting a brief for confirmation. Once confirmed, it authors the skill under `<category>/<skill-name>/SKILL.md` and updates this catalogue.

Acceptance criteria and validation are used where they provide a meaningful check. Qualitative skills can be reviewed against their intent without artificial tests. Completion means a fully authored skill in the repository; installation is a separate, explicit request.

## Using skills

Each skill has a `SKILL.md` entrypoint with its name, description, and instructions. Supporting resources are included only where useful. Use the installation and invocation mechanism supported by your agent.

For Codex, copy an individual skill directory (for example, `misc/add-skill`) into `$CODEX_HOME/skills/`, or `~/.codex/skills/` when `CODEX_HOME` is unset. The installed directory is named after the skill, without the category directory. Invoke this skill with `$add-skill` once it is available. After repository changes, refresh the installed copy explicitly; the repository remains the source of truth.
