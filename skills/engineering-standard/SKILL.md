---
name: engineering-standard
description: "Applies the house engineering standard to software work: repository conventions, scope control, local patterns, readability, idiomatic code, performance, scalability, and evidence-based findings. Use for any request to plan, implement, review, evaluate, or refactor code."
---

# Engineering standard

Apply this whenever you design, write, or judge code. Scale the process to the
task's uncertainty and risk. A mechanical change needs local context and a
focused check; a material design needs alternatives and broader verification.

## Conventions

When guidance conflicts, follow this order:

1. Explicit project instructions in `AGENTS.md`, `CLAUDE.md`, project skills,
   lint, formatter, and compiler configuration.
2. Patterns established in the codebase for names, modules, errors, logs, tests,
   and dependencies.
3. Idioms of the language, framework, and standard library in use.
4. General best practices.

Safety rules and explicit user authorization remain global constraints.

## Use the repository's skills

Load each available repository skill whose description covers a concern in
scope. Defer to the skill that owns that concern instead of restating its rules
through this standard.

Keep findings clean:

- **One finding, one owner.** Report an overlapping concern once under the skill
  that best owns it.
- **Name what mattered.** When recording a review or design decision, identify
  specialized guidance that materially affected the judgment. This does not
  require creating a separate artifact.

For a material change, read two or three comparable implementations to learn the
local pattern. For a small or mechanical change, inspect only enough nearby code
to establish the convention. Name representative files when the pattern supports
a design decision. Do not call a generic best practice an improvement when it
fights a sound local convention. Verify that a comparable implementation's
assumptions and resource ownership apply to this task. Carry over the rationale,
not incidental API shapes or layers; choose the structure for the current
contract. Flag conflicting project guidance rather than propagating a known
retired pattern.

Read these companion skills in full when their conditions apply:

- **`software-design-philosophy`**: substantial feature work, structural
  refactors, or designing, changing, or reviewing module boundaries, APIs,
  abstractions, or architecture. Fallback path:
  `../software-design-philosophy/SKILL.md`.
- **`domain-driven-design`**: designing, changing, or reviewing business rules,
  invariants, model boundaries, or service boundaries. Skip scripts,
  infrastructure glue, and CRUD with no meaningful domain invariant. Fallback
  path: `../domain-driven-design/SKILL.md`.

Find each skill in the available skills list and read its advertised `SKILL.md`
path; its description alone is not the guidance. If it is not listed, resolve
its fallback path relative to this skill's directory, not the working directory.
If neither location is available, ask for the skill's location before proceeding
with work that requires it. Continue independent work.

## Scope and design

Every changed line must trace to the request. Fix the root cause and inspect
other callers of the shared behavior before patching one symptom. Do not mix
unrelated cleanup into the change. Remove imports, variables, and functions that
your change makes dead; report pre-existing dead code instead of expanding the
diff.

For a fix or behavior-preserving refactor, identify the observable change the
request requires. Preserve other callers' behavior, including writes, enqueue
timing, errors, and responses. Explain a deliberate deviation before expanding
the change.

Add an abstraction only when it enforces an invariant, hides non-obvious
complexity, or removes duplication callers would otherwise get wrong. Prefer a
simple interface over a simple implementation and keep side effects visible in
names and orchestration.

Before finalizing, check new code, tests, and prose against the supported
contract, not just the motivating example or investigation. Preserve relevant
regression cases and non-obvious rationale; omit rejected hypotheses and
incidental history. Put operational instructions in their owning documentation.
Detailed comment criteria belong to the design skill.

## Quality bars

Hold changed code to all four. When they conflict, state the trade-off.

- **Readable:** Make code obvious on a first read. Use precise names, explicit
  data flow, and early returns over deep nesting. Avoid clever code without a
  comment that earns it.
- **Idiomatic:** Follow this codebase and its language rather than translating
  patterns from another ecosystem. Prefer the standard library and platform
  constructs already in use.
- **Performant:** Avoid needless allocation, repeated work, and avoidable I/O.
  Run independent work concurrently when it serves the workload, with explicit
  ownership, resource limits, and completion handling. Match data structures to
  access patterns.
- **Scalable:** Check behavior as input, data volume, and concurrency grow. Look
  for accidental quadratic scans, unbounded caches and buffers, N+1 queries,
  missing pagination or backpressure, and unsafe shared state.

Name values for their concepts; distinguish representations when they coexist.
Use domain terms in orchestration and precise platform terms at infrastructure
boundaries. Add qualifiers only to resolve ambiguity in the current scope. If a
name needs its producer to explain it, consider making it more specific.

Performance claims need evidence. Point to a round trip, allocation, scan, lock,
or measurement. Do not sacrifice clarity for an unmeasured hot path. Trace the
complete operation: work before batching, serialized queue arguments,
concurrency across workers as well as within one worker, and downstream
completion. A local limit or successful enqueue does not establish a system-wide
guarantee.

When changing delivery or integration tooling, trace changed inputs through the
trigger, checked-out revision, dependency build, runtime artifact, and terminal
success or failure. Verify that the deployed artifact comes from the intended
revision and includes its runtime dependencies; a passing build alone is not
that evidence.

## Review findings

Report a defect or material-risk concern only when you can show a reachable
failure, violated requirement, regression, or material risk. State the relevant
code path and the evidence that supports the claim. Keep honest uncertainty
visible: identify what runtime value, test, or contract would confirm a
plausible concern.

Distinguish defects from maintainability suggestions. A non-blocking suggestion
can be supported by a specific ambiguity, information leak, or navigation burden
without demonstrating a runtime failure. Explain what the reader must infer or
trace and how the proposed change reduces that work; preference alone is not
evidence.

After verifying findings, check whether several share one root cause. Merge them
when one coordinated change would fix them; otherwise, keep them separate. Do
not create a category solely to group unrelated findings.

For broad static audits or refactor planning, report a systemic pattern only
when it has at least two concrete instances and changes the remediation. Give
the pattern a plain name, cite representative locations, explain the shared
cost, and propose the coordinated fix. A single severe finding remains a
finding.

Order findings by merge impact and then blast radius. Lead with the findings
that reduce the most risk or complexity.

## Honest uncertainty

Say what you did not check. Report verification gaps separately from defects.
Missing tests or an unrun check do not, by themselves, establish incorrect
behavior. State what evidence would resolve an uncertainty. Do not write
confident conclusions about code you did not inspect.
