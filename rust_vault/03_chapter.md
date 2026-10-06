# Chapter 3: Common Programming Concepts

Link: [Book Chapter 03]

## Variables and constants
- Bindings are immutable by default; `let mut` permits reassignment and mutation.
- Shadowing with `let` creates a new binding, which may have a different type. It can also transform a value while keeping the same name.
- Constants use `const`, require an explicit type, and must be evaluable at compile time. By convention, names use `SCREAMING_SNAKE_CASE`.

## Types
- Rust is statically typed: every value's type is known at compile time, often through inference. Add annotations when inference is ambiguous or clarity requires them.
- Scalar types: integers (`i8`…`i128`, `u8`…`u128`, plus `isize`/`usize`), floating point (`f32`, `f64`), `bool`, and Unicode scalar `char` (4 bytes). Integer literals default to `i32`; floats to `f64`.
- Integer ranges: signed `iN` spans `−2^(N−1)` through `2^(N−1)−1`; unsigned `uN` spans `0` through `2^N−1`. Overflow behavior depends on the build mode and operation; it is not always a compile-time error.
- Tuples have fixed length and may mix types; destructure them or access fields by zero-based position (`pair.0`). The unit type `()` is an empty tuple.
- Arrays have fixed length and a single element type: `[T; N]`. Out-of-bounds indexing panics at runtime. Use `Vec<T>` when the collection's length must change.

## Functions and control flow
- Declare functions with `fn`; parameter types are required. Arguments are the values passed at a call.
- Statements perform actions and do not return values; expressions evaluate to values. A trailing expression has no semicolon. Functions return the final expression, or use `return`; declare the return type with `->`.
- `if` is an expression; its condition must be `bool`, and all branches must produce compatible types. `loop` repeats until `break`; `while` repeats while a condition is true; `for` iterates over an iterator, commonly a range (`1..=5` includes both bounds).
- `//` begins a line comment. Comments explain intent or context that code alone does not make clear.

## Keywords
Keywords are reserved by the language and cannot be used as ordinary identifiers; some are reserved for future use.

[Book Chapter 03]: https://doc.rust-lang.org/book/ch03-00-common-programming-concepts.html
