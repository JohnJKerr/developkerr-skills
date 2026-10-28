---
name: add-skill
description: Create a new skill in the DevelopKerr skills repository through intent-first questioning, a confirmed brief, and repository authoring with a README entry. Use when asked to add, create, or define a new skill for agents. Installing an existing skill alone is outside this workflow.
---

# Add Skill

Turn a skill idea into a fully authored, portable skill in this repository. Interview the user before writing: establish intent first, then uncover what is needed to meet it. Completion means repository files and an updated root README. Install only when explicitly requested.

## Gather context

Identify the target repository from the current workspace or the user's instructions. If running from an installed copy, author in the repository, not the installed directory. Ask for the repository location if it is unknown.

Read applicable repository instructions, the root README, and relevant existing skills to understand conventions and avoid overlapping capabilities. Read supplied references purposefully. Previous Launch AI material in Notion is background for a fresh set of skills; do not inherit its pack structure, skill-versus-agent distinction, publishing workflow, or other requirements unless the user chooses them.

Use information already provided to focus the interview. Do not ask the user to repeat answers available in the conversation or relevant sources.

## Establish intent

Ask small themed batches of questions, usually two or three at a time. Wait for answers before asking dependent follow-ups. Start with the purpose rather than implementation details. Establish:

- The problem or recurring task and who the skill serves.
- The desired outcome and what useful results look like.
- When the skill should apply, its boundaries, and what is outside its scope.

Challenge assumptions respectfully. Probe vague answers with concrete situations; point out contradictions and ask the user to resolve choices that would change the skill. Do not silently turn your own preferences into requirements. Briefly reflect the emerging intent before moving into detailed requirements, and resolve any material disagreement.

## Discover what the intent requires

Adapt subsequent batches to the skill. Explore the following where relevant, rather than treating them as a compulsory questionnaire:

- Inputs, their sources, required context, and handling of missing or conflicting information.
- Outputs, audience, format, examples, and qualitative expectations.
- Workflow, decisions, user interaction, and how much autonomy the agent should have.
- Tools, services, dependencies, access requirements, and portability constraints.
- Rules, exclusions, external actions, failure handling, and stopping conditions.
- Representative situations, difficult cases, and ways to judge whether the skill works.
- Name, repository category, and any supporting resources that would help execution.

Follow up until material gaps are resolved. Prefer a focused question about a consequential uncertainty over guessing. Distinguish requirements from suggestions and optional preferences. Stop questioning when the intent and requirements are sufficient to author the skill; do not invent edge cases just to extend the interview.

## Confirm the brief

Before creating skill content, present a concise brief covering purpose, triggers and boundaries, required behaviour, relevant inputs and outputs, constraints, and proposed repository location. Include acceptance criteria or a validation approach only when they provide a meaningful check. Advisory or judgement-based skills may instead use qualitative expectations and a review against intent; do not force artificial pass/fail tests.

Ask for explicit confirmation and wait. If the user requests changes, revise the brief and obtain confirmation of the revision. Read-only discovery can continue while waiting. Reconfirm material changes to the agreed intent or scope during authoring; routine implementation details do not require another approval.

## Author in the repository

After confirmation:

1. Create `<category>/<skill-name>/SKILL.md`. Follow existing categories and the user's choice; use `misc` for this skill. Use a lowercase, hyphenated skill name and match the folder name to it.
2. Include YAML frontmatter with `name` and a concise `description` that explains the capability and when to use it. Write clear instructions that preserve the confirmed intent and guide the agent's decisions.
3. Keep the core instructions portable across agents that support `SKILL.md`. Include environment-specific tools or configuration only when the skill needs them, and explain dependencies rather than assuming they are available everywhere.
4. Add scripts, references, or assets only when they materially support execution. Keep the entrypoint self-contained or link supporting material where it becomes relevant. Avoid generic scaffolding and duplicated instructions.
5. Update the root `README.md` skill catalogue with the name, category, relative link to `SKILL.md`, purpose, and a useful invocation example. Preserve existing entries and conventions.

## Review and finish

Review the files against the confirmed brief and check basic structure, frontmatter, names, relative links, and unfinished placeholders. Use an available skill validator when useful, recognising that structural checks do not establish behavioural correctness.

Where meaningful and feasible, exercise representative examples or run relevant scripts against the agreed expectations. For qualitative skills, review the guidance against the intended situations. Fix issues found within the agreed scope. Report what was actually checked and any material limitations; do not claim an unperformed test passed or require automated validation for every skill.

Finish with links to the authored skill and README and a concise account of the result. Install only if the user explicitly requested installation, using the target agent's supported skill location and preserving existing installations. Keep the repository as the source of truth and report installation separately from authoring. Do not commit, push, or publish solely because a skill was created.
