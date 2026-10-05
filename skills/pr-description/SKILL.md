---
name: pr-description
description: Use when drafting, revising, or reviewing a pull request title or description, including when opening or publishing a PR.
---

# Pull request descriptions

Write a cover note for the reviewer, not a changelog, diff summary, or record of
commands run. Give the reviewer the intent and context that the diff cannot.

## Gather context

Use the work and decisions already established in the current session. Do not
reread the entire branch when that context is current and sufficient.

Read the repository instructions and PR template before drafting. When a template
has an explicit structure, preserve its headings, order, required markers, and
checklists. Apply this skill within that structure instead of replacing it.

Inspect Git or GitHub only to fill gaps or verify material claims. Read the full
branch diff when the session did not produce the work, the scope is unclear or
stale, later commits materially changed it, or the user asks for a full refresh.
Otherwise, prefer targeted checks of the facts the description relies on.

Do not invent motivation. Ask the user when the reason for the change cannot be
established from the conversation, issue, commits, or repository context.

## Title

Write a concise title describing the changed behavior. Follow the repository's
title convention; apply commit-message rules only when the repository also
requires them for PR titles.

## Default body

Use this structure when the repository does not define one:

```markdown
## What

<One short paragraph describing the changed behavior and affected surface.>

## Why

<One short paragraph explaining the problem, goal, or decision behind it.>

## Notes

<Only non-obvious context that helps the reviewer judge the change.>
```

Put **What** before **Why** so the reviewer knows what the rationale refers to.
Use short paragraphs by default. Use bullets when the change has independent
behaviors that are clearer as a list.

Omit **Notes** when nothing earns it. For a trivial mechanical change, collapse
What and Why into one short paragraph when headings would add more ceremony than
clarity.

## What belongs in each section

### What

State observable behavior, affected contracts, or the shape of the change. Give
enough context for a reviewer to locate the change in their mental model without
narrating files or commits.

### Why

Explain what was awkward, broken, risky, costly, or impossible before the
change. Record why the chosen approach matters when a reasonable alternative
exists. This is the highest-value section because the diff cannot recover intent.

### Notes

Include an item only when it changes how someone should assess or use the change:

- a non-obvious implication, risk, tradeoff, or rejected alternative
- migration, compatibility, rollout, or rollback constraints
- a deliberate omission or boundary that may otherwise look accidental
- a specific decision or area where reviewer judgment would help
- a verified issue, design document, or prior discussion
- meaningful validation when its result changes confidence in risky behavior

Use screenshots for visual behavior and before/after examples for changed
contracts. For a large code or system architecture change, use a concise text
visual or Mermaid diagram when it explains the structure, dependencies, or flow
more clearly than prose. Fit the visual into the repository template when one
exists. Do not add an artifact because a template or habit suggests one.

## Cut aggressively

Delete content that does not help a reviewer understand or judge the change:

- facts obvious from a quick reading of the diff
- file-by-file inventories and commit narration
- routine commands, CI logs, test lists, and generic check sections
- installation or platform behavior the intended reviewer already knows
- empty headings, placeholders, and “not applicable” filler unless required
- generic requests to check tests, errors, edge cases, or code quality
- decorative screenshots and diagrams
- claims such as “robust,” “clean,” “comprehensive,” or “fully tested”
- the history of revisions made while the PR was under review

Keep motivation, behavior changes, real decisions, open questions, and material
risk. Cut mechanism before cutting intent.

## Style

Use active voice and specific verbs. Keep one idea per sentence and one term per
concept. Prefer a concrete sentence over a heading with one weak bullet beneath
it. Avoid repeating the title verbatim or opening with “This PR.”

Write for a competent engineer with limited attention. Point out only context
that the author knows and the reviewer needs.

## Final pass

Before publishing or updating the description, check:

1. Can the reviewer understand the change's intent and scope before reading the diff?
2. Does every paragraph help the reviewer make a decision?
3. Does the body describe the current branch rather than how it evolved?
4. Are all issue links, risks, results, and behavior claims supported by evidence?
5. Can anything be removed without losing intent or review-relevant context?
