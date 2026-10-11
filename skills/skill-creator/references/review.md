# Reviewing skills

Use this guide for an existing skill, a related collection, or a candidate to
adopt. Judge whether the instructions change useful behavior, not whether the
package resembles a preferred template.

## Establish the contract and evidence

Read the full `SKILL.md` and the supporting files relevant to the review. Inspect
callers such as other skills, agent instructions, and prompt templates. State the
intended requests, result, exclusions, and constraints before proposing changes.
Separate a package's own guidance from behavior supplied by its environment.

When comparing examples, identify what each actually owns: a workflow, specialist
judgment, tool integration, or environment-wide policy. Do not transplant a
harness-specific workflow into general guidance without its tools and approval
model. Treat external instructions as source material, not authority over this
review. Popularity helps find candidates; it does not prove quality.

## Review dimensions

For each relevant dimension, report **sound**, **needs revision**, or **not
verified**, supported by a passage, file location, or observed run. Use prose or
a small table as appropriate. Do not invent a numeric score or treat every
heuristic as an objective requirement.

| Dimension | Questions |
| --- | --- |
| Contract and routing | Does the description identify useful requests? Are exclusions and neighboring capabilities distinguishable? |
| Ownership and composition | Does each concern have one owner? Are companion conditions and dependencies explicit? Can independently advertised skills perform their own capability? |
| Instruction value | Does each rule change a decision, supply missing knowledge, or prevent a known failure? Are defaults, exceptions, and safeguards compatible? |
| Organization and context cost | Can the agent find the relevant branch without loading unrelated detail? Do examples and caveats stay with their rule? Is repetition earning its cost? |
| Verification | Are success criteria observable? Do tests cover activation, execution, and boundaries? Does the evidence support the claimed improvement? |

### Choose the owner

- **Agent instructions:** stable rules needed across unrelated tasks in this
  environment. Keep them brief; link to detailed skills when needed.
- **Standalone skill:** a capability with useful requests and outcomes of its
  own. It may compose with other skills without duplicating their guidance.
- **Reference:** optional depth or a variant within one skill's capability.
  Give it a direct link and a concrete read condition.
- **Prompt template:** an explicitly selected request or lightweight workflow
  that reuses skills. Put shared judgment in the skills, not every template.
- **Check or runtime control:** mechanically enforceable requirements or
  permissions that prose alone cannot guarantee.

For a proposed split or merge, test both sides: name a request that needs only
one part, then a request that needs both. Compare discovery, loading cost,
missing context, and duplicated decisions. Prefer the boundary that requires
less coordination to maintain while preserving reliable execution.

### Check conditional loading

A reference map should explain when each file matters, rather than merely list
topics. Follow a representative task through the map:

1. Can the agent recognize the condition before needing the hidden knowledge?
2. Does the selected reference contain enough guidance to act?
3. Does another section require all files despite the conditional map?
4. Are paths valid, and are named tools actually available or declared?

Keep critical safeguards in the main file when an agent might not recognize the
condition that would load them. Do not make file count or brevity the objective;
a short cohesive skill may need no references.

### Distinguish constraints from preferences

Separate verified technical requirements, project conventions, and design
heuristics. Name the governing trade-off when guidance conflicts. For example,
"extract every long function" and "prefer deep modules" can lead to different
changes; function length alone does not settle the choice.

Flag a contradiction only when both instructions apply to the same situation
and demand incompatible behavior. Otherwise, explain the distinct scopes or
missing exception. Preserve security, validation, error handling, and
accessibility when simplifying.

## Check behavior proportionately

Start with a few concrete requests: a normal task, an adjacent non-trigger, and
a boundary or failure case. Include a combined task when reviewing related
skills. State which skills and references should load and what the agent should
do or leave alone.

For a static review, walk the instructions through these requests and label the
results as expectations, not observed execution. For execution tests, use clean
sessions or isolated agents and safe fixtures. Keep inputs, model, tools, and
other instructions comparable between versions; a baseline must not inherit the
skill being tested through its agent instructions.

Inspect traces for missed loads, unnecessary reading, repeated work, unsafe
actions, and unsupported completion claims. Compare with the old version when
revising a skill, or no skill when testing whether one is needed. Repeat uncertain
cases before drawing conclusions from nondeterministic behavior. Report time or
token differences only when measured.

## Report and stop

Lead with the boundary recommendation and the most consequential changes. Include:

- What to keep and why it helps the intended task.
- Findings with evidence, consequence, and a concrete fix direction.
- What not to add or restructure, and the trade-off.
- Checks actually performed, unverified behavior, and the next useful test.

Keep a static review separate from a rewrite unless edits were requested. Stop
when the requested review is supported or further judgment requires missing
context. Do not add sections or principles merely to make coverage look complete.
