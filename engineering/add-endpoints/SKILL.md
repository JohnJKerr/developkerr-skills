---
name: add-endpoints
description: "Add ASP.NET endpoints through a staged test-first workflow: success-status integration test, separate domain/storage prerequisites, controller hand-off and status mapping tests, and handler orchestration tests where applicable. Agree the contract and test seams before starting."
---

# Add Endpoints

Add an endpoint in small red-green-refactor steps. Establish its route first, then build orchestration on separately tested domain and storage behaviour. Keep the current architecture; adding an endpoint does not itself justify introducing MediatR or new application layers.

## Agree the contract and seams

Inspect relevant endpoints, controllers, handlers, test projects and authentication policies. Establish the task's intended behaviour and follow existing route, request/response, validation and result-to-HTTP conventions. Resolve consequential choices rather than inventing new API conventions incidentally.

Present the proposed endpoint contract and public test seams to the user. Briefly explain what each seam covers and leaves out. Include the intended success status and the authentication/authorisation requirements, including anonymous access and account/resource ownership where relevant. Wait for confirmation before writing tests. Reuse agreement already provided for the current change.

Once agreed, work through the stages autonomously. Seek further confirmation only when a material contract or seam change is needed. New or changed aggregate boundaries also require the domain sketch confirmation described by the DDD conventions; it can be included in the initial discussion when known.

## Follow the staged workflow

### 1. Establish the route

Write an ASP.NET integration test in `Api.IntegrationTests` asserting only the intended success status code for an appropriate request. Use the contract's success status; do not force HTTP 200 when a different success status was agreed.

Run the test to establish the intended failure. Implement the minimum route/controller behaviour needed to make it pass. This is an initial step, not evidence that orchestration or domain behaviour is complete. Replace temporary success-only behaviour as the subsequent tests drive the implementation.

Keep API integration assertions limited to the success status. Do not add payload, persistence or business-rule assertions here; those belong at the relevant unit or storage seams.

### 2. Complete domain and storage prerequisites

If the endpoint needs new domain or storage behaviour, implement that separately before testing and implementing the orchestration that consumes it. Use focused TDD cycles in `Domain.Tests` and, for MongoDB integration, `Storage.Tests` with Testcontainers.

Keep business rules in Domain. Use existing interfaces and meaningful fakes for orchestration tests once the prerequisite behaviour is available. Avoid building the whole feature inside the first integration-test implementation.

### 3. Test controller responsibilities

Add one controller unit test at a time in `Api.Tests`, then the minimum implementation to satisfy it.

- When the controller directly orchestrates domain primitives, test that orchestration through observable outcomes using fakes.
- When it delegates to MediatR, use an in-memory test mediator that records the submitted command. Assert that the intended command was received, including the relevant mapped input. Successful execution of the real handler is not required by this test.
- Test mapping of results to HTTP status codes in separate tests. Supply controlled results through the test mediator or established test setup when needed for the mapping being exercised.

Prefer the recording test mediator over mock call expectations on `ISender` or `IMediator`. Do not turn a hand-off test into an end-to-end handler test. Follow the project's established result conventions, including FluentResults where used, and keep HTTP mapping in the API layer.

### 4. Test handlers where present

If the architecture has handlers, add focused tests in `Application.Tests` for their orchestration. Use fakes and arrange state through the relevant interfaces. Verify the correct data is returned or persisted, with a separate test for each outcome.

Do not duplicate the controller hand-off assertion here or mock away the handler logic under test. Domain rules should already be covered through domain behaviour tests; storage mechanics should already be covered in storage integration tests.

## Test discipline and authentication

Apply strict red-green-refactor at each stage. Every test has one act and exactly one assertion, with `// Arrange`, `// Act` and `// Assert` where appropriate. Use scenario-based suites, outcome-based names and builders for useful shared setup. Compilation failure alone is not a behavioural red; minimal declarations or stubs may be added to reach an executable failing test. Never claim an unrun red or green. Resolve execution blockers before proceeding with implementation.

Follow the project's OAuth provider and policies. Use its integration-test authentication setup. Prefer exercising real authentication through an available M2M token when that is the project's approach. Do not expose tokens in output or commit them to the repository.

A project may use custom test authentication. Recognise and report that this leaves the real authentication implementation untested; do not describe a successful test-auth request as proof that production authentication works. Do not weaken production policies or introduce an authentication bypass to make a smoke test pass.

The full back-end conventions are in the `tdd` and `ddd` skills when available. Repository sources are [../tdd/SKILL.md](../tdd/SKILL.md) and [../ddd/SKILL.md](../ddd/SKILL.md); installed agents may need those skills installed separately.

## Finish

Rerun relevant tests after the final implementation, including the original success-status integration test. Check that the endpoint now fulfils the agreed behaviour rather than merely returning a successful status. Keep the changeset focused on that endpoint and its necessary prerequisites.

Briefly report the endpoint delivered, behaviour covered, checks actually performed and any remaining limitations, including authentication coverage. Do not imply that smoke-test success establishes business correctness.
