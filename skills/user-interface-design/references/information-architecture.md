# Information architecture

Organize information so users can find the starting point of a task, understand
where they are, and reach the expected content. Work within the existing shell
for a local change; do not redesign site navigation merely because a new screen
needs a place.

## Establish the information space

Inspect representative content, existing navigation, labels, and available
search logs, support reports, or user research. Identify the primary tasks,
user vocabulary, content types, permissions, and likely growth. Distinguish
observed behavior from a proposed mental model; internal categories are not
proof that users think the same way.

For a material navigation change, show where existing destinations move and
which labels or paths change. Preserve URLs, bookmarks, and tracking contracts
unless their change is in scope; routing mechanics belong to implementation.

## Choose structure from the task

| Structure | Useful when | Main trade-off |
| --- | --- | --- |
| Hierarchy | Content has meaningful parent-child relationships | Deep nesting or overlapping categories makes destinations hard to predict |
| Flat collection | Similar records can be scanned, searched, or filtered | Diverse content needs stronger grouping and discovery aids |
| Hub and spoke | Tasks are distinct and users usually finish one before switching | Cross-task work becomes awkward if every move returns through the hub |
| Faceted collection | Users combine independent attributes to narrow many records | Vocabulary, filter interaction, and no-results recovery become part of navigation |
| Sequential flow | Later steps genuinely depend on earlier decisions | Unnecessary sequencing slows repeat users and makes revisiting choices harder |

Use global navigation for stable product areas and local navigation for the
current area. An overview dashboard can summarize and link to tasks, but need
not become the home of every feature. Name the product-specific trade-off rather
than selecting a pattern by fashion or a fixed item-count threshold.

## Categories and labels

Group by the user's content or task, not automatically by database tables or
team ownership. Check ambiguous items against representative examples. If an
item legitimately belongs in multiple categories, use cross-links, facets, or
multiple appearances backed by one authoritative record rather than duplicating
its data. Avoid a growing "Other" category that conceals a broken classification.

Labels should predict what users will find or do. Prefer their vocabulary;
retain established terms when changing them would create confusion. Test a label
by showing its contents and asking whether the destination is predictable, not
by judging whether the word sounds modern.

For example, a documentation topic may serve both a beginner's task guide and
an expert's API lookup. Cross-link the same topic from both paths; do not force
both audiences through one sequence or maintain two conflicting copies. A small
settings panel may need only clear groups and labels, not a search system.

## Support different finding behaviors

- **Known item:** a precise destination, direct link, or search result.
- **Explore:** meaningful categories, previews, and filters that reveal what exists.
- **Return:** relevant history, saved items, stable links, or restoration of the
  agreed view state. Do not persist everything merely to support re-finding.
- **Unfamiliar domain:** plain-language entry points and examples; search alone
  cannot help someone who does not know what to ask for.

Combine search and browse when tasks need both. For filters, show selection and
a usable reset or broadening path. Distinguish an empty collection from no
matches. Do not disable a zero-count filter blindly when counts are unavailable
or changing; choose behavior from the data and task contract.

## Orientation and validation

Keep current location, available destinations, and arrival clear through useful
headings, active states, contextual links, or breadcrumbs. Breadcrumbs help in a
hierarchy but do not repair misleading categories. Check entry through a deep
link as well as the main navigation.

Validate consequential assumptions with the smallest suitable evidence:

- Card sorting explores how participants group and name content.
- Tree testing checks findability in a text hierarchy before visual styling.
- First-click or usability tasks check how people find a destination in the UI.
- Search and support records expose vocabulary mismatches and missing paths.

Choose participants and tasks for the intended audience and decision; a fixed
sample size does not guarantee validity. An agent walkthrough is an expert
hypothesis, not participant research. If evidence is unavailable, present the
structure as a proposal and name what would confirm or challenge it.

For a design discussion, return the relevant hierarchy or paths, label decisions,
main trade-off, and material uncertainty. A sitemap, taxonomy document, or saved
research plan is not required unless the request needs that artifact.

## Background

Optional conceptual source: Intent's [information-architecture reference](https://github.com/ghaida/intent/blob/3fc38dff381ce0e4dec8f52c97c3e37abd95e10e/skills/intent/references/information-architecture.md)
and [`organize` skill](https://github.com/ghaida/intent/blob/3fc38dff381ce0e4dec8f52c97c3e37abd95e10e/skills/organize/SKILL.md)
(CC0-1.0). The guidance here does not depend on Intent's routing or tools.
