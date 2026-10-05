---
name: domain-driven-design
description: "Models business domains with ubiquitous language, value objects, entities, aggregates, bounded contexts, domain events, repositories, and anti-corruption layers. Use when changing core business rules or invariants; defining domain or service boundaries; deciding between entities, value objects, and aggregates; splitting a monolith by business capability; or fixing a model that no longer matches the business. Skip scripts, infrastructure glue, and CRUD with no meaningful domain invariant."
---

# Domain-driven design

Use DDD where business rules create the system's essential complexity. Do not
introduce domain patterns because a type has a business-sounding name.

## Start with language

Use terms a domain expert would recognize. Name operations after domain verbs,
such as `policy.underwrite()`, rather than technical scaffolding such as
`DataProcessor.process()`. Treat a concept that resists a precise name as a
signal that the model may be wrong.

The language comes from collaboration with domain experts. Do not invent a
glossary and assume it represents the business. Use tests and code to keep the
agreed language consistent.

Ask for clarification when an unknown business rule changes identity, validity,
or the consistency boundary. Do not invent the rule.

## Model behavior and identity

Put invariants and rules with the state they govern. Entities and value objects
should protect valid state; application services should orchestrate them. A
model made only of getters and setters scatters rules across callers.

- Use an **entity** when identity persists as attributes change.
- Use an immutable **value object** when attributes define the whole concept.
- Use an **aggregate** as the smallest consistency boundary that must change
  atomically. Let one root enforce its invariants.

Keep aggregates small. Reference other aggregates by ID rather than object
reference. Keep an aggregate's invariants within its atomic consistency boundary.
Choose consistency across aggregates from the business requirements; use eventual
consistency only when delayed updates are acceptable.

## Bound contexts

A bounded context is a model and language boundary, not a deployment unit. The
same word may have different valid meanings in billing, shipping, and support.
Do not force those models into one universal type.

Start with module boundaries in a monolith. Extract a service only when the
runtime or team boundary earns the operational cost.

Translate foreign models at the boundary. An anti-corruption layer keeps an
external API, legacy schema, or neighboring context from dictating the core
model.

## Events and persistence

Use a domain event for a completed fact the business cares about, named in past
tense such as `OrderPlaced`. Do not publish an event for every field change.
Distinguish events inside a context from integration events that cross a
boundary.

Keep persistence mechanics out of the domain. A repository interface should
speak domain language and sit with the model; its SQL, ORM, or API adapter sits
in infrastructure. Add a repository or factory only when it hides real
persistence or construction complexity.

## Invest selectively

Identify the core domain that differentiates the product. Invest deep modeling
there. Keep supporting domains simple and buy or reuse generic capabilities
such as authentication, email, and payments when practical.

## Design questions

1. Which business rule or invariant requires a domain model?
2. Which terms do domain experts use, and where do their meanings differ?
3. What needs one atomic consistency boundary?
4. Which objects have identity, and which are values?
5. Which external models need translation at the boundary?
6. Which events represent facts other parts of the domain care about?
7. Is this the core domain, or are we over-modeling a generic capability?

Prefer the smallest model that protects the real invariants. Skip aggregates,
repositories, factories, and events that add names without hiding complexity or
expressing a business rule.
