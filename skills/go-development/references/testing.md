# Table-driven tests

Use named cases and fresh dependencies inside `t.Run`. Keep simple expectations
in `want` fields; add per-case `setup` and `check` functions when scenarios need
different dependencies or assertions.
Bind testify to the subtest's `t` when installed: `require` for prerequisites,
`assert` for independent comparisons. Prefer small fakes or injected transports
to introducing a mock framework.

This example tests `ReadName(io.Reader)`, an API that decodes a JSON object's
`name` field and preserves read-error identity. Imports: `errors`, `io`, `strings`,
`testing`, and `testing/iotest`.

```go
func TestReadName(t *testing.T) {
	readFailed := errors.New("read failed")
	tests := []struct {
		name    string
		setup   func() io.Reader
		want    string
		wantErr error
	}{
		{
			name:  "reads name",
			setup: func() io.Reader { return strings.NewReader(`{"name":"Ada"}`) },
			want:  "Ada",
		},
		{
			name:    "propagates read failure",
			setup:   func() io.Reader { return iotest.ErrReader(readFailed) },
			wantErr: readFailed,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got, err := ReadName(tt.setup())
			if !errors.Is(err, tt.wantErr) {
				t.Fatalf("ReadName() error = %v, want %v", err, tt.wantErr)
			}
			if got != tt.want {
				t.Errorf("ReadName() = %q, want %q", got, tt.want)
			}
		})
	}
}
```

Use barriers or `testing/synctest` (Go 1.25+) for coordinated concurrency tests.
Prefer `t.Context()` (Go 1.24+) for test-scoped work; cleanup I/O needs another
bounded context because test context cancellation precedes cleanup. Fakes must
honor required stream consumption and deferred failures.
