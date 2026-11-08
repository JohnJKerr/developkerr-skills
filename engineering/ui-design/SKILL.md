---
name: ui-design
description: Design or review websites and applications with deliberate visual choices, clear hierarchy and manageable content density. Use for layout, typography, colour, component appearance and interaction hierarchy; framework and component implementation conventions belong to front-end.
---

# UI Design

Create interfaces shaped by their content, audience and tasks. Avoid the recognisable combination of unchanged defaults, perfect symmetry and decoration used to fill space. Aim for a considered interface that users can understand and act on without feeling overwhelmed.

Apply this guidance when designing new interfaces and reviewing existing ones. The smells below are prompts for judgement, not prohibitions. A familiar pattern can be the right choice when it supports a task or an established brand. Do not replace a useful convention merely to appear different, or turn these preferences into another fixed template.

## Ground the design

Establish the audience, primary task, essential content and existing brand or design system from available context. Ask about material gaps; make modest assumptions explicit when they allow useful progress. For an existing interface, inspect the relevant screens and patterns before proposing changes. Preserve useful consistency and keep redesigns within the requested scope.

Choose typography, colour, layout and component treatment for reasons specific to the product. Briefly explain consequential choices in terms of content, readability, brand or user action. Personality can come from proportion, type, imagery, language or composition; it does not require novel controls, unusual navigation or more decoration.

Treat framework and component-library styles as starting points. Use the project's implementation conventions alongside this skill when building the design; this guidance does not prescribe a stack or authorise a migration.

## Control density and hierarchy

Decide what users need to understand or do first. Give that content and action clear priority; reduce competing headings, badges, metrics and calls to action. Use meaningful grouping, whitespace and a readable type scale to make relationships apparent.

Show essential information where it is needed. Move genuinely secondary detail into contextual or progressive disclosure without hiding information users need to compare, decide or complete a task. Avoid making every item a card: headings, lists, tables, dividers and unboxed content often express relationships more clearly.

Match density to the task. An operational table may need many visible records; a first-use screen may need very little. Reduce visual noise before removing useful data. Generous spacing should clarify grouping, not scatter related information across an unnecessarily long page.

Let content determine section structure and length. Keep alignment and spacing coherent without forcing identical section rhythms, equal-length copy, three-item groups or perfect symmetry. Do not impose asymmetry as a replacement formula.

## Use credible content

Write concrete labels and copy that explain actual behaviour, benefits and decisions. Do not fill a layout with generic claims. Never invent customers, company logos, testimonials, people, usage figures, uptime claims or other evidence. If sample content is necessary for a mockup, identify it as sample content and use plausible variation; do not pass it off as verified product data.

Represent chart data honestly. Preserve real variability, gaps and unfavourable outcomes. Choose charts, tables and metrics because they answer a user question, rather than to make a dashboard look complete.

## Check for formulaic defaults

Use this list when choosing a direction and reviewing the result. Look especially for clusters and repetition. A pattern's presence alone is not proof of poor design; assess whether it contributes meaning or merely repeats a default. Where a listed pattern is retained, have a concrete reason tied to the task or established visual language.

### Typography

- All-caps, letter-spaced eyebrows above every heading, such as “FEATURES” or “HOW IT WORKS”.
- Inter or Geist used everywhere without considering typographic character.
- One gradient word in a headline, or an italic serif accent word inside a sans headline.
- Oversized hero headlines followed by muted grey subheads as a default composition.
- Three-beat headings such as “Fast. Secure. Simple.”

Choose type for readability, hierarchy and the product's voice. Avoid trading legibility for personality or substituting another fashionable font automatically.

### Colour and surface

- Indigo-to-violet or purple-to-blue gradients.
- Blurred gradient orbs behind a hero.
- Glassmorphism cards with backdrop blur and white/10 borders.
- Faint grid or dot backgrounds with radial fades.
- Untouched Tailwind palettes, such as indigo-500 and slate-900.
- Dark mode with neon glows around borders and buttons.

Give colour and surface treatments a role in brand, grouping, emphasis or state. Use a coherent palette and sufficient contrast rather than a decorative effect on every surface.

### Layout

- A centred hero with a pill badge such as “✨ New: …”, followed by primary and ghost buttons.
- Three-column feature grids with rounded-square icons, titles and two-line descriptions.
- Bento grids used regardless of content relationships.
- Every section repeating eyebrow, H2, subhead and grid.
- Generic stats rows such as “10k+ users · 99.9% uptime · 24/7 support”.
- Logo clouds of nonexistent companies.
- Invented testimonials with initial-letter avatars.
- Three-tier pricing with the middle tier labelled “Most popular”.
- An automatic FAQ accordion followed by a four-column footer of dead links.

Include sections because they answer real questions. Pricing emphasis needs a basis in the offer; FAQs need actual questions; links need meaningful destinations. Omit unsupported content rather than filling template slots.

### Components

- The same large radius, such as rounded-2xl, on everything.
- Decorative Lucide icons such as Sparkles, Zap, Rocket and Shield.
- “✨” as shorthand for anything AI, or emoji as section icons.
- Cards with coloured left-border accents.
- Pill badges scattered throughout the interface.
- Hover-lift and shadows on every card, including noninteractive ones.
- An arrow “→” appended to every button.
- Gradient or animated shimmer borders.
- Pulsing green “live” status dots.
- shadcn/ui defaults left exactly as shipped.
- Cards nested inside cards.

Use shape, icons and emphasis consistently with their meaning. Interaction cues should correspond to actual behaviour; reserve badges and status indicators for information users need.

### Dashboards

- Automatic KPI card rows with green “+12.5%” trend arrows.
- Suspiciously smooth chart data.
- The default sidebar of icons and labels with an avatar pinned at the bottom.
- Every metric boxed in its own card.

Organise around monitoring, comparison or action needs. Explain metric context and whether a change is beneficial; a positive number is not always good. Choose navigation for the information architecture and group related metrics so users can understand them together.

### Motion

- Fade-up-on-scroll on every section.
- Staggered entrances on every grid item.

Use motion to clarify feedback, continuity or changes of state. Keep content readily available and respect reduced-motion preferences.

### Copy

- “Supercharge”, “seamless”, “unlock”, “elevate”, “effortless” and “everything you need to…”.
- Em dashes throughout.
- “Built for X, by Y”.
- Placeholder numbers that are conspicuously round.

Prefer specific, credible language and natural sentence rhythm. Do not replace round numbers with invented precise figures to create credibility.

## Review and deliver

For a review, identify the specific screen or element, explain its effect on comprehension or use, and recommend a practical change. Prioritise problems with task completion, hierarchy and density before cosmetic differences. Distinguish observed issues from assumptions; do not diagnose a rendered layout solely from class names.

For a new design, deliver the requested artifact and a short explanation of the main choices. Check the relevant responsive layouts, long or missing content, interaction states and accessibility where practical. Preserve legible text, contrast, keyboard access, visible focus, meaningful labels and usable targets as styling changes. Report what was actually inspected and any material limitations.

Finish by checking that the primary task is apparent, related content reads as a group, decoration earns its space, and the result fits this product rather than a generic showcase. Avoid claiming that removing these smells alone establishes good design.
