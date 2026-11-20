---
title: Go Testing Recipes
type: reference
tags: [technical-knowledge, go, testing, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://go.dev/doc/tutorial/add-a-test
  - https://pkg.go.dev/testing
---

# Go Testing Recipes

## Run tests and coverage

```sh
go test ./...
go test -race ./...
go test -coverprofile=coverage.out ./...
go tool cover -html=coverage.out
```

Race detector catches data races in exercised paths; it does not prove race freedom for untested code.

## Table-driven tests

```go
func TestNormalize(t *testing.T) {
 cases := []struct{name, input, want string}{
  {"trims", " Ada ", "Ada"},
  {"empty", "", ""},
 }
 for _, tc := range cases { t.Run(tc.name, func(t *testing.T) {
  if got := Normalize(tc.input); got != tc.want { t.Fatalf("got %q want %q", got, tc.want) }
 }) }
}
```

Use subtests for readable case names; compare semantics rather than internal calls unless interaction is part of contract.

## HTTP handler test

```go
req := httptest.NewRequest(http.MethodGet, "/health", nil)
rec := httptest.NewRecorder()
router.ServeHTTP(rec, req)
if rec.Code != http.StatusOK { t.Fatalf("status = %d", rec.Code) }
```

Test success, invalid input, missing auth, and dependency failures. Use injected fake interfaces to avoid network/database coupling.

## Test cancellation / concurrency

Create context with timeout/cancel and assert work stops; use channels rather than sleeps to coordinate goroutines. Run targeted tests with `-race` and repeat flaky tests to expose scheduling issues.

## Benchmark

```go
func BenchmarkParse(b *testing.B) {
 for b.Loop() { _, _ = Parse(input) }
}
```

Use stable representative input and compare with `benchstat`; benchmark only after correctness and profile evidence.

## Read next

[[Go Table-Driven Tests]] · [[Go Recipes]] · [[Unit Integration and End-to-End Tests]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
