[![codecov](https://codecov.io/gh/confetti-framework/errors/branch/main/graph/badge.svg?token=8ANZG4V48V)](https://codecov.io/gh/confetti-framework/errors)

# Errors

Package errors provides simple error handling primitives.

`go get github.com/confetti-framework/errors`

The traditional error handling idiom in Go is roughly akin to
```go
if err != nil {
        return err
}
```
which applied recursively up the call stack results in error reports without context or debugging information. The errors package allows programmers to add context to the failure path in their code in a way that does not destroy the original value of the error.

## Adding context to an error

The errors.Wrap function returns a new error that adds context to the original error. For example
```go
_, err := ioutil.ReadAll(r)
if err != nil {
        return errors.Wrap(err, "read failed")
}
```
## Retrieving the cause of an error

Using `errors.Wrap` constructs a stack of errors, adding context to the preceding error. Depending on the nature of the
error it may be necessary to reverse the operation of errors.Wrap to retrieve the original error for inspection. Any
error value which implements this interface can be inspected by `errors.Unwrap`.
```go
type causer interface {
        Unwrap() error
}
```

`errors.Unwrap` will recursively retrieve the topmost error which does not implement `causer`, which is assumed to be
the original cause. For example:
```go
switch err := errors.Unwrap(err).(type) {
case *MyError:
        // handle specifically
default:
        // unknown error
}
```

<<<<<<< HEAD
=======
[Read the package documentation for more information](https://godoc.org/github.com/confetti-framework/errors).

>>>>>>> 762b551bf121c3fb7483623472bf3090cafff8d7
## Contributing

Before sending a PR, please discuss your change by raising an issue.
