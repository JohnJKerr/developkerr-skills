---
name: document
description: Create or update persistent, succinct concept documentation that a user or agent can understand without reading the code. Default to the target project's docs folder and use diagrams or examples when they aid explanation. On-demand explanations belong to Explain instead.
---

# Document

Write a persistent explanation that lets a user or agent understand the concept without opening the implementation. Keep it self-contained and succinct: enough to understand and use the concept, without overloading the reader.

## Establish the subject and destination

Use the request and available context to identify the concept, intended audience and questions the document needs to answer. Ask only when a material ambiguity cannot be resolved from that context.

Default to Markdown in the target project's `/docs` folder, relative to its repository root. Respect an explicitly requested destination. Look for existing relevant documents before creating one; update the appropriate document rather than duplicating the explanation. Preserve unrelated content and useful links.

## Ground the explanation

Read the relevant implementation, tests, existing documentation and decisions to establish what is true. Inspect purposefully rather than reading the entire codebase. Resolve material contradictions or identify uncertainty instead of guessing.

Distinguish current behaviour from planned or proposed behaviour. Do not invent reasons for a design decision when the evidence establishes only what was implemented. Never include secrets or private data in examples.

## Explain the concept

Lead with what the concept is and why it matters. Then explain the behaviour, relationships, decisions and constraints the reader needs. Choose the structure to fit the subject; do not force every document through the same list of sections.

- Use the project's domain language and define unfamiliar terms where needed.
- Make prerequisites and important rules explicit without requiring the reader to trace code or read the original conversation.
- Prefer concrete, short examples over abstract repetition. Use a diagram when it explains a relationship or flow more clearly or briefly than prose.
- Include implementation details only when they are necessary to understand or use the concept. References to code can support the explanation, but must not replace it.
- Link related documents for additional depth while keeping the core explanation understandable on its own.

Avoid code walkthroughs, exhaustive inventories, unnecessary background and repetition. Succinctness means choosing the information that matters, not compressing everything into dense prose or omitting a consequential rule. Use plain language and short, connected explanations.

## Review and deliver

Read the document as someone who has not seen the code or conversation. Can they understand the concept, its important behaviour and its boundaries? Remove detail that does not help answer those questions.

Check factual claims, examples and links against the available sources. Review diagrams for accuracy and render them when supported and useful. Disclose material uncertainty rather than implying checks were performed when they were not. A qualitative review is sufficient when automated validation would add no value.

Save the document in the agreed location and briefly report what was documented with a link to the file. This skill creates persistent documentation; use Explain for an on-demand explanation of a concept or the agent's approach. Do not create persistent files merely because an inline explanation was requested.
