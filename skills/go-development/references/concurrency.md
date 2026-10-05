# Concurrency and lifecycle

Keep APIs synchronous by default so callers own concurrency. Use channels for
ownership transfer, work distribution, or asynchronous results; use mutexes for
shared-state invariants. Choose the simplest expression of the contract, not a
blanket channels-over-locks rule. Prefer a map plus a mutex over `sync.Map` unless
its specialized access patterns fit. Typed atomics suit independent values, not
invariants spanning fields.

Use a `sync.WaitGroup` to wait; prefer `WaitGroup.Go` on Go 1.25+ for scoped tasks
that cannot panic. It supplies neither error propagation nor cancellation.
Use `errgroup.WithContext` when first-error cancellation fits and `x/sync` is
available or justified; independent per-item failures may need collection instead.

## Ownership and blocking

Before starting a goroutine, identify its owner, exit condition, completion/error
path, and behavior when the caller cancels or stops consuming. Join scoped workers
before returning; give service-owned workers shutdown and join paths. Recover
panics only at a deliberate containment boundary with a failure policy.

Bound admission before spawning; acquiring a semaphore inside each goroutine
leaves goroutine count unbounded. Validate limits and make admission cancellable
when required. Stop scheduling on cancellation and collect started work.
`errgroup.SetLimit` bounds active work, but a blocked `Go` call does not select on
cancellation.

Cover blocking receives, sends, and I/O, not just result delivery. A buffer of one
may prevent an abandoned result send from blocking; it cannot stop a stuck
producer. Cancellation is cooperative.

## Channels and shutdown

Choose capacity from the handoff/queue bound and define full-queue behavior.
Use directional parameters. The owner closes only after senders finish; multiple
senders need coordination. Not every channel needs closing. Sending a struct
does not isolate its referenced mutable data.

Call derived-context cancel functions unless ownership transfers.
`context.WithoutCancel` removes deadlines too; detached work needs its own owner,
timeout, and shutdown policy. Cleanup may need a separate bounded context.
Stop admission, finish or cancel active work, collect outcomes, then close
resources. A wait timeout alone does not stop workers.

Test blocked cancellation, early consumer exit, bounds, and failure propagation
as applicable. A passing race test only checks executed paths; it does not prove
termination or leak freedom.

Sources: [Mutex or channel](https://go.dev/wiki/MutexOrChannel),
[Go pipelines](https://go.dev/blog/pipelines),
[errgroup](https://pkg.go.dev/golang.org/x/sync/errgroup).
