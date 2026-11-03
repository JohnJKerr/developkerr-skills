---
name: feature-map
description: Create or update persistent maps of proposed or existing features in the project's docs folder. Explain whole-feature user-facing behaviour, scope and system interactions without implementation details or delivery planning. Probe gaps and confirm scope before authoring.
---

# Feature Map

Map a whole feature so future users and agents can understand its behaviour and scope without reading code. Support both defining a proposed feature and documenting an existing one to build a discoverable collection of feature maps.

## Establish the subject

Determine the feature and whether the task concerns proposed behaviour, existing behaviour or an update to an existing map. Inspect relevant documentation first to avoid creating a competing description.

For a proposed feature, use the request and relevant product context to establish the intended behaviour. Probe missing requirements in small themed batches. Challenge contradictions and resolve consequential ambiguity rather than silently choosing requirements.

For an existing feature, inspect the available product, relevant implementation, tests and documentation purposefully. Reconstruct actual user-facing behaviour, including important failure paths and restrictions. Clarify material gaps or conflicting evidence with the user. Do not present inferred behaviour as established fact or silently turn current behaviour into a recommendation for a redesign.

Before authoring, summarise the understood scope and material open questions, and obtain the user's confirmation. Reuse explicit agreement already provided for the current map. Resolve gaps that prevent an accurate account; label remaining uncertainty rather than filling it with guesses.

## Describe the whole feature

Choose a concise structure suited to the feature. Cover the following where relevant:

- Users, goals and the capability the feature provides.
- Main user flows and the outcomes of user actions.
- Success and failure scenarios, including important restrictions.
- Front-end concerns and visible states such as loading, empty or error states where they matter.
- Permissions and who can see or perform relevant actions.
- Interactions with other systems and their user-visible consequences.
- Included scope, exclusions and unresolved questions.

Describe endpoint needs as capabilities required by the feature, such as allocating a licence or retrieving an account's available users. Keep HTTP routes, methods, DTO schemas, controller/handler designs and other technical contracts out of the map. Implementation details may inform the research but do not belong in this user-facing account.

Map the whole intended feature. Do not divide it into delivery slices, sequence implementation or create tasks; that belongs to task planning. Clearly distinguish proposed behaviour from existing behaviour when both appear, without converting the map into a delivery tracker.

## Persist and maintain

Write Markdown under the target project's `/docs` folder by default, respecting an explicit destination and existing documentation organisation. Use a meaningful feature-based filename and update an existing relevant map rather than duplicating it. Keep the collection discoverable through the project's existing documentation index or links; add a compact index when the collection needs one, not an elaborate documentation framework.

Apply the Document skill's succinct, self-contained writing principles. Its repository source is [../document/SKILL.md](../document/SKILL.md); installed agents may need it installed separately. Include enough to understand the feature without the source code or original chat. Diagrams and short examples are useful when they clarify or shorten the explanation. Avoid exhaustive background, technical walkthroughs and repeated information.

When asked to update a map as agreed behaviour changes, reconcile the relevant sections so the document remains coherent. Preserve unrelated content and useful references. Do not leave obsolete behaviour presented as current or imply an intended change has already been delivered.

## Review and deliver

Review the map from a future consumer's perspective: can they understand what the feature does, who it serves, its boundaries and important scenarios without opening the code? Check factual claims against the sources used, verify links and review diagrams where present. Identify material uncertainty and distinguish inspected behaviour from behaviour actually exercised.

Finish with a link to the saved map and a brief account of what was mapped and any unresolved questions. Do not implement the feature or create delivery tasks solely because a feature map was requested.
