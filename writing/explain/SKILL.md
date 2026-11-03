---
name: explain
description: Explain a specific concept on demand or explain the agent's approach inline, using succinct reasoning, relevant tradeoffs and short examples or diagrams where useful. Avoid overwhelming the reader; persistent documentation belongs to Document.
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
- Choose the detail that answers the actual question. Avoid exhaustive background, code walkthroughs, repeated summaries and lists of every possible alternative.
- Make connections explicit so concision does not become dense prose that requires rereading.
- Link relevant code or sources when helpful, while keeping the essential explanation understandable without opening them.

Adapt to follow-up questions rather than anticipating every possible question in the first answer. Be candid about uncertainty or a material limitation. Explain decisions and useful reasons without narrating every exploratory step.

## Keep the output inline

Do not create persistent files merely because an explanation was requested. Use Document when the user asks for persistent documentation; its repository source is [../document/SKILL.md](../document/SKILL.md), and installed agents may need it installed separately. Explaining an approach does not authorise implementing it.
