---
name: pull-request
description: Write succinct, traceable descriptions when creating or updating pull requests, especially for work completed independently of the user. Explain decisions, pattern departures, new abstractions, blast radius, task criteria and validation. Does not manage CI, review responses or merging.
---

# Pull Request

Make a pull request easy for a colleague to understand and review without needing the original conversation. Focus on the resulting change and the decisions that matter. This skill guides PR content; it does not independently authorise commits, pushes or publication.

## Establish what changed

Read the task's agreed scope and criteria, repository PR conventions or templates, and the actual diff against the intended base. Inspect relevant surrounding code and callers to understand established patterns and affected behaviour. Use commit history where it helps explain the changes; do not simply turn the commit log into a description.

Identify:

- The concrete problem and resulting behaviour.
- Pertinent decisions and their reasons.
- Code that departs from an existing pattern and why that departure is appropriate.
- New abstractions and the demonstrated need for each.
- The blast radius: affected components, behaviour and consumers, including material compatibility or operational implications.
- How the work meets the agreed task criteria, what remains incomplete, and what was actually checked.

Ground claims in the code and available evidence. If the task criteria are unavailable, say so or recover them from the task context; do not invent retrospective criteria and present them as agreed. If you cannot establish a pattern or impact confidently, state the uncertainty rather than claiming there is none.

## Write the description

Lead with the problem and resulting behaviour. Explain the important decisions succinctly in the way a human colleague would. Use a concrete before/after example when it makes a behaviour change easier to understand.

Cover the following information, adapting the layout and combining related points to keep it proportional to the change:

- **Change and decisions:** What the PR accomplishes and why the pertinent choices were made.
- **Pattern departures:** Identify and explain departures. Explicitly state when none were identified.
- **New abstractions:** Name each new abstraction and why it is needed. Explicitly state when none were introduced.
- **Blast radius:** Describe the meaningful effects on behaviour, components and consumers, including compatibility, data or deployment implications where relevant. Avoid replacing this with a list of changed filenames.
- **Task criteria:** Include a checklist against the agreed criteria. Check only items supported by the work and evidence. Leave incomplete or unverified items unchecked and explain the gap. If no criteria were agreed, state that rather than manufacturing a checklist.
- **Validation:** Briefly summarise checks actually performed, their results and material limitations. Distinguish automated evidence from manual review or assumptions.

Follow a repository template when present while retaining this information. A small PR may cover most of it in a few sentences plus the criteria checklist; a complex change may need short sections. Prefer specific, useful detail over boilerplate.

Write for someone who has not seen the chat. Omit conversational history, a chronological work diary and abandoned approaches unless they explain a material tradeoff. When scope changes, update the title and description to match the final implementation. A title should name the concrete change and follow the repository's convention.

## Keep the work reviewable

Prefer small commits that can each be reviewed on their own merits. When preparing commits within the authorised task, group related changes coherently and keep unrelated work out. Do not rewrite shared history merely to make the PR look tidier.

Before finalising the description, compare it with the diff: are the decisions, departures, abstractions and claimed outcomes accurate? Consider likely reviewer questions and answer the pertinent ones concisely. The Code Review skill may inform a readiness check when available, but it is not a required dependency.

If creating or updating the PR is authorised, use the available repository integration and verify the resulting PR identity. Otherwise provide the prepared title and description. Report the PR link when one was created or updated, or clearly identify the output as a draft description.

## Boundaries

This skill concerns creating or updating the PR's description, not an ongoing delivery loop. CI monitoring, fixing review comments and merging are outside its scope. Mention known check failures honestly without implying they were resolved. Code Review covers reviewing somebody else's PR; Delivery covers the broader approach of small changesets, iteration and refactoring as work proceeds.
