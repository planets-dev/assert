# assert

A lightweight Go testing assertion library with a clean, generic API.

## Installation

```bash
go get github.com/planets-dev/assert
```

## Usage

```go
import "github.com/planets-dev/assert"
```

All functions take `*testing.T` as the first argument and call `t.Helper()` so failures point to your test line, not inside the library.

## Functions

### `Equal[T any](t, got, want T)`
Fails if `got` and `want` are not equal. Uses `.Equal(T) bool` if the type implements it, otherwise falls back to `reflect.DeepEqual`.

```go
assert.Equal(t, result, 42)
assert.Equal(t, name, "alice")
```

### `NotEqual[T any](t, got, want T)`
Fails if `got` and `want` are equal.

```go
assert.NotEqual(t, status, "error")
```

### `True(t, got bool)`
Fails if `got` is `false`.

```go
assert.True(t, user.IsActive())
```

### `False(t, got bool)`
Fails if `got` is `true`.

```go
assert.False(t, list.IsEmpty())
```

### `Nil(t, got any)`
Fails if `got` is not nil. Works correctly with typed nils (pointers, slices, maps, channels, funcs).

```go
assert.Nil(t, err)
```

### `NotNil(t, got any)`
Fails if `got` is nil.

```go
assert.NotNil(t, result)
```

### `ErrorIs(t, got, want error)`
Fails if `errors.Is(got, want)` returns false. Supports wrapped errors.

```go
assert.ErrorIs(t, err, ErrNotFound)
```

### `ErrorAs(t, got error, target any)`
Fails if `got` is nil or `errors.As(got, target)` returns false.

```go
var e *MyError
assert.ErrorAs(t, err, &e)
```

### `MatchesRegexp(t, got, pattern string)`
Fails if `got` does not match the regexp `pattern`. Fatally fails if the pattern is invalid.

```go
assert.MatchesRegexp(t, email, `^[^@]+@[^@]+\.[^@]+$`)
```

## License

MIT