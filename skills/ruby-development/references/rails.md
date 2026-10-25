# Rails mechanisms

Check the installed Rails and job-library versions before relying on an API.

## Model behavior and capabilities

A Rails model can be an ordinary Ruby class; inherit from Active Record when the
object needs its persistence contract. Follow the repository's organization for
model-owned operations and collaborators.

Use a concern to group a cohesive part of a model's behavior or share a genuine
capability across models. A model-scoped concern can have one consumer. Make its
host dependencies clear: required attributes, associations, methods, and
callbacks. A mixin that provides behavior, a capability protocol that consumers
implement, and a polymorphic association solve different problems; a shared name
or suffix does not make them interchangeable. Guard optional participation with
`respond_to?`; let missing required methods expose a broken contract.

When adapting a framework method, inspect when it yields, whether it persists,
how it fails, and what protects concurrent calls. For example, a creation block
on `find_or_create_by` does not run for a found record. Reusing another helper
must preserve that distinction; test both found and newly created records.

## Changes and callback timing

Identify whether the rule concerns a pending write or the transition made by a
completed save. A present value alone does not prove a transition occurred in
this save. For example, a registration callback may need to distinguish
`completed_at` moving from nil to a timestamp from a later name edit on an
already-completed record. Test both, plus an unrelated update, before
simplifying the guard.

Use pending-change APIs such as `will_save_change_to_attribute?` and
`attribute_change_to_be_saved` in validations and before-save callbacks. Use
`saved_change_to_attribute?`, `saved_change_to_attribute`, and
`attribute_before_last_save` for the completed save in after-save callbacks.
Inspect intervening saves or reloads that can replace the dirty-tracking state.

Choose side-effect timing explicitly. An after-save callback still runs within
the transaction; it does not prove commit. Use the project's supported
after-commit/enqueue mechanism when a consumer must observe committed rows, and
check its behavior for the installed queue adapter. A database transaction does
not make Redis enqueue or an HTTP request atomic with database writes. A lock,
uniqueness constraint, retry, and transaction protect different failure cases.

## Relations, batches, and associations

An Active Record relation is lazy until an operation evaluates it. `length`,
`to_a`, and ordinary `each` load records; calling them before batching can
retain the full dataset. `size` depends on loaded state and may issue a count,
while `count` normally requests a database aggregate. Choose based on whether
the caller needs records, a count, or existence; avoid an extra query solely for
progress logging.

Use `find_each` or `in_batches` for large datasets only when their ordering and
iteration semantics fit the operation. Inspect query plans and round trips for
large scans, JSON predicates, and repeated lookups. Preload associations where
it removes demonstrated N+1 work, not as a blanket default.

A custom cursor needs a stable total order, a unique tiebreaker where values can
tie, and a predicate that advances in that same order. Test a full batch with
equal timestamps: a timestamp-only `>=` cursor can repeat it indefinitely. Check
Rails-version support for custom batch cursors and account for concurrent
changes to cursor fields.

Loaded associations may be stale after writes through another relation or
instance, particularly bulk operations. Decide which object owns the current
view and reset/reload or query that view when required. Do not add repeated
reloads to disguise an unclear ownership contract.

Bulk updates and deletes can bypass model validations and callbacks. Confirm
that omission is intended and that database constraints still protect required
invariants.

## Presentation, flags, and permissions

Presenters and components own display state, formatting, and rendering choices.
Derive those choices from model or policy decisions rather than making rendering
perform domain writes or become the only enforcement of a business rule. Make
inputs and data loading explicit; repeated rendering must not multiply queries
or side effects.

Distinguish three decisions: a feature flag selects available behavior,
authorization determines whether an actor may act on a resource, and domain
eligibility determines whether the operation is valid. Enforce required checks
server-side even when the UI hides or disables an action. Use the repository's
authorization mechanism for both collection scope and individual operations;
authentication and an enabled flag do not establish record access.

Use the existing flag adapter and distinguish operational switches from
user-targeted rollout or experiments. Choose evaluation identity and behavior
when configuration or the provider is unavailable; the safe fallback depends on
the operation. For queued work, decide whether a flag selects behavior at
enqueue time, execution time, or both. Test meaningful enabled, disabled, and
unavailable-provider paths, plus denied requests independently of UI state.

## HTTP input and job boundaries

Controllers authorize the actor and resource before protected reads, writes, or
enqueue operations. Permit input before mass assignment or conversion into a
downstream payload. Strong parameters restrict assignable input; they do not
grant resource access or define a queue serialization format. Convert the
permitted shape using the repository's native facilities; avoid a new parameter
wrapper that adds no independent contract.

A job boundary needs an explicit payload, enqueue failure behavior, and a
completion contract. An accepted enqueue does not mean execution succeeded.
Design retried work for the actual duplicate delivery and partial-failure risks,
including external side effects. Use the project's chosen job API; Active Job
and native Sidekiq have different serialization and enqueue contracts, so do not
migrate between them incidentally.

When using native Sidekiq, arguments must survive JSON serialization and
decoding: strings, numbers, booleans, nil, arrays, and hashes with string keys.
Pass IDs or small explicit payloads, not model instances, symbols, Time objects,
or raw parameter objects. `as_json` can supply a native representation;
`to_json` produces a string and changes the job's input shape. Test the decoded
payload, not just an in-memory hash.

For sparse updates, omitted means unchanged while nil may mean clear and false
may mean disable. Rails `blank?`, `presence`, and `compact_blank` can erase a
meaningful false value; use them only when that is the intended contract.

## Migrations and rollout

Inspect the production database adapter and existing migration conventions.
Check reversal, lock duration, table size, and compatibility with both old and
new application versions. Separate schema changes and large data backfills when
their deployment or resource requirements differ. A reversible migration is not
necessarily safe to run on a large live table.

Use database constraints for invariants that must survive concurrent or
non-model writes; application validation alone cannot prevent a uniqueness race.
Choose indexes for the actual predicates and ordering, backed by query evidence.
Account for adapter-specific requirements such as concurrent index creation
outside a migration transaction.

Test the transitions, serialization, query behavior, and migration paths
affected by the change. For callback tests, assert both the required side effect
and its absence on unrelated saves.

## API references

Consult documentation matching installed versions for exact API behavior:

- [Active Support concerns](https://api.rubyonrails.org/classes/ActiveSupport/Concern.html)
- [Active Record dirty tracking](https://api.rubyonrails.org/classes/ActiveRecord/AttributeMethods/Dirty.html)
- [Active Record query guide](https://guides.rubyonrails.org/active_record_querying.html)
- [Active Record batch cursors](https://api.rubyonrails.org/classes/ActiveRecord/Batches.html)
- [Active Record migrations](https://guides.rubyonrails.org/active_record_migrations.html)
- [Sidekiq best practices](https://github.com/sidekiq/sidekiq/wiki/Best-Practices)
