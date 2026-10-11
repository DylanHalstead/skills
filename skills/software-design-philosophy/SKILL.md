---
name: software-design-philosophy
description: "Guides and evaluates software design using John Ousterhout's A Philosophy of Software Design (APOSD): complexity, deep modules, information hiding, interface design, error design, and design comments. Use when planning or reviewing APIs, module boundaries, abstractions, architecture, or structural refactors; when an interface feels complex; or when code seems over-engineered. Skip mechanical changes that preserve the existing design."
---

# Software design philosophy

Use these criteria to judge material design decisions. Prefer changes that reduce
the knowledge and coordination required for future work.

## Complexity

Judge a design by the complexity it imposes on future work:

- **Change amplification:** one decision forces edits in many places.
- **Cognitive load:** a developer must know too much to make a safe change.
- **Unknown unknowns:** it is unclear what a change can affect.

Dependencies and obscurity cause these symptoms. Move knowledge to one clear
owner and make dependencies visible.

## Deep modules

Prefer modules with a simple interface and substantial hidden implementation.
The interface is the complexity every caller must pay. A shallow wrapper that
adds another name, signature, or lifecycle without hiding knowledge makes the
system harder to understand.

Pull complexity downward. Let the module that owns a concern handle its edge
cases, defaults, and invariants rather than making every caller repeat them.
Different layers should expose different abstractions. A layer that only
forwards calls has not earned its boundary.

Red flags:

- shallow modules and pass-through methods
- information leakage across modules
- modules organized around successive processing steps that repeatedly expose
  the same implementation knowledge
- special and general behavior mixed together
- repeated decisions or assumptions
- interfaces that require long explanations
- vague abstractions such as `Manager`, `Helper`, or `Processor`
- queries named `get`, `build`, `parse`, or `render` that hide external writes

## Information hiding

Give each design decision one owner. Hide formats, protocols, ordering,
configuration rules, and storage details behind the module that owns them. If
two modules must change together because they share hidden knowledge, merge
the responsibility or create one module that owns that knowledge.

Design interfaces around the concept callers need, not the current
implementation. Prefer the simplest somewhat-general interface that covers
current uses. Avoid speculative generality and special-case methods that
multiply with each new requirement.

## Errors and invariants

Design errors out of existence when a stronger interface, type, or default can
make an invalid state unrepresentable. Otherwise, handle an error at one clear
boundary with one policy. Do not spread the same guard or fallback across
callers.

Keep invariants close to the state they govern. Expose operations that preserve
the invariant rather than mutable parts callers must coordinate correctly.

For stateful behavior, make state transitions and the order of effects easy to
follow. Separate computation from external effects when that clarifies the
flow. Keep ordering-sensitive updates in the operation that owns the invariant,
rather than across helpers callers must invoke in a remembered sequence.
Do not split a cohesive operation merely to make each helper pure.

## Comments as design documentation

Interface comments tell callers what they cannot learn from the signature:
contracts, guarantees, side effects, units, ordering, limits, and edge cases.
Implementation comments explain rationale, invariants, assumptions, and
non-obvious trade-offs. Do not restate code.

A comment must make sense to a future reader with no task, review, or plan
context. Record the code-level reason itself. When choosing a deliberate
simplification with a known ceiling, state the ceiling and what would force a
more complex design.

## Design process

Scale design work to risk. For a new or changed boundary, sketch the caller's
contract before choosing internals: inputs, guarantees, observable effects,
and failure behavior. Clarify completion and resource ownership when relevant.
Use a signature or a short interaction example; it need not become source
comments or a saved document.

Before refining a material design, identify the assumption most likely to
invalidate it. Check it with the smallest useful investigation: existing code,
a focused test or experiment, or authoritative documentation. State any
unverified assumption that affects the recommendation.

For a material boundary or abstraction, compare a second design built around
a different constraint. Judge how each option affects amplification, load, and
unknown unknowns. For a local mechanical change, follow the established design
without manufacturing alternatives.

Prefer strategic improvements that reduce complexity inside the requested
scope. Do not turn “leave it better” into unrelated cleanup. A broad structural
problem belongs in a separate refactor.

For a proposed design change, identify the current complexity, explain how the
change reduces it, and state the main trade-off.

## Review questions

1. Is the interface much simpler than the implementation it hides?
2. Does each important decision have one owner?
3. Can the implementation change without forcing caller changes?
4. Does each layer expose a distinct abstraction?
5. Are defaults and hard cases handled below the interface?
6. Do comments preserve intent rather than narrate code?
7. Does the design reduce total complexity rather than move it elsewhere?

Name a red flag only when you can show its concrete cost. Explain what must
change together, what knowledge leaks, or what a caller must understand that
the module should hide.
