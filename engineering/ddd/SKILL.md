---
name: ddd
description: Model and implement back-end business behaviour using domain-driven design, including aggregate roots, invariants, value objects, repositories and domain services. Confirm aggregate boundaries before coding. Includes general principles and preferred .NET/MongoDB conventions.
---

# Domain-Driven Design

Keep business rules in the domain model and express them in the language of the business. Develop the model through small changes rather than extensive upfront design. The general principles apply across stacks; the .NET/MongoDB conventions describe the preferred implementation.

## General principles

### Establish the language and boundaries

Read the relevant code, requirements, tests and existing domain terminology. Use the same business terms in conversations, code, tests and concise documentation. Resolve ambiguous terms with the user rather than inventing generic names that conceal the uncertainty. Distinct bounded contexts may give the same term different meanings; keep their models separate and translate at their boundaries where needed. Do not introduce services or projects merely to represent hypothetical contexts.

Before establishing or changing aggregate boundaries, present a small domain sketch covering:

- Relevant business terms and their meanings.
- Proposed aggregate roots, owned entities and value objects.
- Invariants each root enforces.
- Cross-aggregate relationships and any coordination needed.

Wait for the user's confirmation before coding those boundaries. Reuse explicit agreement already given for the current change. If the model needs a material boundary change, update the sketch and obtain confirmation before proceeding. Keep the discussion scoped to the current feature rather than designing the entire system.

### Encapsulate business behaviour

An aggregate root owns a consistency boundary and enforces its invariants through behaviour methods. Callers ask it to perform domain actions, rather than setting properties and reconstructing its rules elsewhere. For example, prefer `account.AddUser(...)` over an application service directly modifying an account's user collection.

- Keep business rules in Domain, including when application orchestration initially lives in a controller.
- Expose only the public behaviour needed by callers. Keep supporting domain logic internal or private as appropriate; do not make internals public for tests.
- Protect child entities and mutable collections from external mutation that bypasses the root. Read access must not leak a mutable backdoor.
- Reference other aggregates by identity rather than retaining mutable object graphs across roots.
- Use entities where identity matters and immutable value objects where equality is defined by values.
- Provide a repository per aggregate root, rather than one per owned child entity. Repository operations should express domain needs without exposing database query internals.
- Prefer composition over inheritance. Extract abstractions when a demonstrated need justifies them; avoid generic repositories, base entities or service frameworks introduced speculatively.

Keep aggregates focused on the invariants they actually own. Do not make an aggregate large merely because objects are related in storage.

### Coordinate multiple aggregates

Use a domain service when multiple aggregates need to be updated in one unit of work. It owns the business coordination, works through domain behaviour, and preserves each root's invariants. Do not use it as a collection of rules that naturally belong on a root.

Keep storage sessions, transaction mechanics and other infrastructure outside Domain. When a use case requires several updates to succeed together, establish how the unit of work provides the required consistency and handles failure. Calling several repository saves does not by itself guarantee atomicity. Do not substitute eventual consistency for a required atomic operation without discussing the change with the user.

### Introduce events for an actual need

Introduce domain events only when a concrete side effect or cross-aggregate workflow warrants them. Express an event as an immutable fact in the domain's language. Keep knowledge of subscribers and delivery infrastructure outside the aggregate.

Decide dispatch timing, persistence ordering and failure handling for the actual use case. Do not introduce an event bus, outbox or other event infrastructure speculatively, and do not assume an event automatically provides a unit of work across aggregates.

## Preferred .NET/MongoDB conventions

### Dependency direction and ownership

Domain is the innermost project. Application depends on Domain; API, Storage/Database and External adapters look inward to Application/Domain. Domain must not depend on those outer projects.

Repository and external-service interfaces belong in Domain by default. An interface needed only by Application can live in Application. Place concrete MongoDB and external-service implementations in their respective adapters. Keep HTTP contracts and response mapping outside Domain.

Start with a simple application structure. Controllers can initially coordinate domain calls and persistence. Introduce MediatR and a CQRS application layer when refactoring warrants them, rather than scaffolding handlers and dispatch infrastructure for every new project. Moving orchestration should not move business rules out of Domain.

### Report expected rule failures

Use FluentResults for expected business-rule failures so the rest of the platform can identify why an operation failed. Follow the project's established result and error conventions. Do not reduce distinct business failures to an unexplained boolean or invent a large error taxonomy without need.

Map domain results to HTTP responses in the API layer. Keep HTTP status codes and controller concerns out of the domain model. Distinguish expected domain rejection from unexpected infrastructure or programming failures rather than disguising every failure as a business-rule result.

### Keep persistence outside the model

Keep MongoDB queries, mapping attributes and other persistence concerns outside Domain. Use separate class maps for persistence mapping in the storage adapter.

The following pragmatic accommodations are permitted:

- `ObjectId` identifiers in the domain model.
- Private property setters needed for MongoDB deserialisation.

These exceptions do not permit database access inside Domain or public mutation shortcuts. Keep invariants enforced through domain behaviour and keep other persistence details in the adapter.

## Develop and review the change

Apply the repository's TDD conventions to back-end behaviour: agree the public test seams before writing tests, then use strict red-green-refactor. The aggregate sketch and test seams answer different questions; they can be confirmed together when useful. Consult the `tdd` skill when available. Its repository source is [../tdd/SKILL.md](../tdd/SKILL.md); installed agents may need that skill installed separately.

Review the result against the agreed sketch: business rules remain in Domain, roots protect their invariants, dependencies point inward, and persistence does not bypass the model. Check any concrete cross-aggregate consistency requirement through the relevant behaviour and integration coverage. Use proportionate review rather than imposing an unrelated checklist on every change.

Finish with a concise explanation of the model decisions, behaviour changed and checks actually performed. Highlight material unresolved domain questions or consistency limitations.
