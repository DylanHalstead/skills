# Data visualization

## Choose a representation for the question

Use a number for a single important value, a table for exact lookup across
attributes, and a chart when spatial comparison makes the answer easier.

- Comparisons: bars, often horizontal for long category labels.
- Change over time: lines; use area only when its filled magnitude matters.
- Distribution: histogram or box plot.
- Relationship between variables: scatter plot.
- Parts of a whole: a simple stacked bar or a few labeled slices when proportion
  matters more than precise comparison.

Do not add a chart simply because a dashboard has space for one.

## Make comparisons honest

Start magnitude-encoding bar axes at zero. For lines or scatter plots, use an
appropriate scale for the question and make any restricted range explicit. Keep
scales comparable across related panels; do not exaggerate small changes.

Label axes, units, time ranges, and series. Use consistent numeric precision.
Highlight the relevant series while keeping others readable. Annotate events or
thresholds only when they help explain the data.

For categories, choose distinguishable colors with labels or patterns. For
ordered magnitude, use a coherent sequential range; for deviations around a
meaningful center, use a diverging range. Do not assume red/green alone makes
positive and negative values understandable.

Provide an accessible summary and a data-table alternative when needed. Hover
tooltips must not be the only way to obtain essential values.

## Compose tables and dashboards around the task

Place the information needed for the user's decision before supporting metrics.
A prominent total is useful only if it answers the task. Do not use the same
metric-card shell for every dashboard.

Align text left in left-to-right interfaces and numbers right, with consistent
units and precision. Use clear headers; lower their visual weight only when
users can still scan by column. Keep sorting and filtering understandable and
keyboard-operable.

Increase visible records by removing redundant columns, combining related
unsortable information, and tightening row padding before reducing legibility.
Keep columns separate when comparison, sorting, or export depends on them. Use
restrained separators or alternating backgrounds when they clarify rows;
preserve generous separation between unrelated dashboard regions.

Design no-data, no-results, loading, and error states. Test representative long
values, unusually large or negative numbers, narrow screens, and supported
themes. Do not infer these states from a chart full of convenient sample data.
