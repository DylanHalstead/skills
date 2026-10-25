# Depth, media, and finish

## Keep personality coherent

Use the documented radius treatment. Where it is unspecified, square corners
support a formal direction, modest rounding a neutral direction, and stronger
rounding a playful direction. Carry that choice across comparable components
rather than alternating square and rounded treatments by whim.

Nested shapes need a smaller inner radius so the gap looks even. Functional
shapes, such as circular avatars, do not require every container to be circular.
Resolve a proposed personality change with the user before applying it broadly.

## Elevation describes relationships

Choose the layer's role before its shadow. A resting button or card may need a
small shadow, a floating menu more separation, and a modal the strongest
separation. A flat design may need no shadows at all.

Use a small constrained set of elevation treatments. Two-part shadows can
combine a soft cast shadow with a tighter contact shadow; reduce contact
strength as apparent height increases. On press, a raised control can flatten;
during a drag, the item can rise. Preserve legible boundaries without motion.

When using raised or inset cues, keep the apparent light direction consistent. A
restrained highlight and shadow can indicate depth without photorealism. Avoid
giving every region the same floating treatment.

Use space or background changes to separate groups before adding borders.
Borders remain useful for precise table structure, inputs, high-contrast modes,
and surfaces where another treatment would fail. Do not remove them merely to
satisfy a border-free aesthetic.

## Design with real media constraints

Use representative photos and content rather than assuming a placeholder will
match the final asset. If assets are unavailable, show the dependency and use a
layout that tolerates realistic variation.

For text over an image, check the region behind the text across crops and
responsive sizes. A background overlay, separate text surface, or image
treatment can stabilize contrast. A text shadow alone does not prove contrast.

Use consistent icon style and intended optical sizes. If a small glyph looks
poor at a large size, choose a suitable asset or keep it small within a larger
shape. Crop or simplify screenshots rather than shrinking their content into
unreadable text.

Constrain user uploads to appropriate frames without distortion. Preserve the
image's meaning when cropping matters. Provide fallbacks and meaningful
alternative text where needed; a subtle inner boundary can keep light media
visible on a light surface.

## Finish only what serves the feature

Use a restrained accent or background treatment when hierarchy already works. Do
not add regions, illustrations, or custom controls merely to make the screen
feel designed. Prefer native or installed accessible controls; a brand-colored
selection state need not require a new widget.

Empty states should explain whether the user has no records, no matching
results, or lacks access. Offer the action that applies: create something,
adjust filters, or request access. Preserve search and filter controls when they
help recover from no results. Hide only controls that have no useful function in
that state.
