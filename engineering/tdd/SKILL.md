---
name: tdd
description: Apply strict behaviour-driven red-green-refactor when adding or changing back-end behaviour, including bug fixes. Agree test seams before writing tests. Includes general principles and preferred .NET/xUnit conventions. Front-end work uses Storybook instead of this TDD requirement.
---

# Test-Driven Development

Use short red-green-refactor cycles to implement back-end behaviour through agreed public boundaries. Keep changes small enough to integrate continuously. The general principles can be used on another stack; the .NET conventions capture the preferred implementation approach.

## General principles

### Agree the seams first

Before writing tests, inspect the relevant code, existing tests, and task requirements. Propose the public boundaries at which to observe the behaviour: for example, an aggregate root, application handler, controller, or storage interface. These boundaries are the test seams.

For each proposed seam, briefly state what it covers and what it leaves out. Ask the user to confirm the seams and wait before writing tests. Reuse explicit agreement already given for the current change. If another seam becomes necessary, agree it before adding tests there.

Keep this discussion scoped to the current small change. Settle the boundaries needed for the next behaviour without designing the whole feature or introducing speculative interfaces. Prioritise important behaviour and complex logic; do not duplicate every outcome at every layer.

### Test behaviour

- Describe observable outcomes through the agreed public interface. Keep domain internals internal; do not expose implementation details just to test them.
- Avoid tests tied to private methods, internal structures, or a particular collaborator call sequence. A behaviour-preserving refactor should leave behaviour tests useful.
- Each test has a single act and exactly one assertion. If there are two outcomes to verify, write two tests. Do not hide several assertions in a helper to evade this rule.
- Mark the sections with `// Arrange`, `// Act`, and `// Assert` where appropriate. Preparatory operations belong in Arrange; Act performs the behaviour under test once.
- Derive the expected outcome from the requirement or a concrete example, rather than repeating the production algorithm in the assertion.

### Run the cycle

1. **Red:** Write one test for the next behaviour at an agreed seam. Run it and establish that it fails for the intended behavioural reason. For a bug fix, make the test reproduce the bug.
2. **Green:** Implement only enough production code to satisfy that test. Run it and the relevant existing tests; resolve regressions before adding another behaviour.
3. **Refactor:** With tests green, improve naming, remove useful duplication, and simplify structure without changing behaviour. Prefer composition over inheritance and avoid hasty abstractions. Rerun the affected tests after changes.
4. Repeat for the next small behaviour. Do not write a batch of failing tests and then implement the entire feature against them.

If a new public type or member is needed to compile the first test, add only the minimal declaration or stub needed to reach an executable behavioural failure. A compilation error alone does not establish red. Do not add working behaviour before observing that failure.

Never claim red or green without running the tests. If execution is blocked, report the blocker and resolve it before proceeding with implementation. Keep any preparatory work limited to establishing a runnable test.

Pure refactors and configuration or wiring changes can rely on existing coverage when they introduce no observable behaviour. Do not invent tests that merely mirror configuration. When such a change alters observable behaviour, test that behaviour through an agreed seam first.

### Name scenarios and outcomes

Name suites for the action or context, and tests for the outcome:

```csharp
public class WhenAddingAUser
{
    // The_user_is_associated_to_an_account
}

public class WhenTheAccountHasNoLicenses
{
    // A_user_cannot_be_added
}
```

Use domain language rather than implementation names such as `Repository_calls_insert` or `TestAddUser`.

Start with readable inline setup. When setup is shared across tests or suites, extract domain-expressive builders, for example:

```csharp
var account = new GivenAnAccount()
    .WithNoAvailableUsers()
    .Build();
```

Prefer meaningful domain state over bags of raw property setters. Builders should make ordinary valid arrangements easy and allow specific scenarios to be expressed clearly. Each test gets its own mutable state. Do not create a general fixture framework before repeated setup justifies it.

## Preferred .NET conventions

### Tooling and dependencies

Use xUnit for new .NET/ASP.NET test projects. In existing projects, use the established testing tools unless a change is requested; do not migrate frameworks incidentally.

Prefer fakes over mocks. An `InMemoryUserRepository` can satisfy the same interface as `MongoUserRepository`; arrange its state through that interface and observe outcomes through the agreed seam. Avoid fake-only backdoors or reflection into production internals. Use the test suite's existing assertion style while retaining exactly one assertion per test.

Fakes support fast behaviour tests. They do not establish that MongoDB queries or mappings work; exercise storage integration separately with MongoDB Testcontainers. External adapters can use fakes for the external service boundary.

### Test project responsibilities

Use this layout where the corresponding production layers exist:

| Project | Responsibility |
| --- | --- |
| `Api.IntegrationTests` | ASP.NET integration smoke tests asserting that an endpoint can return HTTP 200 for a suitable successful request. |
| `Api.Tests` | Unit tests of controller behaviour. |
| `Application.Tests` | Unit tests of application handlers, when present. |
| `Domain.Tests` | Unit tests of domain behaviour through the appropriate public domain boundary. |
| `Storage.Tests` | MongoDB integration tests using Testcontainers. |
| `External.Tests` | Unit tests of external adapters with external service boundaries faked. |

Choose the relevant suite for each behaviour. An HTTP 200 smoke test does not establish domain correctness. Do not copy all business assertions into every layer.

Follow the project's actual stage of development. Application orchestration may initially live in controllers; test it there. Do not introduce MediatR, CQRS, empty projects, or extra layers merely to satisfy this table. When orchestration moves into handlers, keep its tests aligned with the new seam and preserve domain behaviour coverage.

## Scope and reporting

This strict TDD requirement applies to back-end work. Front-end UI work uses Storybook stories under the user's front-end conventions; do not impose this back-end test workflow on it. Keep back-end business behaviour under this skill even when the feature also has a UI.

At completion, briefly report the behaviours covered, tests actually run and their results, and any unresolved blockers. Prefer a concise account of evidence over a detailed transcript of each cycle.
