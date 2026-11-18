---
name: explain
description: Explain a specific concept, the agent's approach, or how something is currently implemented in the project, inline. Use succinct reasoning, relevant tradeoffs, short examples or diagrams, and code excerpts when recalling an implementation. Avoid overwhelming the reader; persistent documentation belongs to Document.
---

# Explain

Help the reader understand the requested concept or approach without overloading them. Answer inline and lead with the key point.

## Ground the explanation

Use the request and conversation to identify what needs explaining and the reader's likely familiarity. Ask only when a material ambiguity prevents a useful answer; do not make the reader complete a questionnaire before a straightforward explanation.

Inspect relevant code or context when the explanation concerns a particular implementation or decision. Distinguish established facts, assumptions and proposals. Do not invent a rationale for an existing design or imply that suggested work has already been implemented.

## Explain succinctly

State what the concept means or what approach is being taken, then provide the reasoning needed to understand it. For an approach, explain why it fits the problem and the tradeoffs or alternatives that materially affect the choice.

- Use plain language and the reader's domain terminology. Define unfamiliar terms only where needed.
- Prefer a short concrete example or diagram when it makes the explanation easier or shorter.
- Choose the detail that answers the actual question. Avoid exhaustive background, code walkthroughs (except when recalling an implementation, below), repeated summaries and lists of every possible alternative.
- Make connections explicit so concision does not become dense prose that requires rereading.
- Link relevant code or sources when helpful, while keeping the essential explanation understandable without opening them.

Adapt to follow-up questions rather than anticipating every possible question in the first answer. Be candid about uncertainty or a material limitation. Explain decisions and useful reasons without narrating every exploratory step.

## Recall an existing implementation

When the user asks how something is handled in the project, such as "how are we handling user licensing?", give a complete but succinct account of the current implementation, based on the code rather than the conversation:

- Trace each layer involved, such as endpoint, handler, domain rules, storage and front end, and say where the tests are.
- Include trimmed excerpts of the key logic, such as invariants, queries or contracts, each with a `file:line` link. Omit boilerplate and avoid whole files.
- Achieve completeness by covering every relevant part, not by adding commentary. Give rationale only where it is documented, for example in docs, commits or PRs.
- Note notable gaps or inconsistencies briefly; do not fix them.

## Keep the output inline

Do not create persistent files merely because an explanation was requested. Use Document when the user asks for persistent documentation; its repository source is [../document/SKILL.md](../document/SKILL.md), and installed agents may need it installed separately. Explaining an approach does not authorise implementing it.
