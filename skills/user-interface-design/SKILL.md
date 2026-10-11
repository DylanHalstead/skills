---
name: user-interface-design
description: "Design, refine, and review user interfaces through feature-first layout, visual hierarchy, and constrained design systems. Use for new screens or components, UI design discussions, visual polish, spacing, typography, palettes, themes, empty states, forms, tables, and dashboards. Skip frontend plumbing without a UI design concern and software architecture unrelated to interfaces."
---

# User interface design

Start with what the user needs to do and see. Establish hierarchy and grouping
before choosing decorative details. Use this guidance for design discussions,
implementation, and review.

Own visual and interaction decisions: what users see, understand, can do, and
can recover from. Specify observable behavior without prescribing state storage,
router APIs, event handling, hydration, or framework architecture. Those belong
to frontend-development guidance. A runtime-only fix with an agreed interface
does not require reopening its design.

## Project intent: DESIGN.md

Before UI work, find and read the applicable `DESIGN.md` in full. Look at the
repository root, the target app or package, and then `docs/DESIGN.md` or
`.design/DESIGN.md`. Follow project instructions to a shared or brand package
when it owns design intent for the surface. Read root and scoped guidance when
both exist; use explicit scope to resolve overrides. Ask about conflicting
requirements that affect the requested surface.

Treat `DESIGN.md` as the source of truth for the product's design: palette,
typography, spacing, components, radius, elevation, personality, and copy tone.
Its decisions override this skill's defaults. Do not swap them for preferred
styles or silently revise the document. Safety, accessibility, and explicit user
authorization still apply; surface a conflict rather than implementing an unsafe
requirement.

Read existing components to understand how to work on the requested surface,
not to redefine design intent. Do not audit Tailwind classes or tokens against
`DESIGN.md` unless asked. If a mismatch encountered during the work affects the
result, mention it briefly and use the documented intent for the requested
change. Do not reconcile unrelated drift or create a second design system.

If no `DESIGN.md` exists, use established project conventions before these
defaults. Do not require a new document or write one without authorization.

## Work through the design

Use this order to reason about new UI. For a focused adjustment or review,
start at the relevant concern and leave settled decisions alone. These are not
mandatory phases, approval gates, or an execution-plan template.

1. **Start with a feature.** Identify the real content, primary task, and useful
   action. Design that surface before inventing navigation, sidebars, or a page
   frame. In an existing app, work within its shell unless changing it is in scope.
2. **Make the proposal concrete.** Use representative content and a low-fidelity
   sketch or interface example. Resolve layout and hierarchy in grayscale before
   investing in color, shadows, or icons. A small request may need only a local
   comparison, not a whole-screen sketch.
3. **Keep the version useful and small.** Include the states needed for the
   agreed feature. Omit speculative controls and implied functionality that will
   not work. Design the empty state with the populated state.
4. **Apply a coherent system.** Reuse documented scales and components. Where
   guidance is missing, establish only the tokens needed for this surface. Refine
   hierarchy, grouping, type, color, and elevation where they affect the task;
   load supporting references only for those concerns.
5. **Check the result.** Review the applicable criteria below. Check the rendered
   result and changed interactions when implementing a surface.

## Design defaults

Use these when project intent leaves a gap.

### Hierarchy and layout

- Give the primary content and action more visual weight than supporting content.
  First reduce competitors; then adjust size, weight, or contrast as needed.
- Use labels when they clarify meaning. Omit redundant labels on displayed data;
  retain visible labels for form inputs. Emphasize labels when users scan for
  categories, such as a specification sheet.
- Default to generous space around groups. Use tighter spacing within a group.
  Deliberate density is appropriate for comparing or acting on many records;
  preserve readable text, clear grouping, and usable controls.
- Give elements the width their content needs. Constrain paragraphs to about
  45–75 characters, rather than stretching them to match wide tables or images.
- Start from constrained spacing and sizing scales. Prefer existing tokens to
  introducing one-off values.

### Type, color, and personality

- Use an approximately modular, hand-tuned type scale:
  `12, 14, 16, 18, 20, 24, 30, 36px`, expressed in `rem` where practical.
  Extend it only for a real need.
  Limit the UI to two font families; use 400–500 for body and 600–700 for emphasis.
- Use tighter line-height for headings (about 1–1.25) and more relaxed line-height
  for body text (about 1.5–1.75), adjusted for font and line length.
- Define a fixed palette before assigning shades across components. Tune it in
  context rather than deriving new shades independently at each call site.
- Keep font choice, corner radius, color temperature, and copy tone consistent
  with the product's personality. Without documented intent, infer from the
  product; ask before committing to a materially different direction.
- Use square corners for a formal direction, modest rounding for a neutral one,
  or stronger rounding for a playful one. Do not mix square and rounded component
  treatments without a documented reason. Keep nested inner radii smaller than
  outer radii; preserve functional shapes such as circular avatars.

### Interaction and language

- Use the user's vocabulary. Name actions by their outcome and keep those names
  consistent across controls, confirmations, and feedback. Errors explain what
  happened and what the user can do next.
- Make recovery part of the feature: decide what work survives failures and
  navigation, how users resume, and which consequential actions need confirmation
  or undo. Choose behavior from risk and reversibility, not a universal dialog rule.
- Identify views users need to share, return to, or revisit through browser
  history. Specify what should be restored without choosing a routing mechanism.

### Depth, states, and accessibility

- Use shadows to express elevation, not to decorate every box. Prefer grouping,
  background changes, or restrained depth over unnecessary borders.
- Account for empty, loading, error, disabled, and interaction states when the
  feature can enter them. Empty states explain what is missing and offer a useful
  action when one exists; not every empty state needs an illustration or CTA.
- Preserve semantic structure, visible form labels, keyboard operation, and
  visible focus. Do not rely on color, hover, or motion alone to convey meaning.
- Check actual foreground/background pairs: normal text needs at least 4.5:1;
  large text needs 3:1 (24 CSS px regular or about 18.67 CSS px bold). Required
  visual cues identifying controls and states need 3:1 against adjacent colors.
- Do not de-emphasize pricing, terms, warnings, or cancellation paths in ways
  that obscure important information. Hierarchy must not undermine comprehension.

## Supporting references

Read only the references needed for the request. Paths are relative to this
skill's directory; use the available file-reading tool.

| Condition | Reference |
| --- | --- |
| Competing content, grouping, width, responsive layout, or density | [Hierarchy and layout](references/hierarchy-layout.md) |
| Font selection, type scale, alignment, line-height, or text treatment | [Typography](references/typography.md) |
| Creating a palette, choosing color roles, or designing dark mode | [Color and theming](references/color-theming.md) |
| Elevation, images, icons, corner treatment, or visual finish | [Depth, media, and finish](references/depth-media-finish.md) |
| Action wording, forms, recovery, navigation behavior, gestures, motion, or accessibility checks | [Interaction and accessibility](references/interaction-accessibility.md) |
| Charts, data tables, or dashboard composition | [Data visualization](references/data-visualization.md) |

## Design checks

Check what applies to the requested surface:

- The proposal follows `DESIGN.md`, or established conventions when it is absent.
- The primary task and data remain clear without decorative color.
- Grouping and density support the task; text and controls remain usable.
- Type, spacing, radius, palette, and elevation follow coherent systems.
- Representative content and applicable empty/error/loading states fit.
- Action wording, recovery, and navigation behavior support the task without
  prescribing unrelated implementation choices.
- Semantics, contrast, keyboard focus, and responsive behavior support the user.

Source inspection alone does not establish rendered contrast, layout, or
interaction behavior.
