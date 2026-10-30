---
name: bug-fixing
description: Investigate and fix bugs by forming a hypothesis, reproducing the issue with a back-end behaviour test or front-end Storybook story, and verifying a minimal correction. Stop to discuss hypotheses with the user when reproduction fails rather than applying a speculative patch.
---

# Bug Fixing

Form a hypothesis, reproduce the issue, then fix it and satisfy the reproducer. Keep investigation grounded in evidence and changes focused on the cause.

## Form a hypothesis

Read the bug report, expected behaviour and relevant code. Use static analysis of callers, control flow, contracts, domain rules and existing tests where useful to explain how the reported behaviour could arise. Ask for missing reproduction details when they materially affect the investigation.

State a concrete hypothesis and choose a test or story that can distinguish it from correct behaviour. Do not treat a plausible explanation as an established cause. Inspect the relevant blast radius so the proposed correction accounts for affected callers and behaviour.

## Reproduce before fixing

### Back end

Follow the established TDD conventions. Agree the public test seam with the user before writing the behaviour test, reusing explicit agreement already provided for the current change. Write and run a test that attempts to reproduce the reported issue and fails for the intended reason.

Use one act and exactly one assertion per test, with Arrange/Act/Assert comments where appropriate. Prefer meaningful fakes and observable outcomes over tests coupled to internal implementation. Compilation or environment failures do not establish reproduction of the bug.

### Front end

Add a Storybook story expressing the inputs, state or interaction needed to reproduce the issue. Render it and perform the relevant interaction to verify the failure before changing implementation. A story file existing or compiling is not itself evidence that the issue was reproduced.

Keep the story representative of the actual UI behaviour. Do not replace the faulty behaviour with mocks that hide the issue. Use the project's existing story and data-fixture conventions.

### If reproduction fails

Stop and discuss the hypothesis with the user. Briefly explain the evidence, what was attempted, what happened instead and the next plausible hypotheses or information needed. Wait for that discussion before continuing with a revised investigation or fix. Do not silently cycle through speculative patches or weaken the expected behaviour to manufacture a failure.

Distinguish inability to execute the reproducer from an executed attempt that did not reproduce the issue. Report execution blockers accurately and resolve them before implementation; never claim an unrun test or story demonstrated the failure.

## Correct and verify

Once reproduced, implement the smallest appropriate correction to the cause. Avoid unrelated cleanup or new abstractions. Rerun the reproducing test or story and verify that the expected behaviour is now satisfied.

Refactor while green when useful, without adding unrelated behaviour. Check relevant surrounding behaviour and affected consumers in proportion to the change. Retain the reproducing test or story as regression coverage. Do not remove or relax it merely to make the result pass.

Continue applying the engineering conventions:

- Keep business rules and invariants in Domain; confirm any new or changed aggregate boundaries before coding them.
- Use strict back-end red-green-refactor and relevant storage integration coverage where persistence behaviour is implicated.
- Preserve component-owned React Query data retrieval and mutations, and avoid prop drilling.
- Obtain explicit user permission before introducing `useEffect` or `useState`; do not use a bug fix as a reason to bypass this preference. Reuse permission already given for the relevant work.

Consult `tdd` and `ddd` when available for their full conventions. Repository sources are [../tdd/SKILL.md](../tdd/SKILL.md) and [../ddd/SKILL.md](../ddd/SKILL.md); installed agents may need those skills installed separately.

## Explain the result

Finish with a concise account of the cause, correction, reproducing test or story, checks actually performed and any remaining uncertainty. Distinguish verified behaviour from assumptions. Do not declare the bug fixed solely because a plausible code change was made.
