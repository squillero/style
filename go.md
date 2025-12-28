# Go

> First draft. Follow with care.

## Identifiers (TL;DR)

- **CamelCase:** `privateName` (ie. *unexported*) vs. `GlobalName` (ie. *exported*. The rule apply to everything: variables, functions, structs and their fields, interfaces, types, constants, ... 
- **Proportionality rule:** Link the length of an identifier to its scope and the frequency of its use. One-letter names are fine for disposable loop indexes (eg. `i`, `t`).
- **Universal idioms:** Use `ctx` for context; `err` for error; `v, ok` for *comma-ok* idioms; etc.

## Variables

- Keep acronyms consistent in case (eg. `userID`).
- Keep names short and consistent. Eg. `c` for `Client`.
- Avoid generic names like `me`, `self`, ...

## Functions

- Functions that perform an action should be named using verbs (eg. `LaunchRocket()`).
- Use `field` (or `Field`) for getters; use `setField` (or `SetField`) for setters.

## Interfaces

- Keep them short!
- One-method interface: use the method name + `-er` (eg. `Split()` and `Splitter{}`).
- Multiple-method interface: use a meaningful name (eg. `Codec`).

## Packages

- Always lowercase, single word.
- Avoid generic names.

## File names

- No space, reasonably short, all lowercase.

## Format

Use `gofmt`.

## Coding Styles

> [*Clear is better than clever.*](https://go-proverbs.github.io/)

### Error Handling

```go
if err := doSomething(); err != nil {
    // ...
}
```

or (note the comment)

```go
if err := doSomething(); err == nil { // No error
    // ...
}
```

Note the `:=`

```go
u, err := db.UserByID(userID)
if err != nil {
    return fmt.Errorf("invalid origin user: %s", err)
}
user = u
```

## Documentation

> [*Documentation is for users.*](https://go-proverbs.github.io/)
