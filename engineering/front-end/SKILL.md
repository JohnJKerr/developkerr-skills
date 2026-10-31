---
name: front-end
description: Build React applications or Astro sites with self-contained components, data access close to the consumer, minimal prop drilling and Storybook stories alongside implementation. Includes preferred TypeScript/Tailwind stacks and requires user permission before introducing useState or useEffect.
---

# Front-End

Build simple, readable components that the user can inspect and test through Storybook. Apply the same component-design principles to React applications and Astro sites, adapting the implementation to the project's runtime and conventions.

## General principles

### Keep components self-contained

Keep responsibility and the data needed to fulfil it close together. Feature components should own their data retrieval and mutations rather than require a chain of ancestors and intermediaries to supply server state or operations.

Lightweight reusable components may receive direct props. Prop passing is not inherently wrong; heavy prop drilling is a smell that responsibilities or boundaries need reconsidering. Do not introduce a global store, context hierarchy or other abstraction merely to eliminate every prop. Share data-access code when it provides a concrete benefit while keeping ownership clear.

Keep components and control flow readable. Prefer named intermediate variables over heavily nested expressions or ternaries. Avoid hasty abstractions, excessive DRY and unnecessary dependencies. Follow existing project patterns unless a change is justified and discussed.

### Use state deliberately

Prefer ordinary or derived variables when persistent reactive state is unnecessary. Derive values from existing inputs or query results rather than copying them into local state and synchronising them.

Obtain explicit user permission before introducing `useState` or `useEffect`. Explain the concrete need and relevant alternatives. Reuse permission already given for the relevant work rather than asking again.

An ordinary variable does not substitute for state that must survive renders or update the UI. If an interaction needs that state, discuss the requirement with the user. Do not bypass the permission requirement through a wrapper hook or substitute another mutable mechanism solely to avoid asking.

### Add stories alongside implementation

Develop Storybook stories alongside the components so the user can inspect and test them as the work progresses. Include a success state and the specific scenarios the component needs, such as loading, empty, error or a particular interaction. Choose useful stories rather than mechanically creating every possible state for every component.

Use the project's established story and data-fixture conventions. Keep states representative of the component's real inputs and data access. Render the relevant stories and exercise important interactions where practical; merely creating a story file does not establish that the UI works.

Verify relevant layout and interactions, including responsive or accessibility behaviour where affected by the change. Scale checks to the component and disclose material limitations. Do not impose strict back-end TDD on UI work. For a front-end bug, first reproduce it in a story, then verify the correction against that story.

### Honour the back-end contract

Read the actual endpoint contracts or verified hand-off before integrating. Handle the relevant request and response shapes, authentication requirements and known error statuses. Ask about material gaps rather than inventing contract details.

Keep business rules in the back end. The UI can present available actions, validate input for usability and explain failures, but must not become the sole enforcer of domain invariants or authorisation.

## Preferred stack conventions

### React applications

Prefer React, TypeScript, Tailwind and DaisyUI. Use React Query for server data retrieval and mutations, owned by the components that need them. Avoid duplicating query results in local state or fetching through effects when query mechanisms already express the requirement.

Follow the project's existing query-key, mutation and cache-update conventions. Account for the relevant UI changes after a mutation using the query mechanisms appropriate to that project. Do not add a parallel state or data-fetching framework without a demonstrated need and discussion.

Use DaisyUI components and Tailwind styling consistently with the existing UI. Preserve established visual patterns while keeping component responsibilities clear.

### Static Astro sites

Prefer Astro, TypeScript and Tailwind. Apply the same self-contained component and Storybook approach, with data access close to the component that needs it. Respect the distinction between static/build-time work and browser interaction.

Do not introduce client-side React or React Query solely to fetch static content. Where the project uses interactive React components, apply the React data and state conventions within those components. Discuss a runtime or component-framework change when the desired behaviour requires one, rather than silently expanding a static site into an application.

### Existing projects

Use the project's established stack and supported integrations. These preferences do not authorise an incidental framework migration or installation of a new dependency. Identify a material mismatch with the desired approach and agree the necessary change with the user.

## Finish

Keep changes small and reviewable. Briefly explain what changed, which stories were added, what was checked and any unresolved contract or UI questions. Identify sketches or unverified behaviour clearly so the user knows what is ready to test.
