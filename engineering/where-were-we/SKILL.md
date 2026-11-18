---
name: where-were-we
description: Recap an engineering thread when returning to it after time away. Summarise the current state, verified against the repository and any PR, plus decisions made, decisions awaiting the user (blocking ones first) and remaining steps. Stop and wait for approval before resuming work.
---

# Where Were We

Bring the user back up to speed on a thread they have returned to after a few hours or days. Give them what they need to decide the next action, as succinctly as possible without dropping important information.

## Verify before summarising

Use the conversation for intent, decisions and scope, then check its claims against the actual state:

- Branch, uncommitted changes and recent commits on the branch.
- Any associated PR: state, CI checks and unresolved review comments.
- The most recent known test or build result and roughly how old it is. Do not run slow suites unless asked.

Keep checks read-only: do not commit, push, comment or change anything.

Flag discrepancies, such as work described as done that is not committed, or a PR state that differs from what was discussed. If the conversation has been compacted or is incomplete, state what cannot be confirmed rather than guessing.

## Present the recap inline

Use these sections, omitting any that are empty. Prefer short bullets; avoid a chronological retelling.

1. **Where we are**: the goal, what has been done and the current state in a few lines.
2. **Verified state**: branch, uncommitted changes, PR and checks, and any discrepancies.
3. **Decisions made**: each with a brief reason.
4. **Awaiting your decision**: each with a recommendation. List first and mark those that block progress or significantly alter the remaining work.
5. **Remaining steps**: in order, ending with the proposed next step.

## Stop

Do not resume work. Wait for the user's go-ahead or redirection. Answering a pending decision is not approval to continue unless the user says so.
