---
name: skill-creator
description: "Create, improve, and validate reusable agent skills. Use when turning a recurring workflow or session into a skill, drafting or editing SKILL.md and its bundled resources, or reviewing a skill's instruction quality and package structure."
---

# Skill creator

Produce a skill another agent can use without this conversation. Own the work
from scope and wording through proportionate verification.

## 1. Establish the need

Use the conversation, existing skills, project instructions, and source material
before asking questions. Ask only for missing information that changes scope,
behavior, risk, or the user's preferences.

Identify:

- The recurring task, intended user, and expected result.
- The knowledge or procedure the agent lacks: conventions, corrections,
  tool choices, failure cases, or output requirements.
- Observable success criteria and adjacent tasks the skill should leave alone.

Use concrete requests to establish the workflow and its boundaries. Reuse
examples already available; ask for more only when they would change the
instructions.

Reuse or improve an existing skill when it owns the same capability. For a
one-off request, use a prompt; for a mechanically enforceable rule, use a check
or runtime control. If the agent already succeeds without added guidance, consider
whether a skill offers enough value to justify maintaining it.

For an existing skill, inspect its references, scripts, and callers before
changing shared behavior. Preserve unrelated content. When reviewing a skill or
comparing packages, read [the review guide](references/review.md) before judging
boundaries, instruction quality, or proposed changes.

Proceed when the task, boundaries, source of expertise, and success criteria are
clear. Do not invent domain rules to fill gaps.

## 2. Define the skill's contract

Give the skill one coherent capability. Create separate skills when each has
its own useful requests, activation conditions, and result. Use references for
conditional detail that serves the same capability and does not need independent
discovery. A shared subject or frequent co-use does not require a merge; a
separate file does not, by itself, justify a separate skill.

For related skills, name the owner of each concern and the conditions for loading
companions. Keep workflow, specialist judgment, and environment-wide rules in
their appropriate owners instead of repeating them across packages.

Write a concise frontmatter `description` stating what the skill does and when
the user needs it. Use user-intent language and distinct trigger cases. Keep the
workflow in the body; the description should route the agent to read it.

Use portable YAML frontmatter:

- `name`: 1–64 characters; lowercase ASCII letters, digits, and hyphens; no
  leading, trailing, or consecutive hyphens. Match the directory name.
- `description`: a non-empty string, at most 1,024 characters.
- Optional fields: `license`, `compatibility`, `metadata`, and experimental
  `allowed-tools`. Use only when needed. Limit `compatibility` to 500 characters;
  `metadata` maps string keys to string values.

Use portable conventions by default. Include harness-specific instructions only
when the requested task requires them, and state the requirement. State actual
task dependencies instead of assuming tools exist. Frontmatter does not enforce
permissions or replace runtime safeguards.

## 3. Draft the minimum useful package

Start with `skill-name/SKILL.md`. Add files only when they serve the task:

- `references/`: conditional knowledge, with a direct link and a specific read
  condition in `SKILL.md`.
- `scripts/`: tested deterministic work the agent would otherwise recreate.
- `assets/`: templates or other files used in the output.

Put instructions needed on every run in the main file. Keep related decisions
and caveats together. Move branch-specific detail out when it obscures the core
workflow. Aim below 500 lines and 5,000 tokens; these are ceilings to stay below,
not targets to fill.

For several references, add a compact task-to-file map with concrete read
conditions. Give each reference one coherent topic, with examples and caveats
beside the decisions they explain. Keep links directly reachable from `SKILL.md`
and paths relative to the skill root. Do not split a short, cohesive skill just
to create folders, or require every reference in a supposedly conditional map.

Write the procedure or review criteria with:

- A default approach before exceptions.
- Observable conditions for branches, questions, escalation, and stopping.
- Checkable completion criteria and the required output shape.
- Exact steps for fragile operations; judgment where multiple approaches work.
- Short rationale for non-obvious choices and safeguards for material risks.

Use a concrete example when wording alone leaves an important ambiguity. Model
actual inputs and useful outputs; avoid decorative examples and placeholders.
Read project instructions before prescribing commands or conventions. Resolve
bundled paths from the skill directory, not the caller's working directory.

## 4. Edit for behavioral value

For each instruction, identify the decision it changes, the missing knowledge
it supplies, or the failure it prevents. Cut generic advice such as "follow best
practices" when it provides none of these.

For example:

```text
Vague: Handle missing information appropriately.

Concrete: Ask for missing information only when it changes the result.
Otherwise, proceed and state the relevant assumption.
```

- Remove introductions, repeated meanings, stale facts, and empty sections.
- Keep each rule in one authoritative place within the package. Include the
  knowledge needed to execute the skill's own capability. Explicit companion
  loading may compose independent skills; do not rely on an unnamed skill or
  external authoring guide to explain missing instructions.
- Prefer direct verbs and concrete nouns over jargon, slogans, and roleplay.
- State desired behavior. Reserve prohibitions for real boundaries and pair
  them with the safe alternative where useful.
- Keep safeguards, error handling, and accessibility even when compressing.
- Check contradictions, unsupported tool assumptions, and examples that conflict
  with the rules. Preserve the supplied contract; add output fields or stricter
  policies only when they serve a stated need. Avoid blanket ALWAYS/NEVER rules
  for judgment calls.

Do not compress instructions into ambiguous shorthand. A shorter skill is useful
only if another agent can still execute it.

## 5. Validate and iterate

Parse frontmatter with an existing YAML parser and check the field constraints.
Check local references, required tools, and discovery in the target environment.
Preserve applicable licenses when incorporating third-party material. Run bundled
scripts with their documented interpreter in a safe workspace, checking normal
and error paths.

Check routing and execution separately. Use realistic requests that should
activate the skill, adjacent requests that should not, and at least one boundary
or failure case. Define the expected behavior before judging results. For a
material revision, compare the previous version or a no-skill baseline in clean
sessions when practical; inspect loaded files and wasted steps as well as final
outputs. A static walkthrough can expose ambiguity but does not prove runtime
activation or improvement. Report anything you could not check.

Fix ambiguity, missing knowledge, or wasted steps based on observed behavior.
Rerun affected checks after revision. Stop when the agreed criteria hold or
further progress needs input.

## Handoff

Report the skill path, scope, checks performed, and unresolved gaps. Distinguish
actual results from proposed tests. Include setup or discovery instructions only
when the target environment needs them.
