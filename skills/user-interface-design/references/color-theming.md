# Color and theming

Use documented colors as supplied. This guidance applies when choosing missing
roles or creating a palette, not as permission to replace a project's system or
convert its notation.

## Construct a palette around usage

Define a constrained set of shades, then select from it across components.
Avoid generating slightly different variants independently at each call site.

1. Choose a base shade in context, such as a primary button with its text.
2. Choose a dark endpoint for colored text and a light endpoint for a tinted
   surface. An alert provides a useful fixture for testing both.
3. Fill intermediate shades by comparing neighboring steps. Five to nine shades
   per color is a useful starting range, not a quota.
4. Check actual uses, adjust the set, and give recurring roles semantic names:
   primary action, muted text, surface, border, danger, warning, and success.

Use a neutral range broad enough for backgrounds, text, and controls. Subtle
warm or cool tinting can support personality. Introduce accent ranges for real
states or categorical data, rather than designing every possible color upfront.

## Saturation is a contextual choice

HSL makes hue, saturation, and lightness easy to manipulate, but its lightness
is not perceived brightness and equal steps do not look equally different.
Neither “always lower saturation when lightening” nor “always increase it” is
a universal palette rule.

For vivid HSL palettes, raising saturation toward light or dark extremes can
help avoid washed-out shades. At fixed saturation, the RGB channel spread
shrinks toward black and white; at either endpoint it becomes zero regardless
of saturation. Increasing saturation cannot preserve all vividness there.
For muted tints, lowering saturation may instead serve the intended role.
Tune saturation alongside lightness and, where appropriate, a small hue shift.

OKLCH offers more perceptually consistent controls when creating a new scale,
but chroma is not HSL saturation, and available gamut still limits the result.
Use the project's color space; do not translate an HSL rule into an OKLCH
chroma rule or mandate migration.

Compare shades on their intended backgrounds. Numerical interpolation can
produce candidates; rendered context and measured contrast determine whether
they work. A hue shift may improve contrast, but it guarantees no particular
ratio. Palette labels such as “500” do not guarantee accessible button text.

## Assign color without overpowering hierarchy

Use a restrained set of text roles. On a colored surface, a same-hue supporting
color often looks more intentional than neutral grey or translucent white.
Choose the foreground/background pair and measure it; do not lower contrast
below the requirement to achieve a visual effect.

For secondary status surfaces, dark text on a light tint often carries meaning
without competing with the primary action. Include words, icons, or patterns
alongside color when it communicates status or category.

## Dark mode is a separate role mapping

Preserve the intended hierarchy instead of inverting every color. Map semantic
roles to dark-mode values so components keep their roles without per-component
exceptions.

- Start with dark neutral surfaces and off-white text; tune the contrast rather
  than assuming pure black or white is always wrong.
- Use surface lightness and restrained boundaries for elevation when shadows
  are hard to see.
- Check accents against dark surfaces and button text against accent fills.
  A lighter accent suited to text may not suit a filled button with white text.
- Test focus, errors, disabled controls, charts, and media in each supported
  theme. Do not dim user content or invert diagrams indiscriminately.
- When a theme choice exists, make it understandable and preserve the user's
  selection. Respect system preference according to the project's contract.

Use measured text and non-text contrast, not “looks muted enough”, as the
accessibility criterion. See [Interaction and accessibility](interaction-accessibility.md)
for checks.
