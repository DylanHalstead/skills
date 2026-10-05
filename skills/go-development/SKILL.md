---
name: go-development
description: "Write, test, review, refactor, and debug Go (Golang) code using version-aware idioms, behavior-focused tests, and explicit resource and goroutine ownership. Use for Go implementation, code review, failing tests, bugs, or performance work."
---

# Go development

Optimize for the reader. Follow project instructions, established patterns, and
lint configuration. Check the owning module's Go version, not just the installed
toolchain, before choosing language features or APIs.

## Go conventions

- Use `gofmt`; use `goimports` and import grouping configured by the repository.
- Name packages for what they provide; avoid catch-all packages and name stutter.
  Keep initialisms (`userID`, `httpClient`) and receiver names consistent.
- Prefer keyed struct literals; omit redundant zero values. Make zero values
  useful or document required construction. Embed only when promoted methods
  belong in the API.
- Choose receivers from mutation, identity, and copy safety; keep receiver kinds
  consistent by default. Never copy a used lock-bearing type. Struct copies and
  collection clones do not isolate nested slices, maps, or pointers.
- Put `ctx context.Context` first where it flows. Propagate it to I/O; keep it out
  of long-lived dependency structs and use values for request metadata, not DI.
- Document exported APIs and non-obvious contracts: mutation, ownership,
  concurrent use, cancellation, and completion guarantees. Explain rationale
  rather than narrating statements. Handle failures early to keep nesting shallow.

## Dependencies and interfaces

Wire clients and configuration at the entry point and inject them through
constructors or parameters. Avoid mutable globals, service lookup, and I/O in
`init()`. Reuse long-lived clients; validate required configuration at startup.

Start with concrete types; reuse transport/SDK injection seams for tests.
Define narrow interfaces in the consuming package when substitution or a contract
needs one; neither mirror producers nor require multiple implementations. Reuse
standard interfaces. Prefer concrete returns unless hiding implementation serves
the API, and plain constructors/config structs before functional options or DI
tools. A typed nil pointer in an interface is non-nil; when returning no error,
return a nil `error` interface rather than a typed nil pointer.

## Errors, logging, and resources

Add useful operation context. Wrap with `%w` when cause identity belongs in the
contract; translate implementation-specific failures at the boundary that owns
it. Inspect identity/type with `errors.Is`/`errors.As`, not message parsing.
Use lowercase error messages without trailing punctuation; justify ignored
errors. Return expected failures rather than panicking.

Let the responsible boundary log failures; avoid logging and returning the same
error for another layer to log again. Use the established structured logger,
stable messages, and safe fields. Redact credentials and PII, including values
third-party errors may echo.

Give resources one cleanup owner. Close bodies and iterators, check iteration
errors, and propagate write/flush/close failures that affect correctness. Release
per-item resources during long loops. Preserve streaming and bound payloads,
batches, and pending writes. Enqueue success is not completion; collect deferred
failures. Retry only with failure classification, idempotency, and bounded
attempts/deadlines, accounting for SDK retries.

## Testing

Use test-first or implementation-first development as the task warrants; complete
behavioral tests with the change. Derive expected results from requirements and contracts,
not the implementation. For bugs, add a regression test that reproduces the
failure; confirm it fails against the unfixed code when practical. For
behavior-preserving refactors, start with green tests and add characterization
coverage where needed. Do not weaken assertions to fit code or claim test
results you did not observe.

Use named table-driven `t.Run` tests by default when cases share a useful setup
and assertion shape. Keep coordination-heavy or distinct scenarios separate rather
than forcing them into a table. Cover relevant boundaries and error paths; test
results and required side effects, not private calls. Use fresh dependencies per
subtest and `t.Cleanup` for owned resources. Parallelize only isolated tests.

## References and checks

- [Modern Go](references/modern-go.md): read when choosing features or APIs.
- [Testing](references/testing.md): read for table setup, fakes, or assertions.
- [Concurrency](references/concurrency.md): read before changing goroutines,
  channels, cancellation, synchronization, or shutdown.
- [Performance](references/performance.md): read for optimization or benchmarks.

Format changed Go files and use repository checks: focused tests while developing,
tests covering affected callers afterward, race tests for concurrency changes,
and broader gates as risk warrants. Run checks from the owning module with the
required build tags; `./...` there does not cover other workspace modules.
`go build` does not compile tests. Tidy modules when dependencies change and
inspect the module diff; do not upgrade targets or install tools without
permission. Report check commands, results, and gaps.
