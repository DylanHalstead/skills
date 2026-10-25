---
name: issue-authoring
description: "Investigate and distill context into clear bugs, feature requests, and engineering tasks. Use when drafting or refining tracker issues, defining verifiable outcomes, or splitting work into related issues and milestones. Follow the user's preference for concise descriptions and standalone tasks across Linear, GitHub, and other trackers. Not for implementing the work or writing PR descriptions."
---

# Issue authoring

Write for the person picking up the work. Explain what needs to change, why,
and anything they cannot safely infer. Apply these preferences across trackers
unless the user requests otherwise or a project requires a specific format.

## Establish the work

Start from the supplied context. Investigate gaps that affect scope, expected
behavior, dependencies, or how completion can be verified. Use relevant code,
documentation, existing issues, or external sources as needed; stop when the
work is clear enough to describe.

For bugs, establish observed behavior, expected behavior, and reproduction
details where available. Keep suspected causes separate from verified facts.

Define what would demonstrate completion. Ask about decisions that materially
change the work; leave routine implementation choices to the implementer.

## Writing

Use an action-oriented title. Start the description with the change and its
reason; a short paragraph is often enough. Add bullets for distinct requirements
and examples or code when exact behavior matters.

Less is more. Use headings only when they help the reader follow the content.
Cut repetition, generic engineering advice, and sections that add ceremony.
Leave routine implementation choices to the person doing the work. Select the
details each ticket needs rather than transcribing all the source notes. Put
shared context at the project or milestone level; repeat it only where needed
to understand or safely carry out a ticket.

Keep necessary contracts, existing behavior to preserve, and concrete risks or
rollout constraints. Keep each constraint scoped to the operation it applies to.
Express completion conditions where they clarify the requested behavior without
repeating requirements in a separate checklist. Distinguish open questions and
recommendations from agreed requirements. Brevity must not hide a material risk.

Use plain language and active verbs. Avoid decorative formatting and sentences
that merely introduce or summarize the surrounding text.

Use established context and read existing material before changing it. Preserve
useful decisions and links. Link shared context rather than copying it into every
ticket, while keeping each ticket's requested change understandable.

## Organization

Use the smallest useful set of tickets. Keep work together when it can ship as
one change; separate implementation steps alone do not justify a split. Split
at independent deliverables or necessary deployment boundaries, and preserve
those prerequisites in the blocking relations.

Prefer standalone tickets over subtasks or umbrella parents. Use blocking
relations for real dependencies and related links for context. State additional
conditions, such as deployment or verification, when a relation alone is unclear.

Group tickets when they share a meaningful outcome.
Describe that outcome briefly; leave task details in the tickets.

