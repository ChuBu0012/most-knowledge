---
title: "Go Recipes"
type: reference
domain: go
tags: [technical-knowledge, api-reference, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://go.dev/doc/
---

# Go Recipes

คู่มือค้นจากงานที่ต้องทำ ตัวอย่างมุ่งที่ API/คำสั่งที่ใช้บ่อย; ตรวจ runtime/compiler version ในโปรเจกต์ก่อนใช้

## สร้าง module และรันโปรแกรม

```sh
go mod init example.com/myapp
go run ./cmd/server
go build ./...
go test ./...
```

`go.mod` เป็น module path และ dependency graph; commit `go.sum`. ระบุ Go toolchain ที่ใช้ใน CI/deployment ให้สอดคล้องกับ `go.mod`.

## ประกาศ function, struct และ method

```go
type User struct { ID string; Name string }
func (u User) DisplayName() string { return u.Name }
func FindUser(id string) (User, error) {
    if id == "" { return User{}, errors.New("id is required") }
    return User{ID: id, Name: "Ada"}, nil
}
```

ใช้ pointer receiver เมื่อ method ต้องแก้ receiver หรือ struct ใหญ่; value receiver เมื่อค่าควรเป็น immutable snapshot. Return zero value พร้อม error; อย่าซ่อน failure.

## จัดการ error

```go
user, err := FindUser(id)
if err != nil { return fmt.Errorf("find user %q: %w", id, err) }
if errors.Is(err, sql.ErrNoRows) { /* map to not found */ }
```

ตรวจ error ทันที; `%w` รักษาสายเหตุสำหรับ `errors.Is/As`. ใช้ sentinel/type error เมื่อ caller ต้องตัดสินจากชนิดสาเหตุ ไม่เทียบข้อความ.

## สร้าง HTTP handler

```go
func getUser(w http.ResponseWriter, r *http.Request) {
    id := r.PathValue("id")
    user, err := store.Find(r.Context(), id)
    if err != nil { http.Error(w, "not found", http.StatusNotFound); return }
    w.Header().Set("Content-Type", "application/json")
    _ = json.NewEncoder(w).Encode(user)
}
```

ส่ง `r.Context()` ลง database/network call; ตั้ง timeout, validate input และแยก internal error จากข้อความที่ส่ง client. อย่าละเลย encode error ในระบบที่ต้องรับประกัน response.

## ทำงานพร้อมกันด้วย goroutine/channel

```go
results := make(chan Result, len(ids))
for _, id := range ids {
    go func(id string) { results <- fetch(ctx, id) }(id)
}
for range ids { handle(<-results) }
```

กำหนด owner ของการปิด channel, จำกัด concurrency เมื่อ input โต, propagate cancellation ผ่าน context และป้องกัน goroutine leak เมื่อ consumer หยุดอ่าน.

## สร้าง table-driven test

```go
func TestNormalize(t *testing.T) {
    cases := []struct{name, input, want string}{{"trim", " Ada ", "Ada"}}
    for _, tc := range cases { t.Run(tc.name, func(t *testing.T) {
        if got := Normalize(tc.input); got != tc.want { t.Fatalf("got %q want %q", got, tc.want) }
    }) }
}
```

ใช้ `t.Helper()` ใน assertion helper; `t.Parallel()` เมื่อ test ไม่แชร์ mutable state/resource. ตรวจ race ด้วย `go test -race ./...`.

## ค้นต่อ

[[Go Error Handling]] · [[Go Context]] · [[Go Goroutines]] · [[Go Channels]] · [[Go HTTP Handler Boundaries]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
