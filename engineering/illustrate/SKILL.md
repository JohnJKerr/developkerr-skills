---
name: illustrate
description: Sketch a Miro-style ASCII system diagram of a changeset, a planned implementation or the whole project, showing data flow, what changed and short attached notes so readers can avoid long text. Use for "/illustrate the changes", "/illustrate the plan" or "/illustrate the project"; Pull Request uses it for the PR's at-a-glance diagram. Not UML, not image generation.
---

# Illustrate

Draw a quick sketch that lets someone understand a system or change at a glance, without reading much text. Aim for a whiteboard or Miro sketch: boxes, labelled arrows and short sticky notes. Avoid formal notation such as UML. The picture should carry the meaning. Keep the surrounding text to a title, a legend and at most a sentence or two.

## Choose the scope

Work out the scope from the request:

- **The changes:** what a changeset adds, changes or removes, and how data now flows through the affected parts. Use the diff against the intended base, which is usually the default branch, plus any uncommitted work. If the base is unclear, use the default branch and say so.
- **The plan:** the intended implementation. Use the plan agreed in the conversation, or a plan file the user points to. Show it as proposed, not built.
- **The project:** an overview of the whole system. Use the repository structure, entry points, configuration, data stores, external services and existing docs.

If the scope is genuinely ambiguous, for example there's no plan in context and no changes either, ask one short question. Otherwise infer it.

## Ground the sketch

Read enough code, diff or plan to know what actually talks to what, and what flows between them. Focus on what the reader needs, not on reading everything. Every box, arrow and note must be supported by the evidence. Mark anything inferred or unknown with `?` rather than drawing it as fact. For a changeset, include unchanged components only when they give the reader context: where data comes from, or where it ends up.

## Draw it

Put each sketch in a fenced code block (marked `text`) so it renders in monospace in terminals, chat and GitHub.

- **Components:** draw each component as a box named in the project's own terms, such as `Account (aggregate)`, `POST /licences`, `orders queue` or `MongoDB`. Draw a datastore with round ends, `( MongoDB )`, and an actor or external system as a plain label or a box. Show a component, not every file or class behind it.
- **Data flow:** use arrows (`──▶`, `◀──`, `│`, `▼`). Label each arrow with what travels along it, such as a request, command, event, query or data shape, and where it helps, a key field. Number the steps (`1`, `2`, `3`…) when their order matters.
- **Main path:** lay the primary flow in one direction, left to right or top to bottom. Keep secondary paths short and out of its way, and keep crossing lines to a minimum.
- **Notes:** draw each note as a small rounded box (`╭─╮ ╰─╯`) joined to its subject by a dotted line (`┄┄`). A note says *why* something exists, *what matters* or *what to watch*: an invariant, a failure case, a compatibility risk or a decision. Keep each note to a few words or one short line. Use notes sparingly. If everything is annotated, nothing stands out.
- **Change markers:** in "the changes" sketches, tag each affected component or arrow next to it:
  - `+ NEW` for something added.
  - `~ CHANGED` for something whose behaviour or contract changed.
  - `- REMOVED` for something removed. Strike it through with `╳`, or drop it and add a note if that reads better.
  - Leave unchanged context untagged, and draw it as minimally as you can.
- **Plan markers:** in "the plan" sketches, use `PLANNED` for things the plan adds and `?` for open decisions.
- **Legend:** add a one-line legend under the sketch for whichever markers you used.

### Layout rules

- **Width:** keep each sketch within about 100 columns so it doesn't wrap in a PR or terminal.
- **Characters:** box-drawing characters and plain ASCII only. No emoji, CJK text or other double-width characters inside the block, because they break alignment.
- **Alignment:** make every box edge and arrow line up. Re-read the block line by line before you present it, and fix any ragged corners or misaligned connectors.
- **Big scopes:** if one sketch would be cramped, draw one **overview** sketch, then up to three **zoom-ins** on the busiest or riskiest areas. Give each one a short heading. Drop detail rather than squeezing it in.

## Example

A changeset that adds licence allocation:

```text
                    1 POST /accounts/{id}/licences
  ┌────────────┐          { userId }          ┌──────────────────────┐
  │  Admin UI  │ ───────────────────────────▶ │ AllocateLicence      │ + NEW
  └────────────┘ ◀─────────────────────────── │ handler              │
                   201 / 409 SeatsExhausted   └──────────┬───────────┘
                                                         │ 2 allocate(userId)
                                                         ▼
   ╭─────────────────────────╮                ┌──────────────────────┐
   │ rejects when no seats   │┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄│ Account (aggregate)  │ ~ CHANGED
   │ left; no partial writes │                └──────────┬───────────┘
   ╰─────────────────────────╯                           │ 3 save(account)
                                                         ▼
                                              ( MongoDB: accounts )
                                                ~ new `licences` array

  + NEW   ~ CHANGED   - REMOVED   ┄ note
```

Licences live on the account rather than in a separate collection, which keeps the seat check atomic.

## Output

Present the sketch or sketches inline with:

1. A one-line title naming the scope, such as "Changes: licence allocation".
2. The sketch or sketches.
3. The legend.
4. At most one or two sentences on anything the picture can't show, such as a key decision or an important uncertainty.

Don't write files unless the user asks. For persistent documentation, use Document, which can include the sketch. When Pull Request calls this skill, return the sketch for its description rather than presenting it separately.

## Boundaries

Illustrate draws pictures. It does not:

- Review code quality (Code Review).
- Write prose documentation (Document).
- Explain concepts in depth (Explain).
- Change code or plans.

Never draw something the evidence doesn't support just to make the picture tidier.
