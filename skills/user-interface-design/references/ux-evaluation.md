# UX evaluation

Review the requested experience against a concrete task and the intended
user's knowledge and constraints. Diagnose usability separately from visual
preference. Do not turn a focused review into a product-wide audit.

## Establish the evidence

Read the brief, applicable design intent, representative content, and known
behavior. Include relevant entry points, permissions, failure states, and return
paths. Match claims to the evidence available:

- **Source only:** identify code-supported concerns without claiming observed
  rendered layout, timing, measured contrast, or assistive-technology behavior.
- **Screenshot or static render:** report directly visible hierarchy, grouping,
  labels, density, and visual treatment at the captured viewport and state.
  Check that the capture represents the target under review; note uncertain
  freshness. It does not establish other viewports, keyboard behavior, dynamic
  states, timing, or measured contrast.
- **Runnable interface:** also inspect the relevant flows, changed interactions,
  and states. Measure contrast and test keyboard or assistive-technology behavior
  before claiming those checks passed.

None of these substitutes for participant evidence about actual user behavior.
If a check is unavailable, report the specific limit rather than discarding
observations supported by the evidence you do have.

State the task and success condition before reviewing. Use supplied research,
support reports, or analytics when available. Personas can help form questions,
but invented personas and simulated walkthroughs do not establish how real
people behave. Do not estimate task completion rates or satisfaction scores
from expert judgment.

## Walk the task

At each meaningful step, ask:

1. **Intent:** will the intended user understand the next goal, given what they
   know at this point?
2. **Discovery:** can they notice and reach the relevant action, including with
   keyboard, touch, or assistive technology where applicable?
3. **Meaning:** does the label and affordance connect the action to its outcome?
4. **Feedback:** after acting, can they tell what changed and what to do next?

Check the actual control, wording, state, and path behind a concern. A "no" is
an investigation lead, not automatic proof that users abandon the task. Distinguish
an observed blocker from a plausible hesitation that needs participant evidence.

For example, a successful upload followed by an unchanged screen may leave the
user unsure whether retrying will create a duplicate. Inspect the success feedback
and resulting file location. Recommend making the outcome clear; do not claim a
measured abandonment rate. An expert batch tool may intentionally use quieter
feedback than a first-use upload flow while still making status discoverable.

## Check relevant usability principles

Use these to investigate gaps, not to require a full report on every category:

- Visible status and understandable feedback during and after operations.
- User vocabulary and a structure that fits the task.
- Escape, undo, or confirmation appropriate to risk and reversibility.
- Consistent controls and familiar platform behavior.
- Error prevention and recoverable validation without unnecessary friction.
- Discoverable information instead of forced recall across steps.
- Efficient repeated work without overwhelming newcomers.
- Clear hierarchy and content that earns its place.
- Specific failures with a usable recovery path.
- Help where the task actually requires explanation.

Use this skill's owning references for detailed navigation, controls, recovery,
accessibility, and visual hierarchy. Use `visual-design` only when the review also
questions the visual direction or expressive composition; a task walkthrough
need not reopen the brand.

## Report actionable findings

For each material finding, identify:

- The element, state, or path and the evidence inspected.
- The affected task and observable failure or plausible risk.
- A concrete correction at the owning boundary.
- Any uncertainty or check needed to confirm the effect.

Prioritize blockers, loss of work, deception, and access failures before
recoverable friction and polish. Consider task importance and reach, not just
how visible a defect looks. Group findings that share one cause. Include useful
existing behavior when it constrains the fix; do not invent praise or quotas.

Do not add heuristic verdicts into an overall score. Separate unmet requirements,
observed defects, usability hypotheses, and aesthetic trade-offs. Flag hidden
costs, fabricated proof, misleading consent, or obstructed cancellation through
the specific behavior; determine legal requirements from current authoritative
sources rather than treating an anti-pattern label as a legal conclusion.

Recommend the smallest correction and its verification. Review does not itself
authorize fixes or saved reports. When implementation is requested, recheck the
affected task and relevant regressions after changing it. Stop at the agreed
scope instead of routing through a mandatory chain of specialist reviews.

## Background

Optional conceptual source: Intent's [`evaluate` skill](https://github.com/ghaida/intent/blob/3fc38dff381ce0e4dec8f52c97c3e37abd95e10e/skills/evaluate/SKILL.md)
(CC0-1.0), especially cognitive walkthroughs and evidence-linked findings. This
reference does not adopt Intent's agent routing, estimated metrics, or required
report structure.
