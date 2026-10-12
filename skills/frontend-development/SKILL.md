---
name: frontend-development
description: "Build, debug, refactor, and review frontend components and features across frameworks. Use for state ownership, component props and composition, forms, routing and shareable views, data loading, Suspense or skeletons, styling implementation, hydration, browser resource cleanup, and frontend performance. Skip visual direction without an implementation concern and backend-only work."
---

# Frontend development

Build the requested feature using the project's framework, data layer, and styling
system. Keep page data, interaction state, and browser resources with the owners
that can govern their lifetimes.

Own implementation decisions. `visual-design` owns art direction;
`user-interface-design` owns UI fundamentals and observable interaction
expectations. Frontend development implements the agreed experience through
components, state, routing, events, and runtime behavior. A runtime fix
with an agreed interface does not require redesigning it.

## Establish the local contract

Read project instructions, the target package's dependencies, and comparable
implementations before choosing a mechanism. Identify what renders at build time,
on the server, and in the browser. Check installed versions before using an API.
Keep repository-specific package boundaries, filenames, and test commands local.

Read applicable `DESIGN.md` guidance when the change affects the rendered surface,
including a shared or brand owner named by project instructions. Use it for design
intent and the existing styling system for implementation. Surface conflicting
requirements that affect the requested change; do not silently rewrite intent,
audit unrelated token drift, or create a second design system. When no design
document exists, follow established components and styles.

When implementation leaves design decisions open or changes their contract,
load the relevant companion from the available skills list and read its
`SKILL.md` if it is not already loaded. If unlisted, resolve the fallback relative
to this skill:

- **`user-interface-design`** (`../user-interface-design/SKILL.md`): for unresolved
  or changed hierarchy, navigation, controls, states, interaction expectations,
  or accessibility requirements.
- **`visual-design`** (`../visual-design/SKILL.md`): for unresolved or changed art
  direction, expressive composition, or visual identity. Building a new page
  inside an agreed system does not automatically require new art direction.

Do not reopen settled decisions merely because implementation changes. An
agreed-interface runtime fix can stay in this skill. If a required companion is
unavailable, ask for its location and continue independent work.

For a focused fix, trace the interaction and data path that can explain the
failure. For a feature, identify the required inputs, actions, states, and reset
behavior. Do not introduce a store, query library, form library, or component
framework merely to satisfy this skill.

## Page data and runtime boundaries

- Prepare page data through the project's content system, route loaders, server
  functions, or query layer. Keep transport, validation, cache identity, and
  invalidation with the existing data owner rather than repeating them in views.
  Browser-only assets and external widgets can still need component-owned work.
- Pass the data a component needs, with a clear shape. Keep server credentials,
  database access, and server-only imports out of browser code. Type checking
  does not make a runtime import client-safe; inspect its runtime dependencies.
- In SSR, scope user-specific mutable state and caches to their intended request
  or session. Share public data only under an explicit freshness and isolation
  contract. Preserve compatible server output and initial browser rendering.
- Start independent work concurrently when it removes a real waterfall. Keep
  dependent work ordered and handle failure; do not parallelize writes whose
  ordering matters or start work that a cheap condition would avoid.

## State ownership and lifetime

Choose the smallest owner that satisfies the feature. Distinguish these cases:

| State | Default owner | Decision to check |
| --- | --- | --- |
| Disclosure, hover, selection, or other transient interaction | Component or nearby common parent | Which consumers must agree? |
| Editable draft | Form or interaction session | What starts, preserves, and resets the draft? |
| Shareable or restorable view | Router path/search state | What must reload, Back, Forward, or a shared link restore? |
| Remote result | Existing loader or query cache | What identifies it, makes it stale, and refreshes it after a write? |
| Persisted preference | Existing preference/storage boundary | What is its scope, default, and behavior when storage fails? |

Derive filtered lists, labels, and other computed values from authoritative inputs
instead of maintaining another writable copy. A local draft of remote data is
valid when editing needs isolation; define when it accepts a new source value
and when it retains unsaved work.

Keep ordinary props for nearby sharing. Lift state when siblings must agree;
use composition or a provider for a meaningful shared subtree or capability.
Prop depth alone does not justify an application-wide store.

Distinguish mount lifetime from interaction lifetime. A kept-mounted dialog may
start several sessions; old timers, requests, or exit completions must not mutate
or finish a newer session. Define whether superseded outcomes still notify their
original caller. Use the framework's reset mechanism when appropriate, with
explicit preservation behavior where unmounting is not enough.

For URL-backed controls, use validated router state as the authority. Preserve
unrelated search parameters. Keep credentials and sensitive draft data out of
URLs. Implement the agreed push/replace/Back behavior, including entry from a
shared link, without maintaining a second open flag that can drift. Local gallery
filters need not enter the URL unless sharing or restoration requires it.

## Components, props, and styling

Keep data orchestration distinct from presentation when it hides transport or
workflow knowledge. Do not split a cohesive component into pass-through wrappers
just to shorten files. Extract repeated behavior into an owner with a useful
contract, such as a shared submit operation, not a collection of unrelated hooks.

Use children, slots, or renderable regions for caller-owned content, and callbacks
for caller-owned actions. Variants and independent size/tone props are useful
when they describe supported treatments; do not ban booleans or prescribe compound
components for every control. Avoid prop combinations that imply impossible
states, and preserve native attributes, accessible names, and event behavior.

Use the existing tokens, utilities, and primitives. Keep repeated treatments in
their styling owner rather than copying class strings across surfaces. Respect
the project's class-merging behavior; class-string order alone does not determine
which CSS rule wins. Choose links for navigation and buttons for actions. Prefer
native controls when they provide the required keyboard, focus, and form behavior.

Check container width, long content, wrapping, and overflow, not just viewport
breakpoints. Preserve focus visibility, labels, disabled behavior, reduced-motion
support, and usable controls when implementing styles or animation.

## Loading, actions, and browser resources

Choose a loading boundary around the work that needs to wait. Keep independent
content and actions usable. Use Suspense, route pending UI, or explicit status
according to the installed framework and feature; none is a universal default.
A skeleton should reserve representative space for the resolved region, remain
noninteractive, and avoid announcing decorative placeholders as real content.

Implement the reachable pending, success, empty, failure, and retry states.
Distinguish initial loading from background refresh so a refetch does not erase
usable content or drafts. Preserve early user intent across a loading swap when
the agreed behavior requires it. Surface submission failures where the user can
recover; keep input unless the contract calls for a reset.

Define what happens when work overlaps: repeated submit, changed selection,
navigation, or a new interaction session. An obsolete result must not overwrite
newer intent. Use the existing loader/query cancellation and identity contracts
where available. Aborting a request does not undo a server write; handle uncertain
write outcomes without promising that cancellation prevented the operation.

Derive values during rendering or reactive computation, initiate user actions in
handlers, and use effects/lifecycle hooks for external synchronization. Give
listeners, observers, timers, animation frames, requests, and widget instances an
owner and teardown path. Cleanup must handle replacement as well as unmounting;
deferred callbacks must still belong to the current interaction when they run.

## Performance and verification

First inspect unnecessary client JavaScript, request waterfalls, repeated I/O,
large serialized payloads, and expensive DOM or rendering work. Choose hydration,
lazy loading, caching, memoization, or virtualization for a demonstrated cost or
clear workload. Do not hide required content, break accessibility, or complicate
ordinary code for an unmeasured micro-optimization.

Use the project's checks. Verify pure transformations at their owning module and
rendered interactions through the project's chosen test layer; do not introduce
a component-test framework where the repository uses browser tests instead.
Check the changed feature's relevant cases: reload and history, narrow containers,
keyboard/focus, loading and failure, rapid interaction, or teardown and remount.

Source inspection and passing builds or typechecks do not establish rendered
behavior or measured performance.
