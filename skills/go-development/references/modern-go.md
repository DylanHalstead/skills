# Version-aware Go

Use newer standard features when they simplify changed code without altering its
contract. Check the module's `go` directive and relevant build constraints, not
just `go version`. Preserve sound repository conventions; avoid unrelated
modernization or automatic dependency upgrades.

| Minimum Go | Useful choices |
| --- | --- |
| 1.21 | `min`/`max`, `slices.Contains`/`SortFunc`, `maps.Clone`/`Copy` instead of equivalent boilerplate. Preserve sort stability; clones are shallow. |
| 1.22 | `range n` for zero-based count loops. Loop-declared variables have per-iteration identity; `tt := tt` is unnecessary, but assignment to existing variables still shares them. |
| 1.23 | `slices.Sorted(maps.Keys(m))` for deterministic keys; consume iterators directly when no slice is needed. |
| 1.24 | `strings.SplitSeq`/`FieldsSeq` for iteration without materializing all parts. JSON `omitzero` when zero means absent; preserve wire semantics and distinguish zero from empty. |
| 1.26 | `new(value)` instead of pointer-only helpers; type constants for the desired pointer type. `errors.AsType[T]` for typed error matching. |

Keep simple direct map loops. `slices.Clip` restricts capacity; it does not release
the backing allocation. Do not change serializers or adopt experimental APIs as
style cleanup. Check official release notes for additions beyond this shortlist.

Further reading: [JetBrains guidelines](https://github.com/JetBrains/go-modern-guidelines),
[Go release notes](https://go.dev/doc/devel/release),
[`slices`](https://pkg.go.dev/slices).
