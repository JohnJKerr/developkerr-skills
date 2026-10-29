---
name: code-review
description: Review pull requests, local changes or existing codebases for correctness, performance, maintainability, security and the user's engineering conventions. Present actionable inline findings and a concise summary to the user before offering to publish PR comments. Does not edit code or submit a review verdict unless requested.
---

# Code Review

Keep it simple. Review for production correctness and performance, and for code that remains understandable and maintainable as it grows. Working code and passing tests do not excuse avoidable complexity or weak design.

## Establish scope and evidence

Determine whether the subject is a PR, local changes or an existing codebase. Establish the relevant base revision or review scope and read applicable repository instructions. Inspect surrounding code, callers, tests and task requirements as needed to understand behaviour and established patterns. Ask when a material scope ambiguity cannot be resolved from the request.

For a changeset, focus findings on changes and their consequences. For a broader codebase review, prioritise important paths and state the coverage limits. Do not imply exhaustive review of code you have not examined.

Run focused checks when practical and useful to resolve uncertainty. Distinguish observed failures from findings established by reading the code. State checks not performed when that materially limits the conclusion. Do not require a failing test to report a defect supported by a clear code path and trigger.

Review and report. Do not edit the code, add dependencies or publish feedback unless requested.

## General review principles

### Simplicity and readability

Examine the following in context:

- Nested loops: assess readability, input sizes and computational cost. Explain the concrete problem instead of mechanically demanding a different syntax.
- Comments compensating for unclear code: prefer domain names, clear control flow and small understandable operations. Preserve comments that explain a useful reason or constraint.
- Hasty abstractions: question interfaces, base classes, generic helpers and frameworks without a demonstrated need.
- Excessive DRY: do not force superficially similar operations together when their meaning or likely evolution differs. Small duplication can be clearer than a premature shared abstraction.
- Premature optimisation: require an actual workload, constraint or credible cost argument. Do not introduce complexity to address a hypothetical bottleneck.
- Poor readability: assess whether a colleague can follow the behaviour and decisions without reconstructing intent from incidental details.
- Oversized changesets: identify unrelated concerns or independently reviewable slices that would make the change easier to assess and integrate.

Offer the simplest useful correction. Avoid replacing one complexity with another or turning a review into an unrelated redesign.

### Correctness, performance and impact

Trace meaningful success and failure paths, including affected callers and consumers. Look for concrete production failures and performance problems. Describe the triggering conditions and consequence; distinguish demonstrated behaviour from assumptions about workload or usage.

Review domain changes for invariants, aggregate boundaries and blast radius across callers, persistence and affected behaviour. Consider compatibility and existing data when relevant. A change that works in isolation may still violate a domain rule or break another consumer.

Explicitly identify new conventions and departures from established patterns. Evaluate whether they are justified and what maintainers will need to understand. A justified departure is still worth summarising, but is not automatically a defect.

### Dependencies and security

Check each new dependency for necessity: could the existing platform or a simpler implementation satisfy the actual need? Consider its maintenance and relevant security implications. Use authoritative current evidence before asserting a specific vulnerability; do not infer safety or danger from a package name alone.

Inspect for exposed tokens, credentials and secrets, and for relevant authentication, authorisation, data isolation and unsafe input or output handling. Do not reproduce a secret's value in findings, tool output or published comments. Identify the location and credential type without exposing the value; where exposure is confirmed, explain the need to revoke or rotate it rather than treating deletion alone as sufficient. Do not perform credential changes without authorisation.

## Preferred engineering conventions

### Back end and domain

Apply the user's DDD conventions even when the code currently works: business rules belong in Domain, aggregate roots protect invariants, and project dependencies point inward. Confirmed aggregate boundaries should not be bypassed by controller, handler or persistence code.

Consult the `ddd` and `tdd` skills when available for the full conventions. Their repository sources are [../ddd/SKILL.md](../ddd/SKILL.md) and [../tdd/SKILL.md](../tdd/SKILL.md); installed agents may need those skills installed separately. Review the code's evidence against the conventions without claiming that commit contents prove the historical red-green sequence.

Check tests for:

- Exactly one act and one assertion per test, with Arrange/Act/Assert comments where appropriate. Helpers should not conceal multiple assertions to evade the rule.
- Scenario-based suites and outcome-based names.
- Observable behaviour exercised through appropriate public seams, with shared setup expressed clearly through builders when useful.
- Meaningful fakes in preference to mocks. Flag tests that mock away the logic they purport to test or merely verify internal call choreography.
- Coverage of the actual behaviour and risks. A passing HTTP smoke test does not establish domain correctness, and fake-backed tests do not establish MongoDB integration correctness.

Treat maintainability and convention findings as actionable even when tests pass. Do not impose new behaviour tests on a pure refactor or configuration change already adequately covered by existing tests.

### Front end

Look for unnecessary prop drilling, unclear component responsibilities, questionable effects and other concrete React smells. Components should own their React Query data retrieval and mutations rather than pass server state and operations through chains of intermediaries.

Flag `useEffect` or `useState` introduced without the user's explicit permission. Check task context for existing authorisation rather than requiring it again; when that context is unavailable, identify the missing confirmation without asserting that permission was never given.

Review UI states and relevant Storybook coverage. The user's front-end approach uses stories rather than the strict back-end TDD requirement. Do not demand back-end testing patterns for UI work.

## Classify actionable findings

- **Must fix:** A concrete issue that would break production, cause performance problems or expose a security risk. Explain the evidence, conditions and impact.
- **Should fix:** Other actionable readability, design, convention, dependency, test-quality or maintainability issues. These are worthwhile corrections, not dismissible nits.

Do not inflate severity to force attention or manufacture findings. If a concern remains uncertain, investigate where practical or present the specific open question as such. Keep positive observations and justified new conventions separate from defects.

## Present the review

Provide inline findings tied to precise file locations where supported. Keep ranges tight and explain the issue, impact and a useful direction for correction. Otherwise use clickable file references or PR diff links appropriate to the environment. Each finding should stand on its own without requiring the user to reconstruct the review.

Accompany the inline feedback with a concise summary grouped by Must fix and Should fix, plus new conventions and departures, including whether new dependencies are justified. Avoid repeating every inline paragraph in the summary. Briefly state material verification or scope limits. If no actionable issues were found, say so without claiming the code is defect-free.

For a PR, present the concrete review here first, then ask whether to post those comments to the PR. If posting is already explicitly authorised, follow that authorisation without asking again. Do not submit an approval, request-changes verdict or merge without explicit instruction. For local or codebase reviews, omit the PR publication question unless a relevant PR is part of the task.
