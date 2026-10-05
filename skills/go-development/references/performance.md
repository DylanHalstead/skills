# Performance work

Ordinary efficient code needs no profiling ceremony: preallocate when size is
known, avoid repeated regex compilation, and stream instead of buffering whole
payloads. Use `strconv` for plain primitive conversions and `strings.Builder`
for incremental string construction when they simplify the code.

For an optimization, define workload and metric: latency, throughput, CPU,
allocation rate, retained memory, or contention. Check algorithms and external
round trips before runtime tuning. Preserve error, ordering, and resource contracts.

1. Establish a representative benchmark or workload baseline, including relevant
   input sizes and concurrency. Keep setup outside timing. Prefer `b.Loop()` on
   Go 1.24+; setup that sizes fixtures from `b.N` needs restructuring, not a loop
   replacement. Prevent elimination of the measured work.
2. Diagnose CPU with `pprof`; distinguish allocation churn (`alloc_space`) from
   retention (`inuse_space`). Use mutex/block profiles or execution traces for
   contention and scheduling, and existing request traces for external delays.
3. Change one hypothesis. Remove repeated work or improve algorithms before
   pooling, caching, `unsafe`, or runtime knobs. Pointer parameters do not
   guarantee fewer allocations.
4. Compare repeated runs with equivalent toolchain, flags, machine, and workload.
   Run variants serially on shared hardware. Use `benchstat` when available;
   report noise rather than retrying until results look favorable.

```sh
go test -run='^$' -bench='^BenchmarkName$' -benchmem -count=10 ./path/to/package
# Save before/after output separately, then: benchstat before.txt after.txt
```

Use actual names/paths. Do not use race-instrumented timings for production claims.
Keep profiling endpoints private. Bound caches and pooled buffer retention;
define freshness and ownership, and never return memory already released to a
pool. Rerun correctness tests and retain changes only when measured benefit
warrants complexity. Report workload, before/after metrics, and uncertainty.

Sources: [Go diagnostics](https://go.dev/doc/diagnostics),
[Benchmarks](https://pkg.go.dev/testing#hdr-Benchmarks).
