# Interaction and accessibility

Define the user's experience and its observable guarantees. Leave storage,
routing, event handling, and framework APIs to implementation guidance.

## Words explain the interaction

Use terms the intended audience understands rather than internal system names.
Name actions by their outcome and carry that vocabulary through the flow:
“Publish edition” leads to “Edition published”, not an unrelated “Success”.
A generic label such as “Continue” is useful only when the next step is clear.

Explain failures with enough context to recover. Say what failed, whether the
user's work remains, and what they can do next. For example, “Could not publish
the edition. Your draft is saved. Try again.” is appropriate only if the product
can guarantee that the draft is saved. Do not promise persistence or successful
completion before the behavior supports it.

Keep copy consistent with the product's tone and terminology. Do not impose
universal capitalization, punctuation, or novelty requirements.

## Preserve control contracts

Use semantic elements and native or existing accessible components before
inventing custom widgets. Visual changes must preserve accessible names,
keyboard behavior, focus, and error feedback.

Keep visible labels on form inputs; placeholders are hints, not substitutes.
Associate errors and help text with the input. State required fields and
validation failures in words, not only a border color.

Avoid asking users to re-enter information already provided in the same flow
when it remains valid and safe to reuse. Allow paste, autofill, and password
manager assistance. Authentication should support memory aids or an alternative
to cognitive tests rather than requiring unaided recall or puzzle solving. Do
not invent a new authentication mechanism as part of visual refinement.

Distinguish hover, focus, active, disabled, and selected states. Necessary
actions must remain discoverable without hover. Ensure focus is visible and
not clipped or obscured. An icon-only control needs an accessible name.

For composite widgets such as tabs or menus, follow the established component's
keyboard contract. For modal dialogs, move focus into the dialog appropriately,
keep keyboard focus inside while modal, provide a way to close, and restore
focus to a meaningful location. Do not apply a modal focus trap to ordinary
non-modal content.

## Navigation and returning to a view

Distinguish actions that change data from navigation to another location.
Preserve normal link behaviors, including opening a destination in another tab.

Identify which view state users need to share, bookmark, reload, or revisit
with Back and Forward. Specify the relevant filters, page, selection, and return
position according to the task; do not require every transient state to persist.
Keep private or sensitive data out of a shareable location.

For example, a searchable directory may need a shareable filtered view and a
return path that restores the results after visiting a record. A temporary
confirmation dialog usually does not need a shareable location. The intended
return behavior matters; a particular URL format or state library does not
belong in the design proposal.

## Async and recovery states

Use the indicator that matches the operation: a spinner for an unknown short
wait, progress for measurable work, or a skeleton when the incoming layout is
known. Preserve enough context that users understand what is happening.

Make pending work clear and prevent duplicate submissions. Keep feedback
accessible and avoid unnecessary layout shifts or focus loss. Announce important
status changes without moving focus for every update.

Define what user-entered work survives validation errors, recoverable request
failures, and navigation. Preserve valid input and a useful retry path. Warn
before navigation when it would discard meaningful unsaved work, rather than
interrupting every departure. Do not promise recovery across reloads or devices
unless that guarantee is agreed and supported.

Choose confirmation or undo for consequential destructive actions according to
risk, reversibility, and the opportunity to recover. Avoid both silent,
irreversible loss and confirmation dialogs for every routine action.

Loading, no records, no matching results, and permission failures are distinct
states. Explain the state and offer an applicable next action. For partial success,
keep completed work visible and make failed or pending portions identifiable;
define whether retry affects only failed work. Do not present a mixed outcome
as total success or erase usable content because one region failed. Retain usable
cancellation for long operations where supported.

## Alternatives to gestures

For dragging and complex gestures, provide a usable click/tap alternative as
well as keyboard operation unless the gesture is essential. Keyboard support
alone does not serve pointer users who cannot perform the gesture.

For a reorderable list, moving an item up or down can provide an alternative to
dragging. Specify how users discover the alternative, understand the resulting
order, and retain their place; leave event and focus-management code to the
implementation.

## Motion

Animate to explain a state change, provide feedback, or preserve continuity.
Skip motion that adds delay to repetitive work. Short feedback often works
around 100–150ms, simple transitions around 150–250ms; tune to context instead
of enforcing a universal duration.

Respect reduced-motion preference. Preserve the same state information without
movement. Avoid flashing, compulsory parallax, and unrelated looping motion.
Let users interrupt or reverse an animated interaction when its action allows
that. Motion must not delay the next useful action. Specify the feedback and
continuity needed rather than prescribing CSS properties or animation libraries.

Give immediate visual press feedback while preserving normal activation and
cancel behavior; feedback on press does not mean committing an action on press.
During direct manipulation, keep the object aligned with the user's movement
and preserve where it was grabbed. On release, continuity and momentum can help
explain where it settles; bounce is not required for an ordinary menu or button.
An interrupted transition should continue from the visible position rather than
jumping to its old target. Reversible panels should retain a coherent relation
to their source and return path.

Distinguish interrupting presentation from canceling an operation. A user can
reverse a panel transition without resubmitting its form or undoing a server
write. Specify which controls remain available, including the non-gesture
alternative. Translucency is optional; if used, preserve legibility over real
backgrounds and provide a solid treatment when required by contrast or reduced
transparency. Leave velocity calculation, spring parameters, and pointer handling
to implementation guidance.

## Check beyond the screenshot

- Measure foreground/background contrast: 4.5:1 normal text, 3:1 large text
  (24 CSS px regular or about 18.67 CSS px bold). Use actual rendered colors,
  including transparency and background variation.
- Check required cues identifying controls or states at 3:1 against adjacent
  colors. Add a non-color cue for meaning conveyed by color.
- Navigate changed interactions with keyboard; verify order, focus visibility,
  activation, gesture alternatives, and escape/recovery behavior where applicable.
- Check applicable failure, retry, destructive-action, and return-to-view behavior
  against the agreed recovery and navigation guarantees.
- Verify semantic headings, accessible names, form labels, errors, and dynamic
  feedback. Informative images need text alternatives; decorative images should
  not add screen-reader noise.
- Test text resizing, zoom, narrow layouts, and long content for loss of
  information or functionality. Dense UI still needs usable pointer targets.
  For WCAG 2.2 AA, check the 24 CSS px target-size requirement or its permitted
  spacing/other exceptions; larger targets can improve touch use.
- Check supported themes and reduced-motion or forced-color modes when relevant.
  An automated checker can assist but cannot establish complete accessibility.

A source-only review can identify missing contracts, but cannot confirm rendered
contrast, layout, or assistive-technology behavior.

## Background

The direct-manipulation guidance adapts concepts from Emil Kowalski's
[`apple-design` skill](https://github.com/emilkowalski/skills/blob/2d228630ba1446365f614a108cb8252f1feda202/skills/apple-design/SKILL.md),
particularly press feedback, continuity, and interruptibility. These are optional
background, not a requirement to use Apple aesthetics or any spring library.
The [source license](../licenses/apple-design-MIT.txt) is retained.
