# Typography

## Establish a usable scale

Use an approximately modular scale, tuned to useful sizes instead of enforcing
an exact mathematical ratio. Default to `12, 14, 16, 18, 20, 24, 30, 36px`
(or their `rem` equivalents). Add larger display sizes only when needed.
Project typography overrides these starting values.

Prefer `rem` for text so user font settings can affect it. Avoid nested `em`
font-size rules that compound into different sizes across components. Validate
text resizing rather than treating a unit choice as proof of accessibility.

Use no more than two font families, often one with multiple weights. Use a
neutral, legible sans-serif for ordinary UI unless project intent calls for
another direction. A system stack avoids introducing a webfont dependency.
Evaluate body fonts at actual UI sizes, including numbers and ambiguous glyphs;
a striking headline face may be unsuitable for small controls.

Body text usually works at weight 400–500; emphasis at 600–700. Avoid very thin
small text. Combine weight with contrast before creating extreme size gaps.

## Match line-height and measure

Keep paragraphs around 45–75 characters per line. Wider images or tables need
not stretch neighboring paragraphs. Start body line-height at 1.5–1.75 and
heading line-height at 1–1.25; adjust for the font, size, and measure. Wider or
smaller text may need more leading.

Align mixed-size text on a shared baseline. Left-align long text in left-to-right
interfaces; follow the language direction elsewhere. Reserve centered text for
short, independent blocks. Right-align numeric table columns and use tabular
numerals when available to make comparison easier.

Leave letter-spacing alone by default. Add modest tracking to all-caps labels;
consider tighter tracking for large headings if the face needs it. Do not use
tracking to rescue an illegible font at small sizes.

## Keep meaning and affordances

Use semantic heading levels for document structure, not to obtain a font size.
Style a quiet page heading without changing its semantic role.

In link-heavy navigation, use weight, contrast, and active treatment rather
than coloring everything. Inline prose links need a persistent non-color cue,
such as an underline. Hover and focus may strengthen an affordance, but must
not be the only way users discover a necessary action.

Truncate only when the full value remains available through a usable mechanism,
including keyboard and touch where relevant. Let errors, critical information,
and ordinary body text wrap. Test long and localized content rather than relying
on the example string's length.
