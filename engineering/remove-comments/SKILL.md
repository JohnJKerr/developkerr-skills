---
name: remove-comments
description: Audit the code comments in a codebase or a named section of it. Categorise each as Tautology, Excuse, Stale or Decision Record, and present the inventory for approval. Then delete comments, file issues for hacks and move decisions into ADRs. Add a ratcheted lint rule against new comments and estimate the lines shed. Use when asked to remove or audit comments, or when a review flags them.
---

# Remove Comments

Code should explain itself through names, structure and tests. Comments tend to repeat the code, excuse a hacky implementation that others then copy, or drift out of date. Remove them, keep the knowledge that matters somewhere better suited to it, and stop new comments from appearing.

## Establish scope

Use the scope the user names: a directory, module, file set or the whole codebase. Default to the whole repository when none is given. Read applicable repository instructions, existing lint configuration, any ADR folder and the project's issue tracker conventions.

Exclude generated, vendored and third-party code. Exclude these functional or convention-required comments from the inventory, the lint rule and the estimate:

- Arrange/Act/Assert markers in tests.
- Lint, compiler and tooling directives, such as `eslint-disable`, `@ts-expect-error`, `#pragma`, `# type: ignore`, `//go:` and `# noqa`.
- Licence and copyright headers.
- Doc comments on the public API of a published library or package, such as XML docs or JSDoc. Doc comments on internal or application code are not exempt.

## Build the inventory

Find every remaining comment in scope, including trailing comments and multi-line blocks. Read enough of the surrounding code, history and documentation to judge each one. Use `git log` or blame when it helps establish whether a comment is stale or why a decision was made.

Categorise each comment:

- **Tautology:** repeats what the code already shows.
- **Excuse:** explains or apologises for a hacky, temporary or incomplete implementation, such as a workaround, a `TODO`, a `HACK` or "this is a bit messy but". The code is the problem; the comment lets it persist and invites imitation.
- **Stale:** refers to code, behaviour or implementation details that no longer apply, or that the code now contradicts. This includes commented-out code.
- **Decision Record:** records an important, non-obvious decision, constraint or trade-off that the code cannot express.

When a comment fits more than one category, choose by the action it needs. A comment that both explains a decision and admits a hack is an Excuse unless the hack is the deliberate, lasting decision. Flag borderline Excuse and Decision Record cases instead of deciding them silently.

## Present for approval

Before changing anything, present:

- The inventory, grouped by category, with each comment's location, a short quote and the reason for its category.
- Draft issues for Excuses. Each needs a clear title, the hack it describes, why it is a problem, a link to the code and a suggested direction for the fix. Group closely related Excuses into one issue when they describe the same underlying problem.
- Proposed ADRs for Decision Records, combining related comments into one record where they describe the same decision.
- The lint rule and ratchet you intend to add.
- The lines-shed estimate (see [Estimate lines shed](#estimate-lines-shed)).

Wait for explicit approval. The user may recategorise comments, edit issues or ADRs, or decide to keep some comments for now. Kept comments remain in the ratchet baseline.

## Act on each comment

After approval:

- **Tautology and Stale:** delete the comment. If a Tautology exists because a name is unclear, a rename within scope is acceptable; mention it in the report. Do not refactor beyond that.
- **Excuse:** delete the comment and file the approved issue in the project's tracker. Use the tracker the project already uses; for GitHub, use `gh issue create`. If no tracker is identifiable or accessible, ask the user rather than guessing. Do not fix the hack in this changeset.
- **Decision Record:** move the content into an ADR, then delete the comment. Follow the project's existing ADR location, numbering and format. Otherwise create `docs/adr/NNNN-short-title.md` with Status, Context, Decision and Consequences sections. Write the ADR so it can be understood without the code; consult the `document` skill when available ([../../writing/document/SKILL.md](../../writing/document/SKILL.md)). Do not leave a comment pointing to the ADR.

Remove blank lines left behind by deleted comments where they would leave awkward spacing. Run the project's build, tests and linters to confirm nothing depended on the removed text.

## Add a ratcheted lint rule

Ban comments in the agreed scope while allowing the exemptions above. Assume some comments will survive this changeset: the rule must pass on the current code, fail on any new comment and tighten as comments are removed.

Prefer the linter's own baseline or suppression mechanism. For example, ESLint (v9.24+) bulk suppressions record existing violations in `eslint-suppressions.json` through `--suppress-rule`, and `--prune-suppressions` removes entries that no longer apply. ESLint has no core rule banning all comments. Prefer a small local rule that reports `sourceCode.getAllComments()` minus the exemptions over adding a dependency.

Where the linter has no suitable rule or baseline, such as Roslyn analysers or Ruff, add a small script and a committed baseline:

- The script counts non-exempt comments per file in scope.
- It fails when a file's count exceeds its baseline or a new file contains comments.
- It rewrites the baseline when counts fall, so removed comments cannot return. Run it in CI and document the command to tighten the baseline.

Keep the ratchet in the project's existing lint or CI workflow. Explain the mechanism briefly in the PR or the project's contributing notes, without adding comments to explain it.

## Estimate lines shed

Count comment-only lines: lines that contain nothing but a comment, including every line of a multi-line block. Trailing comments shed no lines; count them separately. Exclude exemptions.

Report:

- Lines shed by this changeset.
- Lines that would be shed if every remaining comment were removed.
- The scope's total line count for context, and the percentage that comments represent.
- A breakdown by category.

Present these as estimates and state the counting method. Use a parser or the linter's comment list where practical; a regex count is acceptable for an estimate but can be fooled by comment markers inside strings.

## Report

Summarise what was deleted, which issues were filed (with links), which ADRs were created, how the ratchet works and how many comments remain in its baseline, and the lines-shed estimate. State the checks that were run and any limitations. Committing, pushing and creating PRs follow the user's normal instructions; use the `pull-request` skill when a PR is requested.
