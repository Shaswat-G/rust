# Chapter 1: Getting Started

These notes cover the setup, first program, compilation, and Cargo workflow introduced in Chapter 1 of *The Rust Programming Language*.

## Installing Rust

Install Rust with **rustup**, the toolchain manager. It installs and manages the Rust compiler (`rustc`) and Cargo, and can select toolchain versions and targets. After installation, check that the tools are available on your `PATH`:

```sh
rustc --version
cargo --version
```

`rustc` compiles Rust source code. Cargo is the usual tool for creating, building, checking, and running Rust packages.

## The first program

Save this as `main.rs`:

```rust
fn main() {
    println!("Hello, world!");
}
```

- `fn main()` defines the program's entry-point function.
- Curly braces delimit the function body.
- `println!` is a macro invocation. The `!` distinguishes a macro from a function call; this macro prints text followed by a newline.
- The semicolon ends this statement. Rust also has expressions that can produce values and appear without a trailing semicolon; the semicolon is not required after every line.

Compile and run it directly with `rustc`:

```sh
rustc main.rs
./main
```

The compiler produces a native executable for the target platform. That executable is not generally portable across operating systems or processor architectures: it is built for a particular target and may depend on that system's runtime libraries. C++ is also commonly compiled to native machine code; it is not inherently an interpreted language. Python and JavaScript are often run by interpreters or virtual machines, though their implementations and execution strategies vary.

## Cargo projects

Cargo is Rust's build system and package manager. It invokes the compiler, manages dependencies, and provides consistent project commands. Create a binary package with:

```sh
cargo new hello_cargo
```

Cargo creates a directory containing `Cargo.toml` (the package manifest) and `src/main.rs` (the binary crate's source). By default, `cargo new` also initializes a Git repository unless told otherwise or run inside an existing repository; nested repositories may not be desirable in a larger learning repository. To add Cargo metadata to an existing directory, run `cargo init` there.

In Cargo terminology, a **package** is described by a manifest and can contain one or more crates. A **crate** is a Rust compilation unit, such as a binary or library. The terms are related but not interchangeable: a package is not simply another name for a directory or a crate.

### Common commands

Run these from the directory containing `Cargo.toml`:

| Command | Purpose |
| --- | --- |
| `cargo check` | Type-check and validate the project without producing a final executable. It is usually faster during development. |
| `cargo build` | Compile a debug build into `target/debug/`. |
| `cargo run` | Build the binary if needed, then run it. |
| `cargo build --release` | Compile an optimized release build into `target/release/`. |

Cargo stores generated build output in `target/`; this directory is normally excluded from version control. The `Cargo.lock` file records the resolved dependency versions. For binary applications, commit it so builds use the same dependency resolution; libraries commonly omit it from version control.

You can run a built executable directly, for example `./target/debug/hello_cargo` on Unix-like systems. `cargo run` is usually more convenient because it builds as needed and passes arguments after `--` to the program.

Release builds use optimizations that can improve runtime performance, but they take longer to compile and may behave differently in timing-sensitive measurements. Use release builds when measuring performance representative of deployment; use a proper benchmark setup rather than assuming every optimized run is a reliable benchmark.

## A practical learning workflow

Start a standalone exercise with `cargo new` (or use `cargo init` for an existing directory), make a small change, then use `cargo check` for quick compiler feedback and `cargo run` when you want to observe program behavior. Before committing, `cargo fmt` formats the code and `cargo check` confirms it still compiles. Run or test the program when the behavior itself needs checking; compilation alone cannot show that the result is correct.

## Configuration-file reflection

Cargo's manifest is written in TOML. TOML is designed to be readable and works well for configuration with tables and nested sections. JSON is common for machine-to-machine data, while YAML is often used for configuration that benefits from indentation-based nested structures. These are conventions rather than strict rules: choose a format based on the tools, schema, and readers involved, not nesting depth alone. Examples include `pyproject.toml`, `Cargo.toml`, `package.json`, and many Kubernetes manifests in YAML.

## Further references

- [[rust]] — vault index and links to other Rust notes
- [[rust_diagram.drawio]]
- [[rust_mindmap.xmind]]
