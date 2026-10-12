# Client design

## Start with the operation contract

Identify inputs, results, failure behavior, and what successful return means.
Distinguish a completed write from accepted asynchronous work, an empty result
from failed retrieval, and a known rejection from an ambiguous remote outcome.
Decide which transport or provider details belong in the public contract and
translate the rest at the boundary that owns them. Preserve streaming when
results can be large; convenience should not imply unbounded buffering.

## Separate client lifetime from call lifetime

Keep stable dependencies and configuration with the reusable client. Pass context,
request data, and operation overrides per call. A constructor may use context for
initialization without retaining it for later requests. Finish configuration before
concurrent use; apply call overrides to call-local settings, not shared fields.

Give mutable state the lifetime its guarantee requires. Backoff progression
usually belongs to one operation, while a quota or connection pool may intentionally
coordinate many operations. Use factories when fresh state is needed. Copy
caller-owned maps/slices when isolation is required; a struct copy is shallow.

## Choose configuration from actual variability

Keep required inputs explicit. Choose the smallest API that makes valid use clear:

| Shape | Use when | Cost to consider |
| --- | --- | --- |
| Ordinary parameters | Inputs are few, required, and stable. | Growing positional parameters and booleans become hard to distinguish. |
| Config struct | Related settings need inspection, storage, or validation as a group. | Zero may be meaningful rather than absent; shared mutable fields need ownership. |
| Functional options | Optional behaviors need defaults and room to evolve without many constructor variants. | Ordering, repetition, and invalid combinations become part of the contract. |

Resolve defaults and explicit settings before validating the complete configuration.
Document whether repeated options replace or accumulate values. For example, if
zero means "no timeout," omitted and explicitly zero must remain distinguishable.
A presence-bearing config field or a `WithTimeout` option can both express that
distinction.

A function option is enough for simple setters. An opaque option interface earns
its machinery when richer option types or API control are needed. A function hook
can express one policy operation; an interface can express a cohesive multi-method
contract. Follow an existing library's configuration API rather than wrapping it
just to impose a preferred pattern. Report invalid configuration at construction
instead of deferring it to requests or unexpectedly panicking.

## Put dependency interfaces with their consumers

Start with concrete dependencies or existing transport/SDK injection seams.
Introduce a narrow interface when a consumer needs substitution or an explicit
contract; include only the operations it uses. Match method signatures exactly,
including variadic SDK operation options. Do not reproduce the entire SDK or add
an adapter merely to satisfy a test. Prefer concrete returns when callers benefit
from an implementation's evolving API.

Library-owned extension interfaces follow the same reasoning: the library consumes
the policy or plugin and owns that contract. They are different from an interface
exported solely so other packages can mock the library. Add compile-time assertions
when conformance is a meaningful API promise; an injection-site assignment often
already checks it.

Add an application wrapper when it hides application policy, conversion, or
protocol details that callers would otherwise need to understand or coordinate.

## Make resource ownership explicit

Document which clients, transports, loggers, or connections are owned versus
borrowed. The owner handles shutdown and flush; a consumer must not close shared
resources after each request. Reuse HTTP clients and transports to retain connection
pools. Customize an owned transport, commonly by cloning `http.DefaultTransport`,
rather than mutating a shared default.

Define who closes returned streams and response bodies on success and failure,
including when both a response and error are returned. Bound draining for connection
reuse and error-body reads. Preserve those contracts in fakes and custom handlers.

## Design the failure policy

Retry only operations safe to replay or protected by an actual idempotency
contract. A replayable request body alone does not make a POST safe after an
ambiguous outcome. Choose which failures merit another attempt, how long to wait,
where retry state belongs, and which layer executes the retries. Prefer an SDK's
policy hooks or decorators to a second retry loop.

Use an overall context deadline that includes attempts and waits. Check whether
limits count total attempts or retries after the first attempt, and what zero
means. A maximum backoff delay is not a total deadline. Preserve cancellation,
permanent failures, and server retry hints when replacing policy. Use jitter
when synchronized retries would overload a shared dependency. Account for retries
inside the SDK, transport, caller, and queue before adding another layer.

## Verify guarantees, not structure

Test configuration defaults, explicit values, conflicts, and invalid combinations
as applicable to the chosen API. Cover retry classification, cancellation during
backoff, exhaustion, body replay, and cleanup when those behaviors change. Use
injected transports or existing testing seams; avoid real network calls and long
sleeps. Assert outcomes and ownership, not private option representations or a
particular arrangement of helpers.

## Optional background

The guidance above is usable without opening these sources.

- [Go code review comments: interfaces](https://go.dev/wiki/CodeReviewComments#interfaces) — consumer contracts and concrete returns.
- [Functional options for friendly APIs](https://dave.cheney.net/2014/10/17/functional-options-for-friendly-apis) — defaults, explicit configuration, and API evolution.
- [Contexts and structs](https://go.dev/blog/context-and-structs) — client versus per-call lifetime.
- [Timeouts, retries, and backoff with jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/) — retry safety, budgets, and load amplification.

## Dependency-specific notes

Use only the notes for a dependency involved in the task. These links are
navigation aids; their default branches or latest documentation may differ from
the project's dependency version. When a change depends on an API detail,
verify it against the project's resolved dependency source or matching
documentation.

- **GAX v2:** [call options](https://github.com/googleapis/gax-go/blob/main/v2/call_option.go)
  and [Invoke](https://github.com/googleapis/gax-go/blob/main/v2/invoke.go) scope
  a retryer to each call through a factory. Return fresh stateful backoff there.
  `WithTimeout` covers all attempts, but an existing context deadline takes
  precedence; set that deadline explicitly when you need a tighter bound.
- **AWS SDK v2:** [retry documentation](https://docs.aws.amazon.com/sdk-for-go/v2/developer-guide/configure-retries-timeouts.html)
  explains the standard retryer's quota bucket. Return a new retryer on each
  `config.WithRetryer` factory invocation to avoid unintentionally sharing quota
  across clients; reuse the resulting client. `AddWithMaxAttempts(r, 0)` permits
  unlimited attempts, while `NewStandard` with `MaxAttempts <= 0` uses its default.
- **retryablehttp:** [client and policy hooks](https://github.com/hashicorp/go-retryablehttp/blob/main/client.go)
  separate retry classification, delay, and exhaustion handling. Configure them
  before concurrent use. `RetryMax` counts retries after the initial request.
  Converting a generic reader to a replayable body can buffer it. On exhaustion,
  the default handler closes the response body; `PassthroughErrorHandler` leaves
  it to the caller, even when returning an error.
- **net/http:** [client and transport docs](https://pkg.go.dev/net/http#Client)
  define connection reuse, concurrency, timeout scope, and response ownership.
