---
name: delivery
description: Deliver coherent, tested and shippable changesets with early user review. Prefer small slices, allowing larger refactors with one focused purpose. Separate prerequisite concerns and stop to agree newly expanded scope. Applies during implementation alongside TDD, DDD and endpoint workflows.
---

# Delivery

Make sound engineering decisions and take the time needed to deliver a coherent, tested, shippable changeset. Keep the implementation focused on the current slice and avoid over-implementing. Small slices let the user review and course-correct before more work accumulates.

## Choose the next shippable slice

Use the agreed task and current code to identify the next focused outcome, what is needed to achieve it, and what remains for later. Keep this discussion brief and practical rather than planning the whole feature in detail. Reuse an agreed slice without asking for approval of routine edits within it.

Prefer breaking work across layers into smaller slices where practical: domain behaviour first, then persistence, API and application orchestration. Necessary work across several layers is a reason to look for smaller boundaries, not automatic justification to include it all in one changeset. Choose boundaries that keep each result coherent and shippable.

Refactors are an exception to the preference for small slices. A refactor aimed at one clear purpose may inevitably require a large changeset across files or layers. Keep the necessary changes together when splitting them would undermine coherence or leave the system in an artificial intermediate state. Judge the boundary by the agreed purpose, not file count or diff size; explain the reach and verify the affected behaviour. This does not permit unrelated cleanup or additional refactoring goals to accumulate in the same slice.

Each slice must leave the system working without relying on unfinished follow-up work. An internal domain or persistence capability can be shippable before a user-facing feature is complete, provided existing behaviour remains sound. Do not call a stub, a fake success response or a partially wired feature shippable merely because its current tests pass.

## Implement within the boundary

- Implement what the current slice needs. Defer speculative features, abstractions, infrastructure and unrelated cleanup.
- Make the implementation readable and maintainable. A small diff does not justify a hack, weakened invariant or skipped engineering work.
- Refactor as work proceeds while tests are green. Keep local improvements within the slice; treat broader refactors, model replacements and migrations as separate concerns.
- Follow the relevant TDD, DDD and front-end conventions. A test cycle is a unit of development within a slice; several successful cycles do not establish that the overall changeset remains focused.
- Check the accumulating diff and blast radius as you learn. Passing tests establish evidence about behaviour, not permission to expand scope.

## Stop when a separate concern emerges

When a prerequisite or expanding blast radius materially changes the slice's agreed purpose or scope, stop and hand control back. Necessary edits across the reach of an agreed, focused refactor do not by themselves constitute scope expansion. This rule applies when a separate concern emerges, including discovering that a feature requires a model replacement, migration or broader refactor with its own consequences. Do not keep widening the change merely to make affected callers compile or tests pass.

Briefly explain:

1. What emerged and how it differs from the agreed slice.
2. What has already changed and what is currently verified or incomplete.
3. The proposed smaller prerequisite slice that should land first, its impact, and what will remain afterwards.

Wait for the user's agreement before implementing the split or continuing the expanded work. Do not silently discard existing work, rewrite history or claim the current state is shippable if it is not. Once the split is agreed, get the prerequisite to a coherent, tested state and hand back before moving to the next slice.

For example, adding a receipt may reveal that `ChargePaymentDateOverride` needs replacing with `ChargeReceiptsOverride`, affecting Application and Storage. Treat that replacement as a distinct concern, propose it as a prerequisite, and agree its boundaries with the user. Do not absorb the replacement and all its downstream changes into the receipt slice solely because the feature needs it. Split the prerequisite further by layer when that produces coherent, shippable increments.

## Hand back at the slice boundary

Verify the slice with relevant checks and review the diff against its agreed outcome. Existing behaviour must remain sound, and any new behaviour must have appropriate coverage. Report failed or unavailable checks honestly rather than claiming readiness from partial evidence.

At the end of each slice, succinctly explain what is shippable, the important decisions, what was checked and the proposed next slice. Give the user an opportunity to review and course-correct; wait for direction before starting that next slice unless they have explicitly authorised continuation across those boundaries.

Several reviewed slices may later form one PR. Slice boundaries need not match PR boundaries. This skill does not itself authorise commits, pushes, PR creation, deployment or merging; follow any explicit authorisation already given for those actions. The Pull Request skill handles the description when a PR is requested.
