---
name: hand-off
description: Prepare an inline hand-off when a completed slice of work needs to pass to another agent, context or project. Establish the destination and tailor the content, including endpoint contracts and error statuses for front-end consumers. Prepare material for the user to send; do not deliver it externally.
---

# Hand Off

Prepare a concise, self-contained hand-off for a completed slice of work. Give the recipient what they need to continue without the original conversation.

## Establish the destination

Ask where the hand-off is going before preparing it, unless the user has already specified the destination. It may be another agent, a fresh context or another project, commonly the front end. Clarify the recipient's intended next task if that materially affects the content and is not apparent from context.

Tailor the hand-off to that destination. Do not include every implementation detail simply because it is available.

## Ground the content

Read the implemented code, relevant contracts and available check results for the completed slice. Use the conversation for decisions and scope, but verify implementation claims against the actual work. Distinguish delivered behaviour from plans, unresolved details or assumptions.

Use the recipient's likely access when choosing references: local file paths alone may be unusable in another project or context. Include enough contract or decision detail inline, with useful repository, PR or file references as appropriate. Do not expose credentials, tokens or private data in examples.

## Adapt the hand-off

### To the front end

Include the integration details the consumer needs:

- The delivered capability and intended UI use.
- Endpoint methods and routes, including relevant path and query parameters.
- Authentication and authorisation requirements, including account/resource scoping where applicable.
- Request and response contracts: field names, types, required or optional values, relevant nullability and success statuses.
- Known error statuses and their meanings, including the error response shape or codes where implemented.
- Small request/response examples when they clarify the contract.
- Material limitations, unresolved details or compatibility concerns affecting integration.

Report known behaviour accurately. Do not invent error mappings, fill contract gaps with guesses or assume a success-only integration test proves all paths work. Identify anything the recipient must confirm before implementing against it.

### To another agent or context

Include the completed scope, pertinent decisions and reasons, relevant code locations and contracts, checks actually performed, outstanding issues and the next useful step. Carry forward consequential constraints or agreements that would otherwise be lost with the conversation.

Keep the hand-off focused on resuming the work. Avoid a chronological transcript, a full codebase tour or an elaborate plan for work the recipient has not been asked to do.

For another kind of project or recipient, use the same principle: retain the verified details needed for their next action and omit unrelated internals.

## Present inline

Write the hand-off directly in the conversation for the user to send. Scale the structure to the content: short prose for simple work, compact tables or examples for contracts where useful. Make it understandable without the original chat.

Do not send messages, create tasks, update external records or write hand-off files as part of this skill. Preparing the material does not authorise delivery to the recipient.
