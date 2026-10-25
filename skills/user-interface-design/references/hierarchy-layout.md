# Hierarchy and layout

## Decide what users need to notice

Use representative content to identify the primary task, primary data, and
supporting context. A page heading need not be its largest element. Keep heading
semantics meaningful while styling each heading for its visual role.

Use size, weight, and contrast together without making every important item
large, bold, and dark. Try reducing competing content before increasing the
primary element. Keep supporting text readable, not merely faint.

Displayed values often need less labeling than a database record: an email
address may explain itself, and “3 bedrooms” may read better than “Bedrooms: 3”.
A specification sheet is different: users scan for “Battery” or “Weight”, so
labels can carry more weight. Do not apply label removal to form inputs.

Give one action clear priority within the active task. Secondary actions can use
restrained fills or outlines; tertiary actions can use text treatment with a
discoverable affordance. A destructive action need not dominate a page. Explain
its consequence and use stronger treatment at confirmation if needed.

Use labels, dividers, numbering, and alignment to express actual relationships.
Number items when order matters, such as steps in a process; do not imply a
sequence merely to decorate unrelated features.

## Space communicates relationships

Default to generous space, then tighten where it improves the task. Keep gaps
within groups smaller than gaps between groups. A heading belongs closer to the
content below it than to the preceding section.

When no spacing scale exists, start with useful steps such as `4, 8, 12, 16, 24,
32, 48, 64, 96px`. Compare adjacent tokens rather than incrementing by an
arbitrary pixel. Extend the scale when a wider layout needs it; do not define a
large token library for a single adjustment.

Dense data areas can coexist with generous page-level spacing. Reduce row
padding and redundant content before shrinking text or controls. Preserve
alignment and group separation so density does not flatten hierarchy.

For example, a customer onboarding form benefits from clear section spacing and
a constrained column. An analyst's comparison table may need compact rows to
keep more records visible. Both still need legible text and stronger gaps
between unrelated groups; neither layout is a template for the other.

## Width and responsiveness

Size the feature before designing the frame around it. A full-width header does
not require full-width inputs. Paragraphs, forms, and tables can use different
widths on the same page.

Use fixed or capped widths for elements whose content does not need to scale,
such as a navigation rail. Let the main content flex. A maximum width with
shrink-to-fit behavior is often simpler than changing grid spans at every
breakpoint. Use grids when they clarify relationships, not as a requirement.

Across available sizes, compress large headings and gaps more than already-small
body text. Choose behavior from content pressure rather than device labels. For
a component used in multiple contexts, design for the space its container
provides, not just the viewport. Specify what reflows or changes priority; leave
breakpoint and container-query mechanics to implementation guidance. Check
narrow screens, long labels, zoom, and overflow; avoid clipping necessary
actions or information. For wide tables, preserve meaningful columns and use an
accessible overflow strategy or a task-appropriate alternate presentation.
