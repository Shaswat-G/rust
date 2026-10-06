# Chapter 6: Enums and Pattern Matching

Link: [Book Chapter 06]

## Enums
- An enum defines a type as a set of named variants. Each variant may carry data, so the type encodes both which case applies and its associated value.
- Variants can hold different types and amounts of data. Their names also act as constructors: `IpAddr::V4(String)` constructs a `V4` value.
- Enums can have methods defined in `impl` blocks, just like structs.

```rust
enum IpAddr {
    V4(String),
    V6(String),
}

let home = IpAddr::V4(String::from("127.0.0.1"));
```

## `Option<T>`
- `Option<T>` represents a value that may be absent: `Some(T)` or `None`. Rust has no null value; an `Option<T>` makes absence explicit in the type.
- Code must handle `None` before using the inner `T`. Pattern matching can safely extract the value.

```rust
enum Option<T> {
    None,
    Some(T),
}
```

The standard library defines `Option<T>`; the declaration above illustrates its shape.

## Pattern matching
- `match` compares a value against patterns in order and evaluates the first matching arm. Each arm is `pattern => expression`; all arms must produce compatible types.
- Matches must be exhaustive, so every possible variant or value must be covered. Use `_` to ignore any remaining case, or a named binding such as `other` when the value is needed. A catch-all arm must come last.
- `if let pattern = value { ... }` handles one pattern when other cases do not need distinct handling. Add `else` for the remaining cases; use `let ... else` when the nonmatching case should exit the current scope.

[Book Chapter 06]: https://doc.rust-lang.org/book/ch06-00-enums.html
