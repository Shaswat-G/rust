# Chapter 2: Programming a Guessing Game

Link: [Book Chapter 02]

## Scope and paths
- `use` binds a path into the current scope; `::` separates path segments (`std` → `io` → `stdin`). Without `use std::io;`, write `std::io::stdin()`.
- The std prelude is imported implicitly; everything else needs `use`.
- `use rand::prelude::*;` glob-imports the crate's common items, including the traits that provide `random_range`. Trait methods resolve only when the trait is in scope.

## Bindings and references
- `let` binds immutably; `let mut` permits reassignment and mutation.
- `String::new()` is an associated function (no `self`) returning an empty `String`; `new` is a convention, not a language constructor.
- `&x` borrows immutably, `&mut x` borrows mutably; the callee mutates the caller's value without taking ownership. `read_line(&mut guess)` appends the line, including `\n`, to `guess`.
- Shadowing (`let guess: u32 = …` over a `String` `guess`) declares a new binding that may change type; `mut` cannot.

## Result and match
- `io::stdin().read_line` returns `Result<usize, io::Error>` (bytes read). `Result<T, E>` is an enum with variants `Ok(T)` and `Err(E)`; ignoring it triggers a `#[must_use]` warning.
- `.expect(msg)` returns the `Ok` value or panics with `msg` on `Err`.
- `match` compares a value against patterns in order and evaluates the first matching arm; the compiler rejects non-exhaustive matches.
- `parse()` is generic over its target; `let guess: u32` selects `u32::from_str`. `Err(_) => continue` discards the error and restarts the loop.
- `guess.cmp(&secret_number)` returns `Ordering` (`Less`, `Equal`, `Greater`); `secret_number` is inferred as `u32` from the comparison.

## Types
- Statically typed with local inference; annotate when inference is ambiguous (`parse`).
- Integers: `i32` (default), `u32`, `i64`, … where `i`/`u` mark signed/unsigned and the suffix gives the bit width.

## Ranges, loops, comments
- `a..=b` includes both bounds; `a..b` excludes `b`. `rand::rng().random_range(1..=100)` samples from the inclusive range using the thread-local generator.
- `loop` repeats until `break`; `continue` skips to the next iteration.
- `//` starts a line comment.

## Dependencies
- Declare crates under `[dependencies]` in `Cargo.toml`: `rand = "0.10.1"` means `^0.10.1`, i.e. any semver-compatible version ≥ 0.10.1 and < 0.11.0.
- A crate is a compilation unit; a package (one `Cargo.toml`) contains one or more crates.
- The first build resolves the dependency graph, including transitive dependencies, downloads crates from crates.io, and records the exact versions in `Cargo.lock`. Later builds reuse the lockfile.
- `cargo update` re-resolves to the newest versions allowed by `Cargo.toml` and rewrites `Cargo.lock`.
- `cargo doc --open` builds local documentation for the package and its dependencies and opens it in a browser.

[Book Chapter 02]: https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html
