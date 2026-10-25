---
name: visual-design
description: "Develop, compare, apply, and critique visual direction for websites and app surfaces. Use when establishing or changing art direction, visual identity, or expressive composition; evaluating visual references; or designing a landing page or portfolio with an unresolved visual direction. Can explore direction without implementing it. Skip routine usability fixes and implementation work inside an agreed design, and software architecture unrelated to visual work."
---

# Visual design

Develop a visual language that fits the subject, audience, content, and use
scene. Make the direction concrete enough to discuss or build. Distinctiveness
should come from those constraints, not from adding fashionable effects or
avoiding anything familiar.

## Ownership and companions

Own art direction: composition, type character, palette character, imagery,
materials, and the expressive role of motion. Do not choose frameworks, storage,
routing, animation libraries, or dependencies as part of a visual proposal.

Load companions from the available skills list and read their `SKILL.md` when
their concerns apply. If unlisted, resolve the fallback relative to this skill:

- **`user-interface-design`** (`../user-interface-design/SKILL.md`): when the
  work specifies or changes an interface's hierarchy, navigation, controls,
  interaction expectations, states, or accessibility. It owns usability and UI
  fundamentals, including legibility, functional color roles, and recovery.
- **`frontend-development`** (`../frontend-development/SKILL.md`): when building
  or reviewing the implementation. It owns components, styling mechanics,
  events, runtime motion, performance, and browser resource lifetimes.

A comparison of references or a visual-direction discussion need not load
implementation guidance. A runtime-only fix or local usability adjustment need
not reopen visual direction. If a required companion is unavailable, ask for its
location and continue independent work.

## Establish what may change

Read applicable project instructions and `DESIGN.md` before proposing a change.
Look at the repository root, target app or package, then `docs/DESIGN.md` or
`.design/DESIGN.md`; follow instructions to a shared brand owner. Read root and
scoped guidance when both apply and surface conflicts affecting this surface.

Use documented intent as authority and representative rendered surfaces,
components, tokens, and assets as evidence of the incumbent identity. Missing
`DESIGN.md` does not make an existing product a blank canvas. If documented
intent and implementation differ, identify the relevant mismatch without
reconciling unrelated drift.

Distinguish the scope from the request:

- **Refine or extend:** preserve the identity and settled composition; resolve
  only what the requested surface needs. A new screen inside a product normally
  inherits its visual system.
- **Expand:** preserve confirmed assets and recognizable traits while proposing
  missing treatments. Show which choices extend the system.
- **Replace:** develop a new visual language only when the user authorizes it.
  Preserve product truth, function, factual copy, and commitments not explicitly
  in scope. Identify proposed departures from documented intent.

Ask if preservation versus replacement changes the result and cannot be
inferred. Do not silently edit `DESIGN.md`, invent another source of truth, or
require a new context document. Save decisions only when requested, at their
owning scope.

## Ground the direction

Inspect supplied material before asking for more. Identify the facts that shape
this surface:

- The subject and its specific mechanism, content, or artifact.
- Who encounters it, where, and what they need to understand or do.
- The real assets, evidence, content ranges, and brand commitments available.
- What remains open, what must stay, and what would make the result
  inappropriate.

Different surfaces of one product can need different expression:

| Visitor's purpose                                       | Design emphasis                                                                            |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Decide and act: a campaign, pricing page, or launch     | Clear proposition, credible evidence, attention, and a meaningful next action              |
| Complete work: an editor, dashboard, or settings screen | Scanability, predictable controls, density suited to the task; identity in precise details |
| Understand: documentation, an article, or a guide       | Reading rhythm, structure, useful wayfinding, and clarity                                  |
| Engage with the work: a portfolio or gallery            | The artifact leads; the surrounding interface supports discovery                           |

These are lenses for the surface, not agent modes or required labels. A tool's
landing page and editor need not share the same composition or motion intensity.

Separate supplied facts, inspected evidence, and hypotheses. Reference sites
show possible treatments, not proof that those treatments improve user outcomes.
Ask only for gaps that materially change the direction, scope, or asset needs.

## Make a proposal concrete

For an open direction, bring a grounded recommendation and the closest
meaningful alternative when one exists. Compare a real trade-off, such as
artifact-led versus narrative-led composition, rather than recoloring the same
template. Do not manufacture alternatives for a precise brief or settled local
adjustment.

Use the smallest useful description, sketch, or representative composition to
make the proposal assessable. Address the choices that distinguish it:

- **Composition:** what leads, the reading or exploration path, the focal point,
  and how sections or states relate. Let different content jobs earn different
  layouts; repeat a pattern when repetition makes comparison easier.
- **Typography:** the character and role of the type, not just a font name. Test
  long and short real headings; distinctive display type need not become the
  face of small controls or body copy.
- **Palette and materials:** what color temperature, contrast, surface
  treatment, and depth express. Keep functional roles and legibility under UI
  guidance.
- **Imagery:** what the media demonstrates, its source, crop, and missing
  assets. Prefer product-specific material to interchangeable stock. Text-led
  work can be complete when text carries the subject.
- **Motion:** what it communicates or lets the visitor experience. Choose
  expression independently of density and layout experimentation; an expressive
  composition can be still. Leave gesture behavior to UI guidance and mechanics
  to frontend guidance.

Use references to explain a transferable principle: what fits, what does not,
and how the current content changes the treatment. Do not copy a competitor's
layout wholesale or reduce direction to labels such as "premium" or "modern."

For example, a ceramics portfolio might lead with close-up material photography,
quiet captions, and a spacious sequence that reveals a collection. A type
specimen portfolio might lead with live text and a compact comparison grid. Both
let the work lead; neither needs the other's imagery, density, or motion. The
medium and browsing task explain the difference, not a universal hero rule.

State why the recommendation fits and its main cost: asset production, reading
speed, implementation complexity, or loss of familiarity. Mark settled choices,
tentative choices, and material open questions without imposing a phase
template.

A direction discussion does not authorize implementation. Do not write source,
produce a full prototype, generate assets, or save a design note merely to make
a proposal feel complete. When building is requested, carry the chosen direction
through implementation and verification; do not ask the user to reconfirm
routine details already specified.

## Apply and critique the direction

Evaluate common patterns as choices, not prohibited shapes. Cards, centered
heroes, gradients, system fonts, serif type, and familiar palettes can fit a
brief. Ask whether they carry this content or substitute for understanding it.
Do not ban colors, fonts, punctuation, or layouts merely because models often
use them. Do not replace one generic template with a mandatory novelty template.

Keep these checks tied to the requested surface:

- Does the result express the chosen direction through composition and content,
  or only through a decorative skin?
- What makes it specific to this subject? Would changing the name and accent
  leave an equally plausible page for any competitor?
- Does the emphasis match the visitor's purpose? Do ornament or effects compete
  with evidence, reading, or repeated work?
- Are repeated sections useful repetition, or evidence that one layout was
  applied regardless of each section's job?
- Do imagery and copy carry supplied truth? Do not fabricate testimonials,
  customer logos, metrics, availability, or product screenshots. Label sample
  content and distinguish a concept illustration from a real product capture.
- Does the identity survive narrow layouts, long content, and required states?
  Do not preserve a dramatic desktop crop at the cost of essential content.
- Can the proposed media or effects actually be delivered within scope? Identify
  unavailable assets, permissions, tool capabilities, or performance constraints
  instead of claiming completion from placeholders.

For implementation, inspect the rendered target and relevant changed states at
representative sizes. Batch related observations, fix supported defects, and
recheck affected behavior. Stop when the brief and agreed direction hold; do not
churn through variants or unrelated polish. If rendering is unavailable, report
that limit and separate source findings from unverified visual judgments.

For critique, connect each material concern to an observable element, its
effect, and a concrete correction. Distinguish usability failures from aesthetic
trade-offs. Do not score subjective taste as measured quality or treat an agent
walkthrough as user research.

## Sources

[Sources and adaptation boundaries](references/sources.md) records optional
background for maintaining this skill. It is not required reading for a design
request; the guidance above must remain usable without upstream tools or files.
